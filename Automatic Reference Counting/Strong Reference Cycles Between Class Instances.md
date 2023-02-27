## *Strong Reference Cycles Between Class Instances : 클래스 인스턴스 간의 강력한 참조 순환*

*In the examples above, ARC is able to track the number of references to the new `Person` instance you create and to deallocate that `Person` instance when it’s no longer needed.*

위의 예에서 ARC는 생성한 새 `Person` 인스턴스에 대한 참조 수를 추적하고 더 이상 필요하지 않을 때 해당 `Person` 인스턴스를 할당 해제할 수 있습니다.

*However, it’s possible to write code in which an instance of a class never gets to a point where it has zero strong references. This can happen if two class instances hold a strong reference to each other, such that each instance keeps the other alive. This is known as a strong reference cycle.*

그러나 클래스의 인스턴스가 강력한 참조가 없는 지점에 도달하지 않는 코드를 작성할 수 있습니다. 이는 두 클래스 인스턴스가 서로에 대한 강력한 참조를 유지하여 각 인스턴스가 서로를 활성 상태로 유지하는 경우에 발생할 수 있습니다. 이를 강력한 참조 순환이라고 합니다.

*You resolve strong reference cycles by defining some of the relationships between classes as weak or unowned references instead of as strong references. This process is described in [Resolving Strong Reference Cycles Between Class Instances](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/automaticreferencecounting#Resolving-Strong-Reference-Cycles-Between-Class-Instances). However, before you learn how to resolve a strong reference cycle, it’s useful to understand how such a cycle is caused.*

클래스 간의 관계 중 일부를 강력한 참조가 아닌 약한 참조 또는 소유하지 않은 참조로 정의하여 강력한 참조 주기를 해결합니다. 이 프로세스는 [링크]에 설명되어 있습니다. 그러나 강력한 참조 주기를 해결하는 방법을 배우기 전에 이러한 주기가 어떻게 발생하는지 이해하는 것이 유용합니다.

*Here’s an example of how a strong reference cycle can be created by accident. This example defines two classes called `Person` and `Apartment`, which model a block of apartments and its residents:*

다음은 실수로 인해 강력한 기준 주기가 생성되는 방법에 대한 예입니다. 이 예에서는 아파트와 그 거주자의 블록을 모델링하는 `Person`과 `Apartment`라는 두 가지 클래스를 정의합니다:

```swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment?
    deinit { print("\(name) is being deinitialized") }
}

class Apartment {
    let unit: String
    init(unit: String) { self.unit = unit }
    var tenant: Person?
    deinit { print("Apartment \(unit) is being deinitialized") }
}
```

*Every `Person` instance has a `name` property of type `String` and an optional `apartment` property that’s initially `nil`. The `apartment` property is optional, because a person may not always have an apartment.*

모든 `Person` 인스턴스에는 `String` 유형의 `name` 프로퍼티와 처음에 `nil`인 옵셔널 `apartment` 프로퍼티가 있습니다. `apartment` 프로퍼티는 옵셔널입니다. 사람이 항상 아파트를 가지고 있지는 않을 수 있기 때문입니다.

*Similarly, every `Apartment` instance has a `unit` property of type `String` and has an optional `tenant` property that’s initially `nil`. The tenant property is optional because an apartment may not always have a tenant.*

마찬가지로 모든 `Apartment` 인스턴스에는 `String` 타입의 `unit` 프로퍼티가 있고 처음에는 `nil`인 옵셔널 `tenant` 프로퍼티가 있습니다. 아파트에 항상 세입자가 있는 것은 아니므로 임차인 프로퍼티는 선택 사항입니다.

*Both of these classes also define a deinitializer, which prints the fact that an instance of that class is being deinitialized. This enables you to see whether instances of `Person` and `Apartment` are being deallocated as expected.*

이 두 클래스는 모두 해당 클래스의 인스턴스가 초기화 해제되고 있다는 사실을 인쇄하는 초기화 해제자를 정의합니다. 이를 통해 `Person` 및 `Apartment` 인스턴스가 예상대로 할당 해제되고 있는지 확인할 수 있습니다.

*This next code snippet defines two variables of optional type called `john` and `unit4A`, which will be set to a specific `Apartment` and `Person` instance below. Both of these variables have an initial value of `nil`, by virtue of being optional:*

이 다음 코드 조각은 `john` 및 `unit4A`라는 옵셔널 타입의 두 변수를 정의하며, 이는 아래의 특정 `Apartment` 및 `Person` 인스턴스로 설정됩니다. 이 두 변수는 모두 옵셔널이므로 초기값이 `nil`입니다.

```swift
var john: Person?
var unit4A: Apartment?
```

*You can now create a specific `Person` instance and `Apartment` instance and assign these new instances to the `john` and `unit4A` variables:*

이제 특정 `Person` 인스턴스 및 `Apartment` 인스턴스를 만들고 이러한 새 인스턴스를 `john` 및 `unit4A` 변수에 할당할 수 있습니다.

```swift
john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")
```

*Here’s how the strong references look after creating and assigning these two instances. The `john` variable now has a strong reference to the new `Person` instance, and the `unit4A` variable has a strong reference to the new `Apartment` instance:*

다음은 이 두 인스턴스를 생성하고 할당한 후 강력한 참조가 어떻게 보이는지 보여줍니다. 이제 `john` 변수에는 새로운 `Person` 인스턴스에 대한 강력한 참조가 있고 `unit4A` 변수에는 새로운 `Apartment` 인스턴스에 대한 강력한 참조가 있습니다.

*![](https://docs.swift.org/swift-book/images/referenceCycle01@2x.png)*

*You can now link the two instances together so that the person has an apartment, and the apartment has a tenant. Note that an exclamation point (`!`) is used to unwrap and access the instances stored inside the `john` and `unit4A` optional variables, so that the properties of those instances can be set:*

이제 두 인스턴스를 함께 연결하여 개인이 아파트를 갖고 아파트가 임차인을 가질 수 있습니다. 느낌표(`!`)는 `john` 및 `unit4A` 옵셔널 변수에 저장된 인스턴스의 래핑을 풀고 액세스하는 데 사용되므로 해당 인스턴스의 프로퍼티를 설정할 수 있습니다.

```swift
john!.apartment = unit4A
unit4A!.tenant = john
```

*Here’s how the strong references look after you link the two instances together:*

다음은 두 인스턴스를 함께 연결한 후의 강력한 참조 모양입니다.

*![](https://docs.swift.org/swift-book/images/referenceCycle02@2x.png)*

*Unfortunately, linking these two instances creates a strong reference cycle between them. The `Person` instance now has a strong reference to the `Apartment` instance, and the `Apartment` instance has a strong reference to the `Person` instance. Therefore, when you break the strong references held by the `john` and `unit4A` variables, the reference counts don’t drop to zero, and the instances aren’t deallocated by ARC:*

안타깝게도 이 두 인스턴스를 연결하면 두 인스턴스 간에 강력한 참조 순환이 생성됩니다. 이제 `Person` 인스턴스는 `Apartment` 인스턴스에 대한 강력한 참조를 가지며 `Apartment` 인스턴스는 `Person` 인스턴스에 대한 강력한 참조를 갖습니다. 따라서 `john` 및 `unit4A` 변수가 보유한 강한 참조를 끊을 때 참조 횟수가 0으로 떨어지지 않고 인스턴스가 ARC에 의해 할당 해제되지 않습니다.

```swift
john = nil
unit4A = nil
```

*Note that neither deinitializer was called when you set these two variables to `nil`. The strong reference cycle prevents the `Person` and `Apartment` instances from ever being deallocated, causing a memory leak in your app.*

이 두 변수를 `nil`로 설정하면 초기화 해제자가 호출되지 않습니다. 강력한 참조 순환은 `Person` 및 `Apartment` 인스턴스가 할당 해제되어 앱에서 메모리 누수가 발생하는 것을 방지합니다.

*Here’s how the strong references look after you set the `john` and `unit4A` variables to `nil`:*

`john` 및 `unit4A` 변수를 `nil`로 설정한 후의 강력한 참조는 다음과 같습니다.

*![](https://docs.swift.org/swift-book/images/referenceCycle03@2x.png)*

*The strong references between the `Person` instance and the `Apartment` instance remain and can’t be broken.*

`Person` 인스턴스와 `Apartment` 인스턴스 사이의 강력한 참조는 유지되며 깨질 수 없습니다.
