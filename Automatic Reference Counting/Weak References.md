### *Weak References : 약한 참조*

*A weak reference is a reference that doesn’t keep a strong hold on the instance it refers to, and so doesn’t stop ARC from disposing of the referenced instance. This behavior prevents the reference from becoming part of a strong reference cycle. You indicate a weak reference by placing the `weak` keyword before a property or variable declaration.*

약한 참조는 참조하는 인스턴스를 강하게 유지하지 않으므로 ARC가 참조하는 인스턴스를 처리하는 것을 중지하지 않는 참조입니다. 이 동작은 참조가 강력한 참조 주기의 일부가 되는 것을 방지합니다. 프로퍼티 또는 변수 선언 앞에 `weak` 키워드를 배치하여 약한 참조를 나타냅니다.

*Because a weak reference doesn’t keep a strong hold on the instance it refers to, it’s possible for that instance to be deallocated while the weak reference is still referring to it. Therefore, ARC automatically sets a weak reference to `nil` when the instance that it refers to is deallocated. And, because weak references need to allow their value to be changed to `nil` at runtime, they’re always declared as variables, rather than constants, of an optional type.*

약한 참조는 참조하는 인스턴스를 강력하게 유지하지 못하기 때문에 약한 참조가 참조하는 동안 해당 인스턴스가 할당 해제될 수 있습니다. 따라서 ARC는 참조하는 인스턴스가 할당 해제될 때 자동으로 약한 참조를 `nil`로 설정합니다. 또한 약한 참조는 런타임시에 값을 `nil`로 변경할 수 있어야 하므로 항상 옵셔널 타입의 상수가 아닌 변수로 선언됩니다.

*You can check for the existence of a value in the weak reference, just like any other optional value, and you will never end up with a reference to an invalid instance that no longer exists.*

다른 옵셔널 값과 마찬가지로 약한 참조에 값이 있는지 확인할 수 있으며, 더 이상 존재하지 않는 잘못된 인스턴스에 대한 참조로 끝나지 않을 것입니다.

> *Note*
> 
> *Property observers aren’t called when ARC sets a weak reference to `nil`.*
> 
> ARC가 `nil`에 대한 약한 참조를 설정할 때 프로퍼티 옵저버가 호출되지 않습니다.

*The example below is identical to the `Person` and `Apartment` example from above, with one important difference. This time around, the `Apartment` type’s `tenant` property is declared as a weak reference:*

아래의 예는 위의 `Person`과 `Apartment`의 예와 동일하며 한 가지 중요한 차이점이 있습니다. 이번에는 `Apartment` 타입의 `tenant` 프로퍼티가 약한 참조로 선언됩니다:

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
    weak var tenant: Person?
    deinit { print("Apartment \(unit) is being deinitialized") }
}
```

*The strong references from the two variables (`john` and `unit4A`) and the links between the two instances are created as before:*

두 변수(`john` 및 `unit4A`)의 강력한 참조와 두 인스턴스 간의 링크는 이전과 같이 생성됩니다.

```swift
var john: Person?
var unit4A: Apartment?

john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")

john!.apartment = unit4A
unit4A!.tenant = john
```

*Here’s how the references look now that you’ve linked the two instances together:*

두 인스턴스를 함께 연결한 참조는 다음과 같습니다.

*![](https://docs.swift.org/swift-book/images/weakReference01@2x.png)*

*The `Person` instance still has a strong reference to the `Apartment` instance, but the `Apartment` instance now has a weak reference to the `Person` instance. This means that when you break the strong reference held by the `john` variable by setting it to `nil`, there are no more strong references to the `Person` instance:*

`Person` 인스턴스는 여전히 `Apartment` 인스턴스에 대한 강력한 참조를 갖지만 이제 `Apartment` 인스턴스는 `Person` 인스턴스에 대한 약한 참조를 갖습니다. 즉, `john` 변수를 `nil`로 설정하여 `john` 변수가 보유한 강한 참조를 깨면 더 이상 `Person` 인스턴스에 대한 강한 참조가 없습니다.

```swift
john = nil// Prints "John Appleseed is being deinitialized"
```

*Because there are no more strong references to the `Person` instance, it’s deallocated and the `tenant` property is set to `nil`:*

`Person` 인스턴스에 대한 강력한 참조가 더 이상 없기 때문에 할당이 취소되고 `tenant` 속성이 `nil`로 설정됩니다.

*<img src="https://docs.swift.org/swift-book/images/weakReference02@2x.png" title="" alt="" data-align="center">*

*The only remaining strong reference to the `Apartment` instance is from the `unit4A` variable. If you break that strong reference, there are no more strong references to the `Apartment` instance:*

`Apartment` 인스턴스에 대한 유일한 강력한 참조는 `unit4A` 변수에서 온 것입니다. 이 강한 참조를 깨면 `Apartment` 인스턴스에 대한 강한 참조가 더 이상 없습니다.

```swift
unit4A = nil// Prints "Apartment 4A is being deinitialized"
```

*Because there are no more strong references to the `Apartment` instance, it too is deallocated:*

`Apartment` 인스턴스에 대한 강력한 참조가 더 이상 없기 때문에 이것도 할당 해제됩니다.

*![](https://docs.swift.org/swift-book/images/weakReference03@2x.png)*

> *Note*
> 
> *In systems that use garbage collection, weak pointers are sometimes used to implement a simple caching mechanism because objects with no strong references are deallocated only when memory pressure triggers garbage collection. However, with ARC, values are deallocated as soon as their last strong reference is removed, making weak references unsuitable for such a purpose.*
> 
> 가비지 컬렉션을 사용하는 시스템에서 강력한 참조가 없는 개체는 메모리 압력이 가비지 컬렉션을 트리거할 때만 할당이 해제되기 때문에 간단한 캐싱 메커니즘을 구현하는 데 약한 포인터가 사용되는 경우가 있습니다. 그러나 ARC를 사용하면 마지막 강한 참조가 제거되자마자 값이 할당 해제되므로 약한 참조는 이러한 목적에 적합하지 않습니다.


