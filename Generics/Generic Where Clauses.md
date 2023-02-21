## *Generic Where Clauses*

*Type constraints, as described in [Type Constraints](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Type-Constraints), enable you to define requirements on the type parameters associated with a generic function, subscript, or type.*

*It can also be useful to define requirements for associated types. You do this by defining a generic where clause. A generic `where` clause enables you to require that an associated type must conform to a certain protocol, or that certain type parameters and associated types must be the same. A generic `where` clause starts with the `where` keyword, followed by constraints for associated types or equality relationships between types and associated types. You write a generic `where` clause right before the opening curly brace of a type or function’s body.*

*The example below defines a generic function called `allItemsMatch`, which checks to see if two `Container` instances contain the same items in the same order. The function returns a Boolean value of `true` if all items match and a value of `false` if they don’t.*

*The two containers to be checked don’t have to be the same type of container (although they can be), but they do have to hold the same type of items. This requirement is expressed through a combination of type constraints and a generic `where` clause:*

```swift
func allItemsMatch<C1: Container, C2: Container>
        (_ someContainer: C1, _ anotherContainer: C2) -> Bool
        where C1.Item == C2.Item, C1.Item: Equatable {

    // Check that both containers contain the same number of items.
    if someContainer.count != anotherContainer.count {
        return false
    }

    // Check each pair of items to see if they're equivalent.
    for i in 0..<someContainer.count {
        if someContainer[i] != anotherContainer[i] {
            return false
        }
    }

    // All items match, so return true.
    return true
}
```

*This function takes two arguments called `someContainer` and `anotherContainer`. The `someContainer` argument is of type `C1`, and the `anotherContainer` argument is of type `C2`. Both `C1` and `C2` are type parameters for two container types to be determined when the function is called.*

*The following requirements are placed on the function’s two type parameters:*

- *`C1` must conform to the `Container` protocol (written as `C1: Container`).*

- *`C2` must also conform to the `Container` protocol (written as `C2: Container`).*

- *The `Item` for `C1` must be the same as the `Item` for `C2` (written as `C1.Item == C2.Item`).*

- *The `Item` for `C1` must conform to the `Equatable` protocol (written as `C1.Item: Equatable`).*

*The first and second requirements are defined in the function’s type parameter list, and the third and fourth requirements are defined in the function’s generic `where` clause.*

*These requirements mean:*

- *`someContainer` is a container of type `C1`.*

- *`anotherContainer` is a container of type `C2`.*

- *`someContainer` and `anotherContainer` contain the same type of items.*

- *The items in `someContainer` can be checked with the not equal operator (`!=`) to see if they’re different from each other.*

*The third and fourth requirements combine to mean that the items in `anotherContainer` can also be checked with the `!=` operator, because they’re exactly the same type as the items in `someContainer`.*

*These requirements enable the `allItemsMatch(_:_:)` function to compare the two containers, even if they’re of a different container type.*

*The `allItemsMatch(_:_:)` function starts by checking that both containers contain the same number of items. If they contain a different number of items, there’s no way that they can match, and the function returns `false`.*

*After making this check, the function iterates over all of the items in `someContainer` with a `for`-`in` loop and the half-open range operator (`..<`). For each item, the function checks whether the item from `someContainer` isn’t equal to the corresponding item in `anotherContainer`. If the two items aren’t equal, then the two containers don’t match, and the function returns `false`.*

*If the loop finishes without finding a mismatch, the two containers match, and the function returns `true`.*

*Here’s how the `allItemsMatch(_:_:)` function looks in action:*

```swift
var stackOfStrings = Stack<String>()
stackOfStrings.push("uno")
stackOfStrings.push("dos")
stackOfStrings.push("tres")

var arrayOfStrings = ["uno", "dos", "tres"]

if allItemsMatch(stackOfStrings, arrayOfStrings) {
    print("All items match.")
} else {
    print("Not all items match.")
}
// Prints "All items match."
```

*The example above creates a `Stack` instance to store `String` values, and pushes three strings onto the stack. The example also creates an `Array` instance initialized with an array literal containing the same three strings as the stack. Even though the stack and the array are of a different type, they both conform to the `Container` protocol, and both contain the same type of values. You can therefore call the `allItemsMatch(_:_:)` function with these two containers as its arguments. In the example above, the `allItemsMatch(_:_:)` function correctly reports that all of the items in the two containers match.*
