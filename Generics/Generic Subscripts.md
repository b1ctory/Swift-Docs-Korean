## *Generic Subscripts*

*Subscripts can be generic, and they can include generic `where` clauses. You write the placeholder type name inside angle brackets after `subscript`, and you write a generic `where` clause right before the opening curly brace of the subscript’s body. For example:*

```swift
extension Container {
    subscript<Indices: Sequence>(indices: Indices) -> [Item]
            where Indices.Iterator.Element == Int {
        var result: [Item] = []
        for index in indices {
            result.append(self[index])
        }
        return result
    }
}
```

*This extension to the `Container` protocol adds a subscript that takes a sequence of indices and returns an array containing the items at each given index. This generic subscript is constrained as follows:*

- *The generic parameter `Indices` in angle brackets has to be a type that conforms to the `Sequence` protocol from the standard library.*

- *The subscript takes a single parameter, `indices`, which is an instance of that `Indices` type.*

- *The generic `where` clause requires that the iterator for the sequence must traverse over elements of type `Int`. This ensures that the indices in the sequence are the same type as the indices used for a container.*

*Taken together, these constraints mean that the value passed for the `indices` parameter is a sequence of integers.*


