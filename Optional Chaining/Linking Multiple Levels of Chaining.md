## *Linking Multiple Levels of Chaining: 여러 레벨의 체인을 연결*

*You can link together multiple levels of optional chaining to drill down to properties, methods, and subscripts deeper within a model. However, multiple levels of optional chaining don’t add more levels of optionality to the returned value.*

여러 레벨의 옵셔널 체이닝을 연결하여 모델 내의 프로퍼티, 메서드 및 서브스크립트를 자세히 살펴볼 수 있습니다. 그러나 여러 레벨의 옵셔널 체이닝은 반환된 값에 더 많은 레벨의 옵셔널 체이닝을 추가하지 않습니다.

*To put it another way:*

다른말로 하면:

- *If the type you are trying to retrieve isn’t optional, it will become optional because of the optional chaining.*
  
  검색하려는 타입이 옵셔널이 아닌 경우 옵셔널 체이닝으로 인해 옵셔널이 됩니다.

- *If the type you are trying to retrieve is already optional, it will not become more optional because of the chaining.*
  
  검색하려는 타입이 이미 옵셔널인 경우, 체이닝으로 인해 더 옵셔널이 되지 않습니다.

*Therefore:*

그러므로:

- *If you try to retrieve an `Int` value through optional chaining, an `Int?` is always returned, no matter how many levels of chaining are used.*
  
  옵셔널 체이닝을 통해 `Int` 값을 검색하려고 하면 사용되는 체이닝 레벨에 관계없이 `Int?`가 항상 반환됩니다.

- *Similarly, if you try to retrieve an `Int?` value through optional chaining, an `Int?` is always returned, no matter how many levels of chaining are used.*
  
  비슷하게, 만약 당신이 옵셔널 체이닝을 통해 `Int?`를 검색하려고 한다면 체이닝의 레벨이 얼마나 많이 사용되었는지와 상관없이 `Int?`를 항상 리턴합니다.

*The example below tries to access the `street` property of the `address` property of the `residence` property of `john`. There are two levels of optional chaining in use here, to chain through the `residence` and `address` properties, both of which are of optional type:*

아래 예제는 `john`의 `residence` 프로퍼티의 `address` 프로퍼티의 `street` 프로퍼티에 액세스하려고 합니다. 여기서 사용되는 옵셔널 체이닝은 `residence`와 `address` 프로퍼티를 체인으로 연결하는 두 가지 레벨이 있으며, 둘 다 옵셔널 타입입니다:

```swift
if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}
// Prints "Unable to retrieve the address."
```

*The value of `john.residence` currently contains a valid `Residence` instance. However, the value of `john.residence.address` is currently `nil`. Because of this, the call to `john.residence?.address?.street` fails.*

`john.residence` 값에는 현재 유효한 `Residence` 인스턴스가 포함되어 있습니다. 그러나 `john.residence.address`의 값은 현재 `nil`입니다. 이것 때문에, `john.residence?.address?.street`의 호출이 실패합니다.

*Note that in the example above, you are trying to retrieve the value of the `street` property. The type of this property is `String?`. The return value of `john.residence?.address?.street` is therefore also `String?`, even though two levels of optional chaining are applied in addition to the underlying optional type of the property.*

위의 예에서는 `street` 프로퍼티의 값을 검색하려고 합니다. 이 프로퍼티의 타입은 `String?` 입니다. 따라서 프로퍼티의 기본 옵셔널 타입 외에 2레벨의 옵셔널 체이닝이 적용되더라도 `john.residence?.address?.street`의 반환값도 `String?` 입니다.

*If you set an actual `Address` instance as the value for `john.residence.address`, and set an actual value for the address’s `street` property, you can access the value of the `street` property through multilevel optional chaining:*

실제 `Address` 인스턴스를 `john.residence.address`의 값으로 설정하고 주소의 `street` 프로퍼티에 대한 실제 값을 설정하면 다음과 같은 다단계 옵셔널 체이닝을 통해 `street` 프로퍼티의 값에 액세스할 수 있습니다:

```swift
let johnsAddress = Address()
johnsAddress.buildingName = "The Larches"
johnsAddress.street = "Laurel Street"
john.residence?.address = johnsAddress

if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}
// Prints "John's street name is Laurel Street."
```

*In this example, the attempt to set the `address` property of `john.residence` will succeed, because the value of `john.residence` currently contains a valid `Residence` instance.*

이 예에서는 `john.residence` 값에 현재 유효한 `Residence` 인스턴스가 포함되어 있으므로 `john.residence`의 `address` 프로퍼티를 설정하려는 시도가 성공합니다.


