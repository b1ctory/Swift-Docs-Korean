## *Capturing Values : 값 캡쳐*

*A closure can capture constants and variables from the surrounding context in which it’s defined. The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.*

클로저는 클로저가 정의된 주변 컨텍스트에서 상수와 변수를 캡쳐할 수 있습니다. 그런 다음 클로저는 상수와 변수를 정의한 원래 범위가 더이상 존재하지 않더라도 해당 상수와 변수의 값을 참조하고 수정할 수 있습니다.

*In Swift, the simplest form of a closure that can capture values is a nested function, written within the body of another function. A nested function can capture any of its outer function’s arguments and can also capture any constants and variables defined within the outer function.*

Swift에서 값을 캡처할 수 있는 가장 간단한 형태의 클로저는 다른 함수의 본문 내에 작성된 중첩 함수입니다. 중첩함수는 외부 함수의 인수를 캡쳐할 수 있으며 외부 함수 내에 정의된 상수와 변수도 캡쳐할 수 있습니다.

*Here’s an example of a function called `makeIncrementer`, which contains a nested function called `incrementer`. The nested `incrementer()` function captures two values, `runningTotal` and `amount`, from its surrounding context. After capturing these values, `incrementer` is returned by `makeIncrementer` as a closure that increments `runningTotal` by `amount` each time it’s called.*

여기 `incrementer`라는 중첩 함수를 포함하는 `makeIncrementer`라는 함수의 예시가 있습니다. 중첩된 `incrementer()`함수는 주변 컨텍스트에서 `runningTotal`과 `amount` 의 두 값을 캡쳐합니다. 이러한 값을 캡쳐한 후 `incrementer`는 `makeIncrementer`에 의해 반환됩니다. `Incrementer`는 호출될 때마다 `runningTotal` 을 `amount` 만큼 증가시키는 클로저입니다.

```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}
```

*The return type of `makeIncrementer` is `() -> Int`. This means that it returns a function, rather than a simple value. The function it returns has no parameters, and returns an `Int` value each time it’s called. To learn how functions can return other functions, see [Function Types as Return Types](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID177).*

`makeIncrementer`의 반환 타입은 `() -> Int` 입니다. 즉 이것은 단순 값이 아닌 함수를 반환합니다. 반환되는 함수에는 매개변수가 없으며 호출될 때마다 `Int` 값을 반환합니다. 함수가 다른 함수를 반환하는 방법에 대해서는 [링크]를 참조하십시오.

*The `makeIncrementer(forIncrement:)` function defines an integer variable called `runningTotal`, to store the current running total of the incrementer that will be returned. This variable is initialized with a value of `0`.*

 `makeIncrementer(forIncrement:)` 함수는 `runningTotal`이라는 정수 변수를 정의해서 반환될 incrementer의 현재 실행 합계를 저장합니다. 이 변수는 `0`으로 초기화됩니다.

*The `makeIncrementer(forIncrement:)` function has a single `Int` parameter with an argument label of `forIncrement`, and a parameter name of `amount`. The argument value passed to this parameter specifies how much `runningTotal` should be incremented by each time the returned incrementer function is called. The `makeIncrementer` function defines a nested function called `incrementer`, which performs the actual incrementing. This function simply adds `amount` to `runningTotal`, and returns the result.*

 `makeIncrementer(forIncrement:)`함수는 인수 레이블이 forIncrement이고 매개변수 이름이 `amount` 인 단일 `Int` 매개변수를 가집니다. 이 매개변수에 전달된 인수 값은 반환된 증분함수가 호출될 때마다 `runningTotal` 이 얼마나 증가하는지 지정합니다. `makeIncrementer` 함수는 실제 증분을 수행하는 `incrementer`라는 중첩 함수를 정의합니다. 이 함수는 단순히 `runningTotal` 에 `amount`를 더하고 결과를 반환합니다.

*When considered in isolation, the nested `incrementer()` function might seem unusual:*

단일적으로 고려할 때, 중첩된 `incrementer()`함수는 비정상적으로 보일 수 있습니다.

```swift
func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
}
```

*The `incrementer()` function doesn’t have any parameters, and yet it refers to `runningTotal` and `amount` from within its function body. It does this by capturing a reference to `runningTotal` and `amount` from the surrounding function and using them within its own function body. Capturing by reference ensures that `runningTotal` and `amount` don’t disappear when the call to `makeIncrementer` ends, and also ensures that `runningTotal` is available the next time the `incrementer` function is called.*

`incrementer()`함수는 매개변수가 없지만 함수 본문 내에서 `total`과 `amount`를 실행하는 것을 의미하는 것입니다. 이것은 주변함수에서 `runningTotal`과 `amount`에 대한 참조를 캡쳐해서 함수 본체 내에서 사용함으로써 수행됩니다. 참조로 캡쳐하면 호출시 runningTotal과 amount가 사라지지 않습니다. `Incrementer`는 종료되며 다음에 `incrementer` 함수를 호출할 때 `runningTotal` 을 사용할 수 있도록 합니다.

> *NOTE*
> 
> *As an optimization, Swift may instead capture and store a copy of a value if that value isn’t mutated by a closure, and if the value isn’t mutated after the closure is created.*
> 
> 최적화를 위해 Swift는 클로저에 의해 값이 변하지 않고 클로저가 생성된 후 값이 변하지 않는 경우 값의 복사본을 캡쳐해서 저장할 수 있습니다.
> 
> *Swift also handles all memory management involved in disposing of variables when they’re no longer needed.*
> 
> Swift는 또한 변수가 더이상 필요하지 않을 때 변수 처리와 관련된 모든 메모리 관리를 처리합니다.

*Here’s an example of `makeIncrementer` in action:*

여기 `makeIncrementer`가 작동하는 예시가 있습니다.

```swift
let incrementByTen = makeIncrementer(forIncrement: 10)
```

*This example sets a constant called `incrementByTen` to refer to an incrementer function that adds `10` to its `runningTotal` variable each time it’s called. Calling the function multiple times shows this behavior in action:*

이 예에서는 호출될 때마다 `runningTotal` 변수에 `10`을 추가하는 증분 함수인 `incrementByTen`이라는 상수를 설정합니다. 함수를 여러번 호출하면 다음 동작이 표시됩니다.

```swift
incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
```

*If you create a second incrementer, it will have its own stored reference to a new, separate `runningTotal` variable:*

두번째 증분을 생성하면, 별도의 새 `runningTotal` 변수에 대한 자체 저장된 참조가 생성됩니다.

```swift
let incrementBySeven = makeIncrementer(forIncrement: 7)
incrementBySeven()
// returns a value of 7
```

*Calling the original incrementer (`incrementByTen`) again continues to increment its own `runningTotal` variable, and doesn’t affect the variable captured by `incrementBySeven`:*

원래 증분 (`incrementByTen`)을 호출하면 자체의 runningTotal 변수가 계속 증가하며 `incrementBySeven`에 의해 캡쳐된 변수에는 영향을 주지 않습니다.

```swift
incrementByTen()
// returns a value of 40
```

> *NOTE*
> 
> *If you assign a closure to a property of a class instance, and the closure captures that instance by referring to the instance or its members, you will create a strong reference cycle between the closure and the instance. Swift uses capture lists to break these strong reference cycles. For more information, see [Strong Reference Cycles for Closures](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID56).*
> 
> 클래스 인스턴스의 속성에 클로저를 할당하고 클로저가 인스턴스 또는 해당 멤버를 참조하여 해당 인스턴스를 캡처하면 폐쇄와 인스턴스 사이에 강력한 참조 주기가 생성됩니다. Swift는 캡처 목록을 사용하여 이러한 강력한 참조 주기를 중단합니다. 자세한 내용은 [링크]를 참조하십시오.
