### *Unowned References : 미소유 참조*

*Like a weak reference, an unowned reference doesn’t keep a strong hold on the instance it refers to. Unlike a weak reference, however, an unowned reference is used when the other instance has the same lifetime or a longer lifetime. You indicate an unowned reference by placing the `unowned` keyword before a property or variable declaration.*

약한 참조와 마찬가지로 미소유 참조는 참조하는 인스턴스를 강력하게 유지하지 않습니다. 그러나 약한 참조와 달리 미소유 참조는 다른 인스턴스의 수명이 같거나 더 긴 경우에 사용됩니다. 프로퍼티 또는 변수 선언 앞에 `unowned` 키워드를 배치하여 미소유 참조를 나타냅니다.

*Unlike a weak reference, an unowned reference is expected to always have a value. As a result, marking a value as unowned doesn’t make it optional, and ARC never sets an unowned reference’s value to `nil`.*

약한 참조와 달리 미소유 참조는 항상 값을 가질 것으로 기대됩니다. 따라서 값을 소유되지 않음으로 표시해도 옵셔널이 아니며 ARC는 미소유 참조의 값을 `nil`로 설정하지 않습니다.

> ***Important***
> 
> *Use an unowned reference only when you are sure that the reference always refers to an instance that hasn’t been deallocated.*
> 
> 참조가 항상 할당 해제되지 않은 인스턴스를 참조한다고 확신하는 경우에만 미소유 참조를 사용하세요.
> 
> *If you try to access the value of an unowned reference after that instance has been deallocated, you’ll get a runtime error.*
> 
> 해당 인스턴스가 할당 해제된 후 소유되지 않은 참조 값에 액세스하려고 하면 런타임 오류가 발생합니다.

*The following example defines two classes, `Customer` and `CreditCard`, which model a bank customer and a possible credit card for that customer. These two classes each store an instance of the other class as a property. This relationship has the potential to create a strong reference cycle.*

다음 예는 은행 고객과 해당 고객의 가능한 신용 카드를 모델링하는 `Customer` 및 `CreditCard`라는 두 가지 클래스를 정의합니다. 이 두 클래스는 각각 다른 클래스의 인스턴스를 프로퍼티로 저장합니다. 이 관계는 강력한 순환 참조를 만들 가능성이 있습니다.

*The relationship between `Customer` and `CreditCard` is slightly different from the relationship between `Apartment` and `Person` seen in the weak reference example above. In this data model, a customer may or may not have a credit card, but a credit card will always be associated with a customer. A `CreditCard` instance never outlives the `Customer` that it refers to. To represent this, the `Customer` class has an optional `card` property, but the `CreditCard` class has an unowned (and non-optional) `customer` property.*

`Customer`와 `CreditCard`의 관계는 위의 약한 참조 예에서 볼 수 있는 `Apartment`와 `Person`의 관계와 약간 다릅니다. 이 데이터 모델에서 고객은 신용카드가 있을 수도 있고 없을 수도 있지만 신용카드는 항상 고객과 연결됩니다. `CreditCard` 인스턴스는 참조하는 `Customer`보다 오래 지속되지 않습니다. 이를 나타내기 위해 `Customer` 클래스에는 옵셔널 `card` 속성이 있지만 `CreditCard` 클래스에는 소유되지 않은(옵셔널이 아닌) `customer` 프로퍼티가 있습니다.

*Furthermore, a new `CreditCard` instance can only be created by passing a `number` value and a `customer` instance to a custom `CreditCard` initializer. This ensures that a `CreditCard` instance always has a `customer` instance associated with it when the `CreditCard` instance is created.*

또한 새 `CreditCard` 인스턴스는 `number` 값과 `customer` 인스턴스를 커스텀 `CreditCard` 이니셜라이저에 전달해야만 생성할 수 있습니다. 이렇게 하면 `CreditCard` 인스턴스가 생성될 때 `CreditCard` 인스턴스에 항상 연결된 `customer` 인스턴스가 있게 됩니다.

*Because a credit card will always have a customer, you define its `customer` property as an unowned reference, to avoid a strong reference cycle:*

신용 카드에는 항상 고객이 있기 때문에 강력한 순환 참조를 피하기 위해 `customer` 프로퍼티를 소유되지 않은 참조로 정의합니다.

```swift
class Customer {
    let name: String
    var card: CreditCard?
    init(name: String) {
        self.name = name
    }
    deinit { print("\(name) is being deinitialized") }
}

class CreditCard {
    let number: UInt64
    unowned let customer: Customer
    init(number: UInt64, customer: Customer) {
        self.number = number
        self.customer = customer
    }
    deinit { print("Card #\(number) is being deinitialized") }
}
```

> *Note*
> 
> *The `number` property of the `CreditCard` class is defined with a type of `UInt64` rather than `Int`, to ensure that the `number` property’s capacity is large enough to store a 16-digit card number on both 32-bit and 64-bit systems.*
> 
> `CreditCard` 클래스의 `number` 프로퍼티는 `Int`가 아닌 `UInt64` 타입으로 정의되어 32비트 및 64비트 시스템 모두에서 `number` 프로퍼티의 용량이 16자리 카드 번호를 저장할 수 있을 만큼 충분히 커집니다. 

*This next code snippet defines an optional `Customer` variable called `john`, which will be used to store a reference to a specific customer. This variable has an initial value of nil, by virtue of being optional:*

이 다음 코드 스니펫은 특정 고객에 대한 참조를 저장하는 데 사용되는 `john`이라는 옵셔널 `Customer` 변수를 정의합니다. 이 변수는 옵셔널이기 때문에 초기 값이 `nil`입니다.

```swift
var john: Customer?
```

*You can now create a `Customer` instance, and use it to initialize and assign a new `CreditCard` instance as that customer’s `card` property:*

이제 `Customer` 인스턴스를 만들고 이를 사용하여 새 `CreditCard` 인스턴스를 해당 고객의 `card` 프로퍼티로 초기화하고 할당할 수 있습니다.

```swift
john = Customer(name: "John Appleseed")
john!.card = CreditCard(number: 1234_5678_9012_3456, customer: john!)
```

*Here’s how the references look, now that you’ve linked the two instances:*

이제 두 인스턴스를 연결했으므로 참조가 표시되는 방식은 다음과 같습니다.

*![](https://docs.swift.org/swift-book/images/unownedReference01@2x.png)*

*The `Customer` instance now has a strong reference to the `CreditCard` instance, and the `CreditCard` instance has an unowned reference to the `Customer` instance.*

이제 `Customer` 인스턴스에는 `CreditCard` 인스턴스에 대한 강력한 참조가 있고 `CreditCard` 인스턴스에는 `Customer` 인스턴스에 대한 소유되지 않은 참조가 있습니다.

*Because of the unowned `customer` reference, when you break the strong reference held by the `john` variable, there are no more strong references to the `Customer` instance:*

소유되지 않은 `customer` 참조 때문에 `john` 변수가 보유한 강한 참조를 끊으면 `Customer` 인스턴스에 대한 강한 참조가 더 이상 없습니다.

*![](https://docs.swift.org/swift-book/images/unownedReference02@2x.png)*

*Because there are no more strong references to the `Customer` instance, it’s deallocated. After this happens, there are no more strong references to the `CreditCard` instance, and it too is deallocated:*

`Customer` 인스턴스에 대한 강력한 참조가 더 이상 없기 때문에 할당이 취소됩니다. 이후에는 `CreditCard` 인스턴스에 대한 강력한 참조가 더 이상 없으며 역시 할당이 해제됩니다.

```swift
john = nil
// Prints "John Appleseed is being deinitialized"
// Prints "Card #1234567890123456 is being deinitialized"
```

*The final code snippet above shows that the deinitializers for the `Customer` instance and `CreditCard` instance both print their “deinitialized” messages after the `john` variable is set to `nil`.*

위의 마지막 코드 스니펫은 `Customer` 인스턴스 및 `CreditCard` 인스턴스의 초기화 해제자가 모두 `john` 변수가 `nil`로 설정된 후 "초기화 해제" 메시지를 출력함을 보여줍니다.

> *Note*
> 
> *The examples above show how to use safe unowned references. Swift also provides unsafe unowned references for cases where you need to disable runtime safety checks — for example, for performance reasons. As with all unsafe operations, you take on the responsibility for checking that code for safety.*
> 
> 위의 예는 안전한 미소유 참조를 사용하는 방법을 보여줍니다. 또한 Swift는 성능상의 이유로 런타임 안전 확인을 비활성화해야 하는 경우 안전하지 않은 미소유 참조를 제공합니다. 안전하지 않은 모든 작업과 마찬가지로 안전을 위해 해당 코드를 확인할 책임이 있습니다.
> 
> *You indicate an unsafe unowned reference by writing `unowned(unsafe)`. If you try to access an unsafe unowned reference after the instance that it refers to is deallocated, your program will try to access the memory location where the instance used to be, which is an unsafe operation.*
> 
> `unowned(unsafe)`를 작성하여 안전하지 않은 미소유 참조를 나타냅니다. 참조하는 인스턴스가 할당 해제된 후 안전하지 않은 미소유 참조에 액세스하려고 하면 프로그램은 인스턴스가 있던 메모리 위치에 액세스하려고 시도하며 이는 안전하지 않은 작업입니다.


