## *Escaping Closures : 탈출 클로저*

*A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns. When you declare a function that takes a closure as one of its parameters, you can write `@escaping` before the parameter’s type to indicate that the closure is allowed to escape.*

클로저는 클로저가 함수에 인수로 전달될 때 함수를 탈출한다고 하지만 함수가 반환된 후에 호출됩니다. 클로저를 매개변수 중 하나로 사용하는 함수를 선언할 때 매개변수 타입 앞에 `@escaping` 을 입력해서 클로저가 탈출할 수 있음을 나타낼 수 있습니다.

*One way that a closure can escape is by being stored in a variable that’s defined outside the function. As an example, many functions that start an asynchronous operation take a closure argument as a completion handler. The function returns after it starts the operation, but the closure isn’t called until the operation is completed—the closure needs to escape, to be called later. For example:*

클로저가 탈출할 수 있는 한가지 방법은 함수 외부에 정의된 변수에 저장되는 것입니다. 예를 들어, 비동기 작업을 시작하는 많은 함수는 CompletionHandler로 클로저 인수를 사용합니다. 이 함수는 작업을 시작한 후에 반환되지만 작업이 완료될 때까지 클로저가 호출되지 않습니다. 나중에 클로저를 호출하려면 클로저를 탈출해야 합니다. 예를 들어 :

```swift
var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}
```

*The `someFunctionWithEscapingClosure(_:)` function takes a closure as its argument and adds it to an array that’s declared outside the function. If you didn’t mark the parameter of this function with `@escaping`, you would get a compile-time error.*

`someFunctionWithEscapingClosure(_:)` 함수는 클로저를 인수로 사용해서 함수 외부에 선언된 배열에 추가합니다. 이 함수의 매개변수를 `@escaping`으로 표시하지 않으면 컴파일 타임 오류가 발생합니다.

*An escaping closure that refers to `self` needs special consideration if `self` refers to an instance of a class. Capturing `self` in an escaping closure makes it easy to accidentally create a strong reference cycle. For information about reference cycles, see [Automatic Reference Counting](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html).*

`self`가  클래스의 인스턴스를 참조하는 경우 `self`를 참조하는 탈출 클로저는 특별한 고려가 필요합니다. 탈출 클로저에서 `self`를 포착하면 실수로 강력한 참조 사이클을 쉽게 만들 수 있습니다. 참조 사이클에 대한 자세한 내용은 [링크]를 참조하세요.

*Normally, a closure captures variables implicitly by using them in the body of the closure, but in this case you need to be explicit. If you want to capture `self`, write `self` explicitly when you use it, or include `self` in the closure’s capture list. Writing `self` explicitly lets you express your intent, and reminds you to confirm that there isn’t a reference cycle. For example, in the code below, the closure passed to `someFunctionWithEscapingClosure(_:)` refers to `self` explicitly. In contrast, the closure passed to `someFunctionWithNonescapingClosure(_:)` is a nonescaping closure, which means it can refer to `self` implicitly.*

일반적으로 클로저는 클로저 본문에서 변수를 사용해서 암시적으로 캡쳐하지만, 이 경우에는 변수를 명시적으로 캡쳐해야 합니다. `self`를 캡쳐하려면 사용할 때 self를 명시적으로 쓰거나 클로저의 캡쳐 목록에 `self`를 포함시키세요. self를 명시적으로 쓰면 자신의 의도를 표현할 수 있고 참조 사이클이 없음을 확인할 수 있습니다. 예를 들어, 아래 코드에서 `someFunctionWithEscapingClosure(_:)`함수로 전달된 클로저는 `self`를 명시적으로 나타냅니다. 대조적으로, 클로저는 `someFunctionWithNonescapingClosure(_:)`은 `self`를 암시적으로 지칭할 수 있는 비탈출 클로저입니다.

```swift
func someFunctionWithNonescapingClosure(closure: () -> Void) {
    closure()
}

class SomeClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { self.x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}

let instance = SomeClass()
instance.doSomething()
print(instance.x)
// Prints "200"

completionHandlers.first?()
print(instance.x)
// Prints "100"
```

*Here’s a version of `doSomething()` that captures `self` by including it in the closure’s capture list, and then refers to `self` implicitly:*

여기 클로저의 캡쳐 목록에 포함시켜 `self`를 캡쳐한다음 암시적으로 `self`를 나타내는 `doSomething()`의 버전이 있습니다.

```swift
class SomeOtherClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { [self] in x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}
```

*If `self` is an instance of a structure or an enumeration, you can always refer to `self` implicitly. However, an escaping closure can’t capture a mutable reference to `self` when `self` is an instance of a structure or an enumeration. Structures and enumerations don’t allow shared mutability, as discussed in [Structures and Enumerations Are Value Types](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID88).*

`self`가 구조체 혹은 열거형의 인스턴스인 경우 항상 암시적으로 `self`를 참조할 수 있습니다. 그러나 탈출 클로저는 `self`가 구조체 혹은 열거형의 인스턴스일 때 `self`에 대한 가변 참조를 캡쳐할 수 없습니다. [링크]에서 설명한 바와 같이 구조체 및 열거형은 공유 변동성을 허용하지 않습니다.

```swift
struct SomeStruct {
    var x = 10
    mutating func doSomething() {
        someFunctionWithNonescapingClosure { x = 200 }  // Ok
        someFunctionWithEscapingClosure { x = 100 }     // Error
    }
}
```

*The call to the `someFunctionWithEscapingClosure` function in the example above is an error because it’s inside a mutating method, so `self` is mutable. That violates the rule that escaping closures can’t capture a mutable reference to `self` for structures.*

위의 예시에서 `someFunctionWithEscapingClosure` 함수에 대한 호출은 변환 메서드 내부에 있으므로 `self`는 변환 가능하기 때문에 에러입니다.그것은 탈출 클로저가 구조체의 `self` 에 대한 가변적인 참조를 포착할 수 없다는 규칙을 위반합니다.
