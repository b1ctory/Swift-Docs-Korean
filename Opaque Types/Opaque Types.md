# *Opaque Types : 불투명 타입*

*Hide implementation details about a value’s type.*

값 타입에 대한 구현 세부 정보를 숨깁니다.

*A function or method with an opaque return type hides its return value’s type information. Instead of providing a concrete type as the function’s return type, the return value is described in terms of the protocols it supports. Hiding type information is useful at boundaries between a module and code that calls into the module, because the underlying type of the return value can remain private. Unlike returning a value whose type is a protocol type, opaque types preserve type identity — the compiler has access to the type information, but clients of the module don’t.*

리턴 타입이 불투명한 함수 또는 메서드는 반환 값의 타입 정보를 숨깁니다. 함수의 반환 타입으로 구체적인 타입을 제공하는 대신 반환 값은 지원하는 프로토콜의 관점에서 설명됩니다. 반환 값의 기본 타입은 비공개로 유지될 수 있기 때문에 타입 정보를 숨기는 것은 모듈과 모듈을 호출하는 코드 사이의 경계에서 유용합니다. 형식이 프로토콜 타입인 값을 반환하는 것과 달리 불투명 타입은 타입 정체성을 유지합니다. 컴파일러는 타입 정보에 액세스할 수 있지만 모듈의 클라이언트는 그렇지 않습니다.

## *The Problem That Opaque Types Solve : 불투명 타입이 해결하는 문제*

*For example, suppose you’re writing a module that draws ASCII art shapes. The basic characteristic of an ASCII art shape is a `draw()` function that returns the string representation of that shape, which you can use as the requirement for the `Shape` protocol:*

예를 들어 ASCII 아트 도형을 그리는 모듈을 작성한다고 가정합니다. ASCII 아트 모양의 기본 특성은 해당 모양의 문자열 표현을 반환하는 `draw()` 함수이며, `Shape` 프로토콜의 요구 사항으로 사용할 수 있습니다.

```swift
protocol Shape {
    func draw() -> String
}

struct Triangle: Shape {
    var size: Int
    func draw() -> String {
       var result: [String] = []
       for length in 1...size {
           result.append(String(repeating: "*", count: length))
       }
       return result.joined(separator: "\n")
    }
}
let smallTriangle = Triangle(size: 3)
print(smallTriangle.draw())
// *
// **
// ***
```

*You could use generics to implement operations like flipping a shape vertically, as shown in the code below. However, there’s an important limitation to this approach: The flipped result exposes the exact generic types that were used to create it.*

제네릭을 사용하여 아래 코드와 같이 도형을 세로로 뒤집는 것과 같은 작업을 구현할 수 있습니다. 그러나 이 접근 방식에는 중요한 제한이 있습니다. 뒤집힌 결과는 그것을 생성하는 데 사용된 정확한 제네릭 타입을 노출합니다.

```swift
struct FlippedShape<T: Shape>: Shape {
    var shape: T
    func draw() -> String {
        let lines = shape.draw().split(separator: "\n")
        return lines.reversed().joined(separator: "\n")
    }
}
let flippedTriangle = FlippedShape(shape: smallTriangle)
print(flippedTriangle.draw())
// ***
// **
// *
```

*This approach to defining a `JoinedShape<T: Shape, U: Shape>` structure that joins two shapes together vertically, like the code below shows, results in types like `JoinedShape<FlippedShape<Triangle>, Triangle>` from joining a flipped triangle with another triangle.*

아래 코드와 같이 두 개의 도형을 수직으로 결합하는 `JoinedShape<T: Shape, U: Shape>` 구조체를 정의하는 접근 방식은 `JoinedShape<FlippedShape, Triangle>`과 같은 타입을 다른 삼각형과 결합하는 결과를 초래합니다.

```swift
struct JoinedShape<T: Shape, U: Shape>: Shape {
    var top: T
    var bottom: U
    func draw() -> String {
       return top.draw() + "\n" + bottom.draw()
    }
}
let joinedTriangles = JoinedShape(top: smallTriangle, bottom: flippedTriangle)
print(joinedTriangles.draw())
// *
// **
// ***
// ***
// **
// *
```

*Exposing detailed information about the creation of a shape allows types that aren’t meant to be part of the ASCII art module’s public interface to leak out because of the need to state the full return type. The code inside the module could build up the same shape in a variety of ways, and other code outside the module that uses the shape shouldn’t have to account for the implementation details about the list of transformations. Wrapper types like `JoinedShape` and `FlippedShape` don’t matter to the module’s users, and they shouldn’t be visible. The module’s public interface consists of operations like joining and flipping a shape, and those operations return another `Shape` value.*

도형 생성에 대한 자세한 정보를 노출하면 전체 반환 타입을 명시해야 하기 때문에 ASCII 아트 모듈의 공용 인터페이스의 일부가 아닌 타입이 누출될 수 있습니다. 모듈 내부의 코드는 다양한 방식으로 동일한 모양을 만들 수 있으며 모양을 사용하는 모듈 외부의 다른 코드는 변환 목록에 대한 구현 세부 정보를 설명할 필요가 없습니다. `JoinedShape` 및 `FlippedShape`와 같은 래퍼 타입은 모듈 사용자에게 중요하지 않으며 표시되어서는 안 됩니다. 모듈의 공개 인터페이스는 도형 결합 및 뒤집기와 같은 작업으로 구성되며 이러한 작업은 또 다른 `Shape` 값을 반환합니다.
