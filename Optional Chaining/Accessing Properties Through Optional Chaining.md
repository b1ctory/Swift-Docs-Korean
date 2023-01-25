## *Accessing Properties Through Optional Chaining : 옵셔널 체이닝을 통해 프로퍼티에 엑세스*

*As demonstrated in [Optional Chaining as an Alternative to Forced Unwrapping](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html#ID246), you can use optional chaining to access a property on an optional value, and to check if that property access is successful.*

[링크]에서 설명한 것처럼 옵셔널 체이닝을 사용하여 옵셔널 값으로 프로퍼티에 액세스하고 해당 프로퍼티에 액세스가 성공했는지 확인할 수 있습니다.

*Use the classes defined above to create a new `Person` instance, and try to access its `numberOfRooms` property as before:*

위에서 정의한 클래스를 사용하여 새 `Person` 인스턴스를 만들고 이전과 같이 `numberOfRooms` 프로퍼티에 액세스합니다:

```swift
let john = Person()
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "Unable to retrieve the number of rooms."
```

*Because `john.residence` is `nil`, this optional chaining call fails in the same way as before.*

`john.residence`가 `nil`이기 때문에 이 옵셔널 체이닝 호출은 이전과 동일한 방식으로 실패합니다.

*You can also attempt to set a property’s value through optional chaining:*

옵셔널 체이닝을 통해 프로퍼티 값을 설정할 수도 있습니다:

```swift
let someAddress = Address()
someAddress.buildingNumber = "29"
someAddress.street = "Acacia Road"
john.residence?.address = someAddress
```

*In this example, the attempt to set the `address` property of `john.residence` will fail, because `john.residence` is currently `nil`.*
이 예에서는 `john.residence`가 현재 `nil`이기 때문에 `john.residence`의 `address` 프로퍼티를 설정하려는 시도가 실패합니다.

*The assignment is part of the optional chaining, which means none of the code on the right-hand side of the `=` operator is evaluated. In the previous example, it’s not easy to see that `someAddress` is never evaluated, because accessing a constant doesn’t have any side effects. The listing below does the same assignment, but it uses a function to create the address. The function prints “Function was called” before returning a value, which lets you see whether the right-hand side of the `=` operator was evaluated.*

이 할당은 옵셔널 체이닝의 일부이며, 이는 `=` 연산자의 오른쪽에 있는 코드가 평가되지 않음을 의미합니다. 앞의 예에서는 상수에 접근해도 부작용이 없기 때문에 `someAddress`가 평가되지 않는다는 것을 쉽게 알 수 없습니다. 아래 목록은 동일한 할당을 수행하지만, 주소를 생성하는 함수를 사용합니다. 함수는 값을 반환하기 전에 "Function was called"를 출력하여 `=` 연산자의 오른쪽이 평가되었는지 여부를 확인할 수 있습니다.

```swift
func createAddress() -> Address {
    print("Function was called.")

    let someAddress = Address()
    someAddress.buildingNumber = "29"
    someAddress.street = "Acacia Road"

    return someAddress
}
john.residence?.address = createAddress()
```

*You can tell that the `createAddress()` function isn’t called, because nothing is printed.*

`createAddress()` 함수가 호출되지 않은 것은 아무것도 출력되지 않았기 때문임을 알 수 있습니다.
