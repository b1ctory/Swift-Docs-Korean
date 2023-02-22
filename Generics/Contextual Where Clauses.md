## *Contextual Where Clauses*

*You can write a generic `where` clause as part of a declaration that doesn’t have its own generic type constraints, when you’re already working in the context of generic types. For example, you can write a generic `where` clause on a subscript of a generic type or on a method in an extension to a generic type. The `Container` structure is generic, and the `where` clauses in the example below specify what type constraints have to be satisfied to make these new methods available on a container.*

```swift
extension Container {
    func average() -> Double where Item == Int {
        var sum = 0.0
        for index in 0..<count {
            sum += Double(self[index])
        }
        return sum / Double(count)
    }
    func endsWith(_ item: Item) -> Bool where Item: Equatable {
        return count >= 1 && self[count-1] == item
    }
}
let numbers = [1260, 1200, 98, 37]
print(numbers.average())
// Prints "648.75"
print(numbers.endsWith(37))
// Prints "true"
```

*This example adds an `average()` method to `Container` when the items are integers, and it adds an `endsWith(_:)` method when the items are equatable. Both functions include a generic `where` clause that adds type constraints to the generic `Item` type parameter from the original declaration of `Container`.*

*If you want to write this code without using contextual `where` clauses, you write two extensions, one for each generic `where` clause. The example above and the example below have the same behavior.*

```swift
extension Container where Item == Int {
    func average() -> Double {
        var sum = 0.0
        for index in 0..<count {
            sum += Double(self[index])
        }
        return sum / Double(count)
    }
}
extension Container where Item: Equatable {
    func endsWith(_ item: Item) -> Bool {
        return count >= 1 && self[count-1] == item
    }
}
```

*In the version of this example that uses contextual `where` clauses, the implementation of `average()` and `endsWith(_:)` are both in the same extension because each method’s generic `where` clause states the requirements that need to be satisfied to make that method available. Moving those requirements to the extensions’ generic `where` clauses makes the methods available in the same situations, but requires one extension per requirement.*
