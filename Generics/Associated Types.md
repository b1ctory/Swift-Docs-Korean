## *Associated Types : 관련 타입*

*When defining a protocol, it’s sometimes useful to declare one or more associated types as part of the protocol’s definition. An associated type gives a placeholder name to a type that’s used as part of the protocol. The actual type to use for that associated type isn’t specified until the protocol is adopted. Associated types are specified with the `associatedtype` keyword.*

프로토콜을 정의할 때 프로토콜 정의의 일부로 하나 이상의 연관된 유형을 선언하는 것이 유용할 수 있습니다. 관련 타입은 프로토콜의 일부로 사용되는 타입에 플레이스 홀더 이름을 제공합니다. 프로토콜이 적용될 때까지 관련된 타입에 사용할 실제 타입이 지정되지 않습니다. 연관 타입은 `associatedtype` 키워드로 지정됩니다.

### *Associated Types in Action : 액션에서의 연관 타입*

*Here’s an example of a protocol called `Container`, which declares an associated type called `Item`:*

다음은 `Item`이라는 관련 타입을 선언하는 `Container`라는 프로토콜의 예입니다:

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

*The `Container` protocol defines three required capabilities that any container must provide:*

`Container` 프로토콜은 컨테이너가 제공해야 하는 세 가지 필수 기능을 정의합니다:

- *It must be possible to add a new item to the container with an `append(_:)` method.*
  
  `append(_:)` 메서드로 컨테이너에 새 항목을 추가할 수 있어야 합니다.

- *It must be possible to access a count of the items in the container through a `count` property that returns an `Int` value.*
  
  `Int` 값을 반환하는 `count` 프로퍼티를 통해 컨테이너의 항목 수에 액세스할 수 있어야 합니다.

- *It must be possible to retrieve each item in the container with a subscript that takes an `Int` index value.*
  
  `Int` 인덱스 값을 사용하는 서브스크립트를 사용하여 컨테이너의 각 항목을 검색할 수 있어야 합니다.

*This protocol doesn’t specify how the items in the container should be stored or what type they’re allowed to be. The protocol only specifies the three bits of functionality that any type must provide in order to be considered a `Container`. A conforming type can provide additional functionality, as long as it satisfies these three requirements.*

이 프로토콜은 컨테이너에 있는 항목을 저장하는 방법이나 항목 타입을 지정하지 않습니다. 이 프로토콜은 `Container`로 간주되기 위해 모든 타입이 제공해야 하는 기능의 3비트만 지정합니다. 적합 타입은 이러한 세 가지 요구 사항을 충족하는 한 추가 기능을 제공할 수 있습니다.

*Any type that conforms to the `Container` protocol must be able to specify the type of values it stores. Specifically, it must ensure that only items of the right type are added to the container, and it must be clear about the type of the items returned by its subscript.*

컨테이너 프로토콜을 준수하는 모든 타입은 저장하는 값의 타입을 지정할 수 있어야 합니다. 특히 올바른 유형의 항목만 컨테이너에 추가해야 하며, 구독자가 반환하는 항목의 타입에 대해 명확해야 합니다.

*To define these requirements, the `Container` protocol needs a way to refer to the type of the elements that a container will hold, without knowing what that type is for a specific container. The `Container` protocol needs to specify that any value passed to the `append(_:)` method must have the same type as the container’s element type, and that the value returned by the container’s subscript will be of the same type as the container’s element type.*

이러한 요구사항을 정의하기 위해 `Container` 프로토콜은 특정 컨테이너에 대한 타입이 무엇인지 알지 못한 채 컨테이너가 보유할 요소의 타입을 참조하는 방법이 필요합니다. `Container` 프로토콜은 `append(_:)` 메서드에 전달된 값이 컨테이너의 요소 타입과 동일한 타입이어야 하며 컨테이너의 서브스크립트에 의해 반환된 값이 컨테이너의 요소 타입과 동일한 타입이어야 함을 지정해야 합니다.

*To achieve this, the `Container` protocol declares an associated type called `Item`, written as `associatedtype Item`. The protocol doesn’t define what `Item` is — that information is left for any conforming type to provide. Nonetheless, the `Item` alias provides a way to refer to the type of the items in a `Container`, and to define a type for use with the `append(_:)` method and subscript, to ensure that the expected behavior of any `Container` is enforced.*

이를 달성하기 위해 `Container` 프로토콜은 `associatedtype Item`으로 작성된 `Item`이라는 연결 타입을 선언합니다. 프로토콜은 `Item`이 무엇인지 정의하지 않습니다- 이 정보는 제공할 적합한 타입을 위해 남겨집니다. 그럼에도 불구하고 `Item` 별칭은 `Container`의 항목 타입을 참조하고 `append(_:)` 메서드 및 서브스크립트와 함께 사용할 타입을 정의하여 `Container`의 예상 동작이 적용되도록 합니다.

*Here’s a version of the nongeneric `IntStack` type from [Generic Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Generic-Types) above, adapted to conform to the `Container` protocol:*

위의 [링크]의 비제너럴 `IntStack` 타입 버전은 `Container` 프로토콜에 맞게 조정되었습니다:

```swift
struct IntStack: Container {
    // original IntStack implementation
    var items: [Int] = []
    mutating func push(_ item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
    // conformance to the Container protocol
    typealias Item = Int
    mutating func append(_ item: Int) {
        self.push(item)
    }
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Int {
        return items[i]
    }
}
```

*The `IntStack` type implements all three of the `Container` protocol’s requirements, and in each case wraps part of the `IntStack` type’s existing functionality to satisfy these requirements.*

`IntStack` 타입은 `Container` 프로토콜의 세 가지 요구 사항을 모두 구현하며, 각각의 경우 이러한 요구 사항을 충족하기 위해 `IntStack` 타입의 기존 기능의 일부를 포장합니다.

*Moreover, `IntStack` specifies that for this implementation of `Container`, the appropriate `Item` to use is a type of `Int`. The definition of `typealias Item = Int` turns the abstract type of `Item` into a concrete type of `Int` for this implementation of the `Container` protocol.*

또한, `IntStack`은 `Container`의 이러한 구현을 위해 사용할 적절한 `Item`이 `Int` 타입임을 지정합니다. `type alias Item = Int`의 정의는 `Container` 프로토콜의 이러한 구현을 위해 `Item`의 추상적인 타입을 `Int`의 구체적인 타입으로 바꿉니다.

*Thanks to Swift’s type inference, you don’t actually need to declare a concrete `Item` of `Int` as part of the definition of `IntStack`. Because `IntStack` conforms to all of the requirements of the `Container` protocol, Swift can infer the appropriate `Item` to use, simply by looking at the type of the `append(_:)` method’s `item` parameter and the return type of the subscript. Indeed, if you delete the `typealias Item = Int` line from the code above, everything still works, because it’s clear what type should be used for `Item`.*

Swift의 타입 추론 덕분에 실제로는 `IntStack`의 정의의 일부로 `Int`의 구체적인 `Item`을 선언할 필요가 없습니다. `IntStack`은 `Container` 프로토콜의 모든 요구 사항을 준수하기 때문에 Swift는 `append(_:)` 메서드의 `Item` 매개 변수 타입과 서브스크립트의 반환 타입만 보고 사용할 적절한 `Item`을 추론할 수 있습니다. 실제로 위의 코드에서 `type alias Item = Int` 줄을 삭제해도 `Item`에 어떤 타입을 사용해야 하는지 명확하기 때문에 모든 것이 작동합니다.

*You can also make the generic `Stack` type conform to the `Container` protocol:*

또한 일반적인 `Stack` 타입을 `Container` 프로토콜을 준수하도록 만들 수 있습니다:

```swift
struct Stack<Element>: Container {
    // original Stack<Element> implementation
    var items: [Element] = []
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
    // conformance to the Container protocol
    mutating func append(_ item: Element) {
        self.push(item)
    }
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Element {
        return items[i]
    }
}
```

*This time, the type parameter `Element` is used as the type of the `append(_:)` method’s `item` parameter and the return type of the subscript. Swift can therefore infer that `Element` is the appropriate type to use as the `Item` for this particular container.*

이번에는 타입 매개 변수 `Element`가 `append(_:)` 메서드의 `item` 매개 변수의 타입과 서브스크립트 반환 타입으로 사용됩니다. 따라서 Swift는 `Element`가 이 특정 컨테이너의 `Item`으로 사용하기에 적합한 타입이라고 추론할 수 있습니다.

### *Extending an Existing Type to Specify an Associated Type : 기존 타입 확장하여 연결된 타입 지정*

*You can extend an existing type to add conformance to a protocol, as described in [Adding Protocol Conformance with an Extension](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/protocols#Adding-Protocol-Conformance-with-an-Extension). This includes a protocol with an associated type.*

[링크] 에 설명된 대로 기존 유형을 확장하여 프로토콜에 적합성을 추가할 수 있습니다. 여기에는 연관된 타입이 있는 프로토콜이 포함됩니다.

*Swift’s `Array` type already provides an `append(_:)` method, a `count` property, and a subscript with an `Int` index to retrieve its elements. These three capabilities match the requirements of the `Container` protocol. This means that you can extend `Array` to conform to the `Container` protocol simply by declaring that `Array` adopts the protocol. You do this with an empty extension, as described in [Declaring Protocol Adoption with an Extension](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/protocols#Declaring-Protocol-Adoption-with-an-Extension):*

Swift의 `Array` 타입은 이미 `append(_:)` 메서드, `count` 프로퍼티 및 해당 요소를 검색하기 위한 `Int` 인덱스를 가진 서브스크립트를 제공합니다. 이 세 가지 기능은 `Container` 프로토콜의 요구 사항과 일치합니다. 즉, [링크]에 설명된 대로 `Array`가 프로토콜을 채택한다고 선언하는 것만으로 `Array`를 확장하여 `Container` 프로토콜을 준수할 수 있습니다. 

```swift
extension Array: Container {}
```

*Array’s existing `append(_:)` method and subscript enable Swift to infer the appropriate type to use for `Item`, just as for the generic `Stack` type above. After defining this extension, you can use any `Array` as a `Container`.*

Array의 기존 `append(_:)` 메서드 및 서브스크립트를 통해 Swift는 위의 일반적인 `Stack` 타입과 마찬가지로 `Item`에 사용할 적절한 타입을 추론할 수 있습니다. 이 확장을 정의한 후에는 임의의 `Array`를 `Container`로 사용할 수 있습니다.

### *Adding Constraints to an Associated Type : 연관 타입에 제약 조건을 추가*

*You can add type constraints to an associated type in a protocol to require that conforming types satisfy those constraints. For example, the following code defines a version of `Container` that requires the items in the container to be equatable.*

프로토콜의 연관 타입에 타입 제약 조건을 추가하여 적합한 타입이 이러한 제약 조건을 충족하도록 요구할 수 있습니다. 예를 들어, 다음 코드는 컨테이너의 항목이 동일해야 하는 `Container` 버전을 정의합니다.

```swift
protocol Container {
    associatedtype Item: Equatable
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

*To conform to this version of `Container`, the container’s `Item` type has to conform to the `Equatable` protocol.*

이 버전의 `Container`를 준수하려면 컨테이너의 `Item` 타입이 `Equatable` 프로토콜을 준수해야 합니다.

### *Using a Protocol in Its Associated Type’s Constraints : 관련 타입의 제약 조건에서 프로토콜을 사용*

*A protocol can appear as part of its own requirements. For example, here’s a protocol that refines the `Container` protocol, adding the requirement of a `suffix(_:)` method. The `suffix(_:)` method returns a given number of elements from the end of the container, storing them in an instance of the `Suffix` type.*

프로토콜은 자체 요구사항의 일부로 나타날 수 있습니다. 예를 들어, 여기 `Container` 프로토콜을 세분화하는 프로토콜이 있습니다. 여기에 `suffix(_:)`메서드의 요구 사항이 추가됩니다. `suffix(_:)` 메서드는 컨테이너 끝에서 지정된 수의 요소를 반환하여 `Suffix` 타입의 인스턴스에 저장합니다.

```swift
protocol SuffixableContainer: Container {
    associatedtype Suffix: SuffixableContainer where Suffix.Item == Item
    func suffix(_ size: Int) -> Suffix
}
```

*In this protocol, `Suffix` is an associated type, like the `Item` type in the `Container` example above. `Suffix` has two constraints: It must conform to the `SuffixableContainer` protocol (the protocol currently being defined), and its `Item` type must be the same as the container’s `Item` type. The constraint on `Item` is a generic `where` clause, which is discussed in [Associated Types with a Generic Where Clause](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Associated-Types-with-a-Generic-Where-Clause) below.*

이 프로토콜에서 `Suffix`는 위의 `Container` 예제의 `Item` 타입과 같이 연관 타입입니다. `Suffix`에는 두 가지 제약 조건이 있습니다: 이는 `SuffixableContainer` 프로토콜(현재 정의 중인 프로토콜)을 준수해야 하며, `Item` 타입은 컨테이너의 `Item` 타입과 동일해야 합니다. `Item`에 대한 제약 조건은 일반적인 `where` 절로, 아래의 [링크]에서 설명합니다.

*Here’s an extension of the `Stack` type from [Generic Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Generic-Types) above that adds conformance to the `SuffixableContainer` protocol:*

다음은 확장된 `Stack` 타입으로, `SuffixableContainer` 프로토콜을 준수합니다:

```swift
extension Stack: SuffixableContainer {
    func suffix(_ size: Int) -> Stack {
        var result = Stack()
        for index in (count-size)..<count {
            result.append(self[index])
        }
        return result
    }
    // Inferred that Suffix is Stack.
}
var stackOfInts = Stack<Int>()
stackOfInts.append(10)
stackOfInts.append(20)
stackOfInts.append(30)
let suffix = stackOfInts.suffix(2)
// suffix contains 20 and 30
```

*In the example above, the `Suffix` associated type for `Stack` is also `Stack`, so the suffix operation on `Stack` returns another `Stack`. Alternatively, a type that conforms to `SuffixableContainer` can have a `Suffix` type that’s different from itself — meaning the suffix operation can return a different type. For example, here’s an extension to the nongeneric `IntStack` type that adds `SuffixableContainer` conformance, using `Stack<Int>` as its suffix type instead of `IntStack`:*

위의 예에서 `Stack`에 대한 `Suffix` 연관 타입도 `Stack`이므로 `Stack`의 접미사 연산은 다른 `Stack`을 반환합니다. 또는 `SuffixableContainer`를 준수하는 타입은 자신과 다른 `Suffix` 타입을 가질 수 있습니다. 즉, 접미사 연산이 다른 타입을 반환할 수 있습니다. 예를 들어, 다음은 접미사로 `IntStack` 대신 `Stack<Int>`을 사용하여 `SuffixableContainer` 준수를 추가하는 비제너럴 `IntStack` 타입의 확장입니다.

```swift
extension IntStack: SuffixableContainer {
    func suffix(_ size: Int) -> Stack<Int> {
        var result = Stack<Int>()
        for index in (count-size)..<count {
            result.append(self[index])
        }
        return result
    }
    // Inferred that Suffix is Stack<Int>.
}
```
