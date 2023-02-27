## *ARC in Action*

*Here’s an example of how Automatic Reference Counting works. This example starts with a simple class called `Person`, which defines a stored constant property called `name`:*

다음은 자동 참조 카운팅 작동 방식의 예입니다. 이 예는 `name`이라는 상수 저장 프로퍼티를 정의하는 `Person`이라는 간단한 클래스로 시작합니다.

```swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}
```

*The `Person` class has an initializer that sets the instance’s `name` property and prints a message to indicate that initialization is underway. The `Person` class also has a deinitializer that prints a message when an instance of the class is deallocated.*

`Person` 클래스에는 인스턴스의 `name` 프로퍼티를 설정하고 초기화가 진행 중임을 나타내는 메시지를 출력하는 이니셜라이저가 있습니다. `Person` 클래스에는 클래스 인스턴스가 할당 해제될 때 메시지를 출력하는 초기화 해제자가 있습니다.

*The next code snippet defines three variables of type `Person?`, which are used to set up multiple references to a new `Person` instance in subsequent code snippets. Because these variables are of an optional type (`Person?`, not `Person`), they’re automatically initialized with a value of `nil`, and don’t currently reference a `Person` instance.*

다음 코드 스니펫은 후속 코드 스니펫에서 새로운 `Person` 인스턴스에 대한 여러 참조를 설정하는 데 사용되는 `Person?` 타입의 세 가지 변수를 정의합니다. 이러한 변수는 옵셔널 타입 (`Person`이 아닌 `Person?`)이므로 자동으로 `nil` 값으로 초기화되며 현재 `Person` 인스턴스를 참조하지 않습니다.

```swift
var reference1: Person?
var reference2: Person?
var reference3: Person?
```

*You can now create a new `Person` instance and assign it to one of these three variables:*

이제 새로운 `Person` 인스턴스를 만들어 다음 세 변수 중 하나에 할당할 수 있습니다.

```swift
reference1 = Person(name: "John Appleseed")
// Prints "John Appleseed is being initialized"
```

*Note that the message `"John Appleseed is being initialized"` is printed at the point that you call the `Person` class’s initializer. This confirms that initialization has taken place.*

`"John Appleseed is being initialized"`라는 메시지는 `Person` 클래스의 이니셜라이저를 호출하는 지점에 출력됩니다. 이것은 초기화가 수행되었음을 확인합니다.

*Because the new `Person` instance has been assigned to the `reference1` variable, there’s now a strong reference from `reference1` to the new `Person` instance. Because there’s at least one strong reference, ARC makes sure that this `Person` is kept in memory and isn’t deallocated.*

새 `Person` 인스턴스가 `reference1` 변수에 할당되었으므로 이제 `reference1`에서 새 `Person` 인스턴스로의 강력한 참조가 있습니다. 하나 이상의 강력한 참조가 있기 때문에 ARC는 이 `Person`이 메모리에 유지되고 할당이 취소되지 않도록 합니다.

*If you assign the same `Person` instance to two more variables, two more strong references to that instance are established:*

동일한 `Person` 인스턴스를 두 개의 추가 변수에 할당하면 해당 인스턴스에 대한 강력한 참조가 두 개 더 설정됩니다.

```swift
reference2 = reference1
reference3 = reference1
```

*There are now three strong references to this single `Person` instance.*

이제 이 단일 `Person` 인스턴스에 대한 세 가지 강력한 참조가 있습니다.

*If you break two of these strong references (including the original reference) by assigning `nil` to two of the variables, a single strong reference remains, and the `Person` instance isn’t deallocated:*

두 개의 변수에 `nil`을 할당하여 이러한 강력한 참조(원래 참조 포함) 중 두 개를 끊는 경우 하나의 강력한 참조가 유지되고 `Person` 인스턴스가 할당 해제되지 않습니다.

```swift
reference1 = nil
reference2 = nil
```

*ARC doesn’t deallocate the `Person` instance until the third and final strong reference is broken, at which point it’s clear that you are no longer using the `Person` instance:*

ARC는 세 번째이자 마지막 강한 참조가 끊어질 때까지 `Person` 인스턴스를 할당 해제하지 않습니다. 이 시점에서 `Person` 인스턴스를 더 이상 사용하지 않는다는 것이 분명해집니다.

```swift
reference3 = nil
// Prints "John Appleseed is being deinitialized"
```
