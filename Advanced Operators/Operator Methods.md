## *Operator Methods*

*Classes and structures can provide their own implementations of existing operators. This is known as overloading the existing operators.*

*The example below shows how to implement the arithmetic addition operator (`+`) for a custom structure. The arithmetic addition operator is a binary operator because it operates on two targets and it’s an infix operator because it appears between those two targets.*

*The example defines a `Vector2D` structure for a two-dimensional position vector `(x, y)`, followed by a definition of an operator method to add together instances of the `Vector2D` structure:*

```swift
struct Vector2D {
    var x = 0.0, y = 0.0
}

extension Vector2D {
    static func + (left: Vector2D, right: Vector2D) -> Vector2D {
       return Vector2D(x: left.x + right.x, y: left.y + right.y)
    }
}
```

*The operator method is defined as a type method on `Vector2D`, with a method name that matches the operator to be overloaded (`+`). Because addition isn’t part of the essential behavior for a vector, the type method is defined in an extension of `Vector2D` rather than in the main structure declaration of `Vector2D`. Because the arithmetic addition operator is a binary operator, this operator method takes two input parameters of type `Vector2D` and returns a single output value, also of type `Vector2D`.*

*In this implementation, the input parameters are named `left` and `right` to represent the `Vector2D` instances that will be on the left side and right side of the `+` operator. The method returns a new `Vector2D` instance, whose `x` and `y` properties are initialized with the sum of the `x` and `y` properties from the two `Vector2D` instances that are added together.*

*The type method can be used as an infix operator between existing `Vector2D` instances:*

```swift
let vector = Vector2D(x: 3.0, y: 1.0)
let anotherVector = Vector2D(x: 2.0, y: 4.0)
let combinedVector = vector + anotherVector
// combinedVector is a Vector2D instance with values of (5.0, 5.0)
```

*This example adds together the vectors `(3.0, 1.0)` and `(2.0, 4.0)` to make the vector `(5.0, 5.0)`, as illustrated below.*

*![](https://docs.swift.org/swift-book/images/vectorAddition@2x.png)*

### *Prefix and Postfix Operators*

*The example shown above demonstrates a custom implementation of a binary infix operator. Classes and structures can also provide implementations of the standard unary operators. Unary operators operate on a single target. They’re prefix if they precede their target (such as `-a`) and postfix operators if they follow their target (such as `b!`).*

*You implement a prefix or postfix unary operator by writing the `prefix` or `postfix` modifier before the `func` keyword when declaring the operator method:*

```swift
extension Vector2D {
    static prefix func - (vector: Vector2D) -> Vector2D {
        return Vector2D(x: -vector.x, y: -vector.y)
    }
}
```

*The example above implements the unary minus operator (`-a`) for `Vector2D` instances. The unary minus operator is a prefix operator, and so this method has to be qualified with the `prefix` modifier.*

*For simple numeric values, the unary minus operator converts positive numbers into their negative equivalent and vice versa. The corresponding implementation for `Vector2D` instances performs this operation on both the `x` and `y` properties:*

```swift
let positive = Vector2D(x: 3.0, y: 4.0)
let negative = -positive
// negative is a Vector2D instance with values of (-3.0, -4.0)
let alsoPositive = -negative
// alsoPositive is a Vector2D instance with values of (3.0, 4.0)
```

### *Compound Assignment Operators*

*Compound assignment operators combine assignment (`=`) with another operation. For example, the addition assignment operator (`+=`) combines addition and assignment into a single operation. You mark a compound assignment operator’s left input parameter type as `inout`, because the parameter’s value will be modified directly from within the operator method.*

*The example below implements an addition assignment operator method for `Vector2D` instances:*

```swift
extension Vector2D {
    static func += (left: inout Vector2D, right: Vector2D) {
        left = left + right
    }
}
```

*Because an addition operator was defined earlier, you don’t need to reimplement the addition process here. Instead, the addition assignment operator method takes advantage of the existing addition operator method, and uses it to set the left value to be the left value plus the right value:*

```swift
var original = Vector2D(x: 1.0, y: 2.0)
let vectorToAdd = Vector2D(x: 3.0, y: 4.0)
original += vectorToAdd
// original now has values of (4.0, 6.0)
```

> *Note*
> 
> *It isn’t possible to overload the default assignment operator (`=`). Only the compound assignment operators can be overloaded. Similarly, the ternary conditional operator (`a ? b : c`) can’t be overloaded.*

### *Equivalence Operators*

*By default, custom classes and structures don’t have an implementation of the equivalence operators, known as the equal to operator (`==`) and not equal to operator (`!=`). You usually implement the `==` operator, and use the standard library’s default implementation of the `!=` operator that negates the result of the `==` operator. There are two ways to implement the `==` operator: You can implement it yourself, or for many types, you can ask Swift to synthesize an implementation for you. In both cases, you add conformance to the standard library’s `Equatable` protocol.*

*You provide an implementation of the `==` operator in the same way as you implement other infix operators:*

```swift
extension Vector2Dextension Vector2D: Equatable {
    static func == (left: Vector2D, right: Vector2D) -> Bool {
       return (left.x == right.x) && (left.y == right.y)
    }
}: Equatable {    static func == (left: Vector2D, right: Vector2D) -> Bool {       return (left.x == right.x) && (left.y == right.y)    }}
```

*The example above implements an `==` operator to check whether two `Vector2D` instances have equivalent values. In the context of `Vector2D`, it makes sense to consider “equal” as meaning “both instances have the same `x` values and `y` values”, and so this is the logic used by the operator implementation.*

*You can now use this operator to check whether two `Vector2D` instances are equivalent:*

```swift
let twoThree = Vector2D(x: 2.0, y: 3.0)
let anotherTwoThree = Vector2D(x: 2.0, y: 3.0)
if twoThree == anotherTwoThree {
    print("These two vectors are equivalent.")
}
// Prints "These two vectors are equivalent."
```

*In many simple cases, you can ask Swift to provide synthesized implementations of the equivalence operators for you, as described in [Adopting a Protocol Using a Synthesized Implementation](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/protocols#Adopting-a-Protocol-Using-a-Synthesized-Implementation).*
