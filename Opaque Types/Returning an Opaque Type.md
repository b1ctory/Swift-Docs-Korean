## *Returning an Opaque Type*

*You can think of an opaque type like being the reverse of a generic type. Generic types let the code that calls a function pick the type for that function’s parameters and return value in a way that’s abstracted away from the function implementation. For example, the function in the following code returns a type that depends on its caller:*

```swift
func max<T>(_ x: T, _ y: T) -> T where T: Comparable { ... }
```

*The code that calls `max(_:_:)` chooses the values for `x` and `y`, and the type of those values determines the concrete type of `T`. The calling code can use any type that conforms to the `Comparable` protocol. The code inside the function is written in a general way so it can handle whatever type the caller provides. The implementation of `max(_:_:)` uses only functionality that all `Comparable` types share.*

*Those roles are reversed for a function with an opaque return type. An opaque type lets the function implementation pick the type for the value it returns in a way that’s abstracted away from the code that calls the function. For example, the function in the following example returns a trapezoid without exposing the underlying type of that shape.*

```swift
struct Square: Shape {
    var size: Int
    func draw() -> String {
        let line = String(repeating: "*", count: size)
        let result = Array<String>(repeating: line, count: size)
        return result.joined(separator: "\n")
    }
}

func makeTrapezoid() -> some Shape {
    let top = Triangle(size: 2)
    let middle = Square(size: 2)
    let bottom = FlippedShape(shape: top)
    let trapezoid = JoinedShape(
        top: top,
        bottom: JoinedShape(top: middle, bottom: bottom)
    )
    return trapezoid
}
let trapezoid = makeTrapezoid()
print(trapezoid.draw())
// *
// **
// **
// **
// **
// *
```

*The `makeTrapezoid()` function in this example declares its return type as `some Shape`; as a result, the function returns a value of some given type that conforms to the `Shape` protocol, without specifying any particular concrete type. Writing `makeTrapezoid()` this way lets it express the fundamental aspect of its public interface — the value it returns is a shape — without making the specific types that the shape is made from a part of its public interface. This implementation uses two triangles and a square, but the function could be rewritten to draw a trapezoid in a variety of other ways without changing its return type.*

*This example highlights the way that an opaque return type is like the reverse of a generic type. The code inside `makeTrapezoid()` can return any type it needs to, as long as that type conforms to the `Shape` protocol, like the calling code does for a generic function. The code that calls the function needs to be written in a general way, like the implementation of a generic function, so that it can work with any `Shape` value that’s returned by `makeTrapezoid()`.*

*You can also combine opaque return types with generics. The functions in the following code both return a value of some type that conforms to the `Shape` protocol.*

```swift
func flip<T: Shape>(_ shape: T) -> some Shape {
    return FlippedShape(shape: shape)
}
func join<T: Shape, U: Shape>(_ top: T, _ bottom: U) -> some Shape {
    JoinedShape(top: top, bottom: bottom)
}

let opaqueJoinedTriangles = join(smallTriangle, flip(smallTriangle))
print(opaqueJoinedTriangles.draw())
// *
// **
// ***
// ***
// **
// *
```

*The value of `opaqueJoinedTriangles` in this example is the same as `joinedTriangles` in the generics example in the [The Problem That Opaque Types Solve](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/opaquetypes#The-Problem-That-Opaque-Types-Solve) section earlier in this chapter. However, unlike the value in that example, `flip(_:)` and `join(_:_:)` wrap the underlying types that the generic shape operations return in an opaque return type, which prevents those types from being visible. Both functions are generic because the types they rely on are generic, and the type parameters to the function pass along the type information needed by `FlippedShape` and `JoinedShape`.*

*If a function with an opaque return type returns from multiple places, all of the possible return values must have the same type. For a generic function, that return type can use the function’s generic type parameters, but it must still be a single type. For example, here’s an invalid version of the shape-flipping function that includes a special case for squares:*

```swift
func invalidFlip<T: Shape>(_ shape: T) -> some Shape {
    if shape is Square {
        return shape // Error: return types don't match
    }
    return FlippedShape(shape: shape) // Error: return types don't match
}
```

*If you call this function with a `Square`, it returns a `Square`; otherwise, it returns a `FlippedShape`. This violates the requirement to return values of only one type and makes `invalidFlip(_:)` invalid code. One way to fix `invalidFlip(_:)` is to move the special case for squares into the implementation of `FlippedShape`, which lets this function always return a `FlippedShape` value:*

```swift
struct FlippedShape<T: Shape>: Shape {
    var shape: T
    func draw() -> String {
        if shape is Square {
           return shape.draw()
        }
        let lines = shape.draw().split(separator: "\n")
        return lines.reversed().joined(separator: "\n")
    }
}
```

*The requirement to always return a single type doesn’t prevent you from using generics in an opaque return type. Here’s an example of a function that incorporates its type parameter into the underlying type of the value it returns:*

```swift
func `repeat`<T: Shape>(shape: T, count: Int) -> some Collection {
    return Array<T>(repeating: shape, count: count)
}
```

*In this case, the underlying type of the return value varies depending on `T`: Whatever shape is passed it, `repeat(shape:count:)` creates and returns an array of that shape. Nevertheless, the return value always has the same underlying type of `[T]`, so it follows the requirement that functions with opaque return types must return values of only a single type.*


