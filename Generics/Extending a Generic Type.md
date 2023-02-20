## *Extending a Generic Type*

*When you extend a generic type, you don’t provide a type parameter list as part of the extension’s definition. Instead, the type parameter list from the original type definition is available within the body of the extension, and the original type parameter names are used to refer to the type parameters from the original definition.*

*The following example extends the generic `Stack` type to add a read-only computed property called `topItem`, which returns the top item on the stack without popping it from the stack:*

```swift
extension Stack {
    var topItem: Element? {
        return items.isEmpty ? nil : items[items.count - 1]
    }
}
```

*The `topItem` computed property can now be used with any `Stack` instance to access and query its top item without removing it.*

```swift
if let topItem = stackOfStrings.topItem {
    print("The top item on the stack is \(topItem).")
}
// Prints "The top item on the stack is tres."Extensions of a generic type can also include requirements that instances of the extended type must satisfy in order to gain the new functionality, as discussed in [Extensions with a Generic Where Clause](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Extensions-with-a-Generic-Where-Clause) below.
```

*Extensions of a generic type can also include requirements that instances of the extended type must satisfy in order to gain the new functionality, as discussed in [Extensions with a Generic Where Clause](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Extensions-with-a-Generic-Where-Clause) below.*


