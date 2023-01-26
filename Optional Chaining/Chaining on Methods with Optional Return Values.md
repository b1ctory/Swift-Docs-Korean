## *Chaining on Methods with Optional Return Values: 옵셔널 리턴 값이 있는 메서드에 체인을 연결*

*The previous example shows how to retrieve the value of a property of optional type through optional chaining. You can also use optional chaining to call a method that returns a value of optional type, and to chain on that method’s return value if needed.*

이전 예에서는 옵셔널 체이닝을 통해 옵셔널 타입의 프로퍼티 값을 검색하는 방법을 보여 줍니다. 또한 옵셔널 체이닝을 사용하여 옵셔널 타입의 값을 반환하는 메서드를 호출하고 필요한 경우 해당 메서드의 반환 값을 체인으로 연결할 수 있습니다.

*The example below calls the `Address` class’s `buildingIdentifier()` method through optional chaining. This method returns a value of type `String?`. As described above, the ultimate return type of this method call after optional chaining is also `String?`:*

아래 예제는 옵셔널 체이닝을 통해 `Address` 클래스의 `buildingIdentifier()` 메서드를 호출합니다. 이 메서드는 `String?` 타입의 값을 반환합니다. 위에서 설명한 바와 같이 옵셔널 체이닝 후 이 메서드 호출의 최종 반환 타입 역시 `String?` 입니다:

```swift
if let buildingIdentifier = john.residence?.address?.buildingIdentifier() {
    print("John's building identifier is \(buildingIdentifier).")
}
// Prints "John's building identifier is The Larches."
```

*If you want to perform further optional chaining on this method’s return value, place the optional chaining question mark after the method’s parentheses:*

이 메서드의 반환 값에 추가로 옵셔널 체이닝을 수행하려면 옵셔널 체이닝 물음표를 메서드의 괄호 뒤에 붙입니다:

```swift
if let beginsWithThe =
    john.residence?.address?.buildingIdentifier()?.hasPrefix("The") {
    if beginsWithThe {
        print("John's building identifier begins with \"The\".")
    } else {
        print("John's building identifier doesn't begin with \"The\".")
    }
}
// Prints "John's building identifier begins with "The"."
```

> *NOTE*
> 
> *In the example above, you place the optional chaining question mark after the parentheses, because the optional value you are chaining on is the `buildingIdentifier()` method’s return value, and not the `buildingIdentifier()` method itself.*
> 
> 위의 예에서는 괄호 뒤에 옵셔널 체이닝 물음표를 배치합니다. 이는 연결 중인 옵셔널 값이 `buildingIdentifier()` 메서드의 반환 값이지 `buildingIdentifier()` 메서드 자체가 아니기 때문에 옵셔널 리턴값이 있는 메서드에 체인을 연결합니다.


