## *Associated Types*

*When defining a protocol, it’s sometimes useful to declare one or more associated types as part of the protocol’s definition. An associated type gives a placeholder name to a type that’s used as part of the protocol. The actual type to use for that associated type isn’t specified until the protocol is adopted. Associated types are specified with the `associatedtype` keyword.*

### *Associated Types in Action*

*Here’s an example of a protocol called `Container`, which declares an associated type called `Item`:*

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

*The `Container` protocol defines three required capabilities that any container must provide:*

- *It must be possible to add a new item to the container with an `append(_:)` method.*

- *It must be possible to access a count of the items in the container through a `count` property that returns an `Int` value.*

- *It must be possible to retrieve each item in the container with a subscript that takes an `Int` index value.*

*This protocol doesn’t specify how the items in the container should be stored or what type they’re allowed to be. The protocol only specifies the three bits of functionality that any type must provide in order to be considered a `Container`. A conforming type can provide additional functionality, as long as it satisfies these three requirements.*

*Any type that conforms to the `Container` protocol must be able to specify the type of values it stores. Specifically, it must ensure that only items of the right type are added to the container, and it must be clear about the type of the items returned by its subscript.*

*To define these requirements, the `Container` protocol needs a way to refer to the type of the elements that a container will hold, without knowing what that type is for a specific container. The `Container` protocol needs to specify that any value passed to the `append(_:)` method must have the same type as the container’s element type, and that the value returned by the container’s subscript will be of the same type as the container’s element type.*

*To achieve this, the `Container` protocol declares an associated type called `Item`, written as `associatedtype Item`. The protocol doesn’t define what `Item` is — that information is left for any conforming type to provide. Nonetheless, the `Item` alias provides a way to refer to the type of the items in a `Container`, and to define a type for use with the `append(_:)` method and subscript, to ensure that the expected behavior of any `Container` is enforced.*

*Here’s a version of the nongeneric `IntStack` type from [Generic Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Generic-Types) above, adapted to conform to the `Container` protocol:*

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

*Moreover, `IntStack` specifies that for this implementation of `Container`, the appropriate `Item` to use is a type of `Int`. The definition of `typealias Item = Int` turns the abstract type of `Item` into a concrete type of `Int` for this implementation of the `Container` protocol.*

*Thanks to Swift’s type inference, you don’t actually need to declare a concrete `Item` of `Int` as part of the definition of `IntStack`. Because `IntStack` conforms to all of the requirements of the `Container` protocol, Swift can infer the appropriate `Item` to use, simply by looking at the type of the `append(_:)` method’s `item` parameter and the return type of the subscript. Indeed, if you delete the `typealias Item = Int` line from the code above, everything still works, because it’s clear what type should be used for `Item`.*

*You can also make the generic `Stack` type conform to the `Container` protocol:*

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

### *Extending an Existing Type to Specify an Associated Type*

*You can extend an existing type to add conformance to a protocol, as described in [Adding Protocol Conformance with an Extension](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/protocols#Adding-Protocol-Conformance-with-an-Extension). This includes a protocol with an associated type.*

*Swift’s `Array` type already provides an `append(_:)` method, a `count` property, and a subscript with an `Int` index to retrieve its elements. These three capabilities match the requirements of the `Container` protocol. This means that you can extend `Array` to conform to the `Container` protocol simply by declaring that `Array` adopts the protocol. You do this with an empty extension, as described in [Declaring Protocol Adoption with an Extension](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/protocols#Declaring-Protocol-Adoption-with-an-Extension):*

```swift
extension Array: Container {}
```

*Array’s existing `append(_:)` method and subscript enable Swift to infer the appropriate type to use for `Item`, just as for the generic `Stack` type above. After defining this extension, you can use any `Array` as a `Container`.*

### *Adding Constraints to an Associated Type*

*You can add type constraints to an associated type in a protocol to require that conforming types satisfy those constraints. For example, the following code defines a version of `Container` that requires the items in the container to be equatable.*

```swift
protocol Container {
    associatedtype Item: Equatable
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

*To conform to this version of `Container`, the container’s `Item` type has to conform to the `Equatable` protocol.*

### *Using a Protocol in Its Associated Type’s Constraints*

*A protocol can appear as part of its own requirements. For example, here’s a protocol that refines the `Container` protocol, adding the requirement of a `suffix(_:)` method. The `suffix(_:)` method returns a given number of elements from the end of the container, storing them in an instance of the `Suffix` type.*

```swift
protocol SuffixableContainer: Container {
    associatedtype Suffix: SuffixableContainer where Suffix.Item == Item
    func suffix(_ size: Int) -> Suffix
}
```

*In this protocol, `Suffix` is an associated type, like the `Item` type in the `Container` example above. `Suffix` has two constraints: It must conform to the `SuffixableContainer` protocol (the protocol currently being defined), and its `Item` type must be the same as the container’s `Item` type. The constraint on `Item` is a generic `where` clause, which is discussed in [Associated Types with a Generic Where Clause](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Associated-Types-with-a-Generic-Where-Clause) below.*

*Here’s an extension of the `Stack` type from [Generic Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Generic-Types) above that adds conformance to the `SuffixableContainer` protocol:*

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
