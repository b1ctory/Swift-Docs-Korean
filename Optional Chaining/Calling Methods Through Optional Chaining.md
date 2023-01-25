## *Calling Methods Through Optional Chaining : 옵셔널 체이닝을 통해 메서드 호출*

*You can use optional chaining to call a method on an optional value, and to check whether that method call is successful. You can do this even if that method doesn’t define a return value.*

옵셔널 체이닝을 사용하여 옵셔널 값으로 메서드를 호출하고 해당 메서드 호출이 성공했는지 확인할 수 있습니다. 이 메서드가 반환 값을 정의하지 않는 경우에도 이 작업을 수행할 수 있습니다.

*The `printNumberOfRooms()` method on the `Residence` class prints the current value of `numberOfRooms`. Here’s how the method looks:*

`Residence` 클래스의 `printNumberOfRooms()` 메서드는 `numberOfRooms`의 현재 값을 출력합니다. 메서드의 생김새는 다음과 같습니다:

```swift
func printNumberOfRooms() {
    print("The number of rooms is \(numberOfRooms)")
}
```

*This method doesn’t specify a return type. However, functions and methods with no return type have an implicit return type of `Void`, as described in [Functions Without Return Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID163). This means that they return a value of `()`, or an empty tuple.*

이 메서드는 반환 타입을 지정하지 않습니다. 그러나 반환 타입이 없는 함수와 메서드는 [링크]에서 설명한 것처럼 암시적 반환 타입이 `Void`입니다. 이것은 그들이 `()`또는 빈 튜플의 값을 반환한다는 것을 의미합니다.

*If you call this method on an optional value with optional chaining, the method’s return type will be `Void?`, not `Void`, because return values are always of an optional type when called through optional chaining. This enables you to use an `if` statement to check whether it was possible to call the `printNumberOfRooms()` method, even though the method doesn’t itself define a return value. Compare the return value from the `printNumberOfRooms` call against `nil` to see if the method call was successful:*

옵셔널 체이닝이 있는 옵셔널 값에 대해 이 메서드를 호출하면 반환 값이 항상 옵셔널 체이닝을 통해 호출될 때 옵셔널 타입이기 때문에 메서드의 반환 타입은 `Void`가 아니라 `Void?`가 됩니다. 이렇게 하면 메서드 자체가 반환 값을 정의하지 않더라도 `if` 문을 사용하여 `printNumberOfRooms()` 메서드를 호출할 수 있는지 여부를 확인할 수 있습니다. `printNumberOfRooms` 호출의 반환 값을 `nil`과 비교하여 메서드 호출이 성공했는지 확인합니다:

```swift
if john.residence?.printNumberOfRooms() != nil {
    print("It was possible to print the number of rooms.")
} else {
    print("It was not possible to print the number of rooms.")
}
// Prints "It was not possible to print the number of rooms."
```

*The same is true if you attempt to set a property through optional chaining. The example above in [Accessing Properties Through Optional Chaining](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html#ID248) attempts to set an `address` value for `john.residence`, even though the `residence` property is `nil`. Any attempt to set a property through optional chaining returns a value of type `Void?`, which enables you to compare against `nil` to see if the property was set successfully:*

옵션 체인을 통해 프로퍼티를 설정하려는 경우에도 마찬가지입니다. 위의 [링크]의 예는 `john.residence`에 대한 `address` 값을 설정하려고 시도합니다. `john.residence` 프로퍼티가 `address`임에도 불구하고. 옵셔널 체이닝을 통해 프로퍼티를 설정하려고 하면 프로퍼티가 성공적으로 설정되었는지 확인할 수있는 `Void` 타입의 값이 반환됩니다.

```swift
if (john.residence?.address = someAddress) != nil {
    print("It was possible to set the address.")
} else {
    print("It was not possible to set the address.")
}
// Prints "It was not possible to set the address."
```
