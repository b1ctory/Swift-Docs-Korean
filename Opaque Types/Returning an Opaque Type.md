## *Returning an Opaque Type : 불투명 타입 반환*

*You can think of an opaque type like being the reverse of a generic type. Generic types let the code that calls a function pick the type for that function’s parameters and return value in a way that’s abstracted away from the function implementation. For example, the function in the following code returns a type that depends on its caller:*

불투명 타입은 제네릭 타입의 반대라고 생각하시면 됩니다. 일반 타입을 사용하면 함수를 호출하는 코드가 해당 함수의 매개변수 타입을 선택하고 함수 구현에서 추상화된 방식으로 값을 반환할 수 있습니다. 예를 들어 다음 코드의 함수는 호출자에 따라 달라지는 유형을 반환합니다.

```swift
func max<T>(_ x: T, _ y: T) -> T where T: Comparable { ... }
```

*The code that calls `max(_:_:)` chooses the values for `x` and `y`, and the type of those values determines the concrete type of `T`. The calling code can use any type that conforms to the `Comparable` protocol. The code inside the function is written in a general way so it can handle whatever type the caller provides. The implementation of `max(_:_:)` uses only functionality that all `Comparable` types share.*

`max(_:_:)`를 호출하는 코드는 `x` 및 `y`에 대한 값을 선택하고 이러한 값의 타입은 `T`의 구체적인 타입을 결정합니다. 호출 코드는 `Comparable` 프로토콜을 준수하는 모든 타입을 사용할 수 있습니다. 함수 내부의 코드는 호출자가 제공하는 모든 타입을 처리할 수 있도록 일반적인 방식으로 작성됩니다. `max(_:_:)` 구현은 모든 `Comparable` 타입이 공유하는 기능만 사용합니다.

*Those roles are reversed for a function with an opaque return type. An opaque type lets the function implementation pick the type for the value it returns in a way that’s abstracted away from the code that calls the function. For example, the function in the following example returns a trapezoid without exposing the underlying type of that shape.*

반환 타입이 불투명한 함수의 경우 이러한 역할이 반대입니다. 불투명 타입을 사용하면 함수 구현이 함수를 호출하는 코드에서 추상화된 방식으로 반환하는 값의 타입을 선택할 수 있습니다. 예를 들어 다음 예제의 함수는 해당 모양의 기본 타입을 노출하지 않고 사다리꼴을 반환합니다.

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

이 예에서 `makeTrapezoid()` 함수는 반환 타입을 `some Shape`로 선언합니다. 결과적으로 이 함수는 특정 구체적인 타입을 지정하지 않고 `Shape` 프로토콜을 준수하는 특정 타입의 값을 반환합니다. `makeTrapezoid()`를 이런 식으로 작성하면 공개 인터페이스의 일부에서 도형이 만들어지는 특정 타입을 만들지 않고도 공개 인터페이스의 기본 측면(반환하는 값은 도형)을 표현할 수 있습니다. 이 구현은 두 개의 삼각형과 사각형을 사용하지만 반환 타입을 변경하지 않고 다양한 다른 방법으로 사다리꼴을 그리도록 함수를 다시 작성할 수 있습니다.

*This example highlights the way that an opaque return type is like the reverse of a generic type. The code inside `makeTrapezoid()` can return any type it needs to, as long as that type conforms to the `Shape` protocol, like the calling code does for a generic function. The code that calls the function needs to be written in a general way, like the implementation of a generic function, so that it can work with any `Shape` value that’s returned by `makeTrapezoid()`.*

이 예는 불투명 반환 타입이 제네릭 타입의 반대와 같은 방식을 강조합니다. `makeTrapezoid()` 내부의 코드는 호출 코드가 일반 함수에 대해 수행하는 것처럼 해당 타입이 `Shape` 프로토콜을 준수하는 한 필요한 모든 타입을 반환할 수 있습니다. 함수를 호출하는 코드는 `makeTrapezoid()`에서 반환하는 모든 `Shape` 값과 함께 작동할 수 있도록 일반 함수 구현과 같은 일반적인 방식으로 작성해야 합니다.

*You can also combine opaque return types with generics. The functions in the following code both return a value of some type that conforms to the `Shape` protocol.*

불투명한 반환 타입을 제네릭과 결합할 수도 있습니다. 다음 코드의 함수는 모두 `Shape` 프로토콜을 준수하는 일부 타입의 값을 반환합니다.

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

이 예의 `opaqueJoinedTriangles` 값은 [링크] 섹션 앞부분에 있습니다. 그러나 이 예의 값과 달리 `flip(_:)`및 `join(_:_:)`은 일반 셰이프 작업이 반환하는 기본 타입을 불투명한 반환 타입으로 래핑하여 이러한 타입이 표시되지 않도록 합니다. 두 함수 모두 의존하는 타입이 일반적이고 함수에 대한 타입 매개변수가 `FlippedShape` 및 `JoinedShape`에 필요한 타입 정보를 전달하기 때문에 제네릭입니다.

*If a function with an opaque return type returns from multiple places, all of the possible return values must have the same type. For a generic function, that return type can use the function’s generic type parameters, but it must still be a single type. For example, here’s an invalid version of the shape-flipping function that includes a special case for squares:*

불투명 반환 타입을 가진 함수가 여러 위치에서 반환되는 경우 가능한 모든 반환 값은 동일한 타입이어야 합니다. 일반 함수의 경우 해당 반환 타입은 함수의 일반 타입 매개변수를 사용할 수 있지만 여전히 단일 타입이어야 합니다. 예를 들어 다음은 사각형에 대한 특수한 경우를 포함하는 도형 뒤집기 함수의 잘못된 버전입니다.

```swift
func invalidFlip<T: Shape>(_ shape: T) -> some Shape {
    if shape is Square {
        return shape // Error: return types don't match
    }
    return FlippedShape(shape: shape) // Error: return types don't match
}
```

*If you call this function with a `Square`, it returns a `Square`; otherwise, it returns a `FlippedShape`. This violates the requirement to return values of only one type and makes `invalidFlip(_:)` invalid code. One way to fix `invalidFlip(_:)` is to move the special case for squares into the implementation of `FlippedShape`, which lets this function always return a `FlippedShape` value:*

`Square`로 이 함수를 호출하면 `Square`를 반환합니다. 그렇지 않으면 `FlippedShape`를 반환합니다. 이는 한 가지 타입의 값만 반환해야 한다는 요구 사항을 위반하고 `invalidFlip(_:)`을 유효하지 않은 코드로 만듭니다. `invalidFlip(_:)`을 수정하는 한 가지 방법은 사각형의 특수한 경우를 `FlippedShape` 구현으로 이동하여 이 함수가 항상 `FlippedShape` 값을 반환하도록 하는 것입니다.

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

항상 단일 타입을 반환해야 한다는 요구 사항이 불투명 반환 타입에서 제네릭을 사용하는 것을 막지는 않습니다. 다음은 타입 매개변수를 반환하는 값의 기본 타입에 통합하는 함수의 예입니다.

```swift
func `repeat`<T: Shape>(shape: T, count: Int) -> some Collection {
    return Array<T>(repeating: shape, count: count)
}
```

*In this case, the underlying type of the return value varies depending on `T`: Whatever shape is passed it, `repeat(shape:count:)` creates and returns an array of that shape. Nevertheless, the return value always has the same underlying type of `[T]`, so it follows the requirement that functions with opaque return types must return values of only a single type.*

이 경우 반환 값의 기본 타입은 `T`에 따라 달라집니다. 어떤 모양이 전달되든`repeat(shape:count:)`는 해당 모양의 배열을 만들고 반환합니다. 그럼에도 불구하고 반환 값은 항상 동일한 기본 타입인 `[T]`를 가지므로 불투명한 반환 타입이 있는 함수는 단일 타입의 값만 반환해야 한다는 요구 사항을 따릅니다.
