## *Differences Between Opaque Types and Protocol Types : 불투명 타입과 프로토콜 타입의 차이점*

*Returning an opaque type looks very similar to using a protocol type as the return type of a function, but these two kinds of return type differ in whether they preserve type identity. An opaque type refers to one specific type, although the caller of the function isn’t able to see which type; a protocol type can refer to any type that conforms to the protocol. Generally speaking, protocol types give you more flexibility about the underlying types of the values they store, and opaque types let you make stronger guarantees about those underlying types.*

불투명 타입을 반환하는 것은 함수의 반환 타입으로 프로토콜 타입을 사용하는 것과 매우 유사해 보이지만 이 두 종류의 반환 타입은 타입 동일성을 유지하는지 여부가 다릅니다. 불투명 타입은 하나의 특정 타입을 참조하지만 함수 호출자는 타입을 볼 수 없습니다. 프로토콜 타입은 프로토콜을 준수하는 모든 타입을 참조할 수 있습니다. 일반적으로 프로토콜 타입은 저장하는 값의 기본 타입에 대해 더 많은 유연성을 제공하고 불투명 타입을 사용하면 이러한 기본 타입에 대해 더 강력한 보증을 할 수 있습니다.

*For example, here’s a version of `flip(_:)` that uses a protocol type as its return type instead of an opaque return type:*

예를 들어 다음은 불투명한 반환 타입 대신 프로토콜 타입을 반환 타입으로 사용하는 `flip(_:)` 버전입니다.

```swift
func protoFlip<T: Shape>(_ shape: T) -> Shape {
    return FlippedShape(shape: shape)
}
```

*This version of `protoFlip(_:)` has the same body as `flip(_:)`, and it always returns a value of the same type. Unlike `flip(_:)`, the value that `protoFlip(_:)` returns isn’t required to always have the same type — it just has to conform to the `Shape` protocol. Put another way, `protoFlip(_:)` makes a much looser API contract with its caller than `flip(_:)` makes. It reserves the flexibility to return values of multiple types:*

이 버전의 `protoFlip(_:)`은 `flip(_:)`과 본문이 동일하며 항상 동일한 타입의 값을 반환합니다. `flip(_:)`과 달리 `protoFlip(_:)`이 반환하는 값은 항상 동일한 타입을 가질 필요가 없습니다. `Shape` 프로토콜을 준수하기만 하면 됩니다. 다른 말로 하면, `protoFlip(_:)`은 `flip(_:)`이 만드는 것보다 호출자와 훨씬 더 느슨한 API 계약을 만듭니다. 여러 타입의 값을 반환할 수 있는 유연성을 보유합니다.

```swift
func protoFlip<T: Shape>(_ shape: T) -> Shape {
    if shape is Square {
        return shape
    }

    return FlippedShape(shape: shape)
}
```

*The revised version of the code returns an instance of `Square` or an instance of `FlippedShape`, depending on what shape is passed in. Two flipped shapes returned by this function might have completely different types. Other valid versions of this function could return values of different types when flipping multiple instances of the same shape. The less specific return type information from `protoFlip(_:)` means that many operations that depend on type information aren’t available on the returned value. For example, it’s not possible to write an `==` operator comparing results returned by this function.*

수정된 버전의 코드는 전달된 도형에 따라 `Square` 인스턴스 또는 `FlippedShape` 인스턴스를 반환합니다. 이 함수에서 반환된 두 개의 뒤집힌 모양은 완전히 다른 타입을 가질 수 있습니다. 이 함수의 다른 유효한 버전은 동일한 도형의 여러 인스턴스를 뒤집을 때 다른 타입의 값을 반환할 수 있습니다. `protoFlip(_:)`의 덜 구체적인 반환 타입 정보는 반환된 값에서 타입 정보에 의존하는 많은 작업을 사용할 수 없음을 의미합니다. 예를 들어 이 함수에서 반환된 결과를 비교하는 `==` 연산자를 작성할 수 없습니다.

```swift
let protoFlippedTriangle = protoFlip(smallTriangle)
let sameThing = protoFlip(smallTriangle)
protoFlippedTriangle == sameThing  // Error
```

*The error on the last line of the example occurs for several reasons. The immediate issue is that the `Shape` doesn’t include an `==` operator as part of its protocol requirements. If you try adding one, the next issue you’ll encounter is that the `==` operator needs to know the types of its left-hand and right-hand arguments. This sort of operator usually takes arguments of type `Self`, matching whatever concrete type adopts the protocol, but adding a `Self` requirement to the protocol doesn’t allow for the type erasure that happens when you use the protocol as a type.*

예제 마지막 줄의 오류는 여러 가지 이유로 발생합니다. 문제는 `Shape`가 프로토콜 요구 사항의 일부로 `==` 연산자를 포함하지 않는다는 것입니다. 하나를 추가하려고 하면 다음에 직면하게 될 문제는 `==` 연산자가 왼쪽 인수와 오른쪽 인수의 타입을 알아야 한다는 것입니다. 이러한 종류의 연산자는 일반적으로 `Self` 타입의 인수를 사용하여 프로토콜을 채택하는 구체적인 타입과 일치하지만 프로토콜에 `Self` 요구사항을 추가하면 프로토콜을 타입으로 사용할 때 발생하는 타입 삭제가 허용되지 않습니다.

*Using a protocol type as the return type for a function gives you the flexibility to return any type that conforms to the protocol. However, the cost of that flexibility is that some operations aren’t possible on the returned values. The example shows how the `==` operator isn’t available — it depends on specific type information that isn’t preserved by using a protocol type.*

프로토콜 타입을 함수의 반환 타입으로 사용하면 프로토콜을 준수하는 모든 타입을 반환할 수 있는 유연성이 제공됩니다. 그러나 이러한 유연성의 비용은 반환된 값에 대해 일부 작업이 불가능하다는 것입니다. 예는 `==` 연산자를 사용할 수 없는 방법을 보여줍니다. 프로토콜 타입을 사용하여 보존되지 않는 특정 타입 정보에 따라 달라집니다.

*Another problem with this approach is that the shape transformations don’t nest. The result of flipping a triangle is a value of type `Shape`, and the `protoFlip(_:)` function takes an argument of some type that conforms to the `Shape` protocol. However, a value of a protocol type doesn’t conform to that protocol; the value returned by `protoFlip(_:)` doesn’t conform to `Shape`. This means code like `protoFlip(protoFlip(smallTriangle))` that applies multiple transformations is invalid because the flipped shape isn’t a valid argument to `protoFlip(_:)`.*

이 접근 방식의 또 다른 문제는 도형 변환이 중첩되지 않는다는 것입니다. 삼각형을 뒤집은 결과는 `Shape` 유형의 값이고 `protoFlip(_:)` 함수는 `Shape` 프로토콜을 준수하는 일부 타입의 인수를 취합니다. 그러나 프로토콜 타입의 값은 해당 프로토콜을 준수하지 않습니다. `protoFlip(_:)`에서 반환한 값이 `Shape`를 따르지 않습니다. 이는 뒤집힌 모양이 `protoFlip(_:)`에 대한 유효한 인수가 아니기 때문에 여러 변환을 적용하는 `protoFlip(protoFlip(smallTriangle))`과 같은 코드가 유효하지 않음을 의미합니다.

*In contrast, opaque types preserve the identity of the underlying type. Swift can infer associated types, which lets you use an opaque return value in places where a protocol type can’t be used as a return value. For example, here’s a version of the `Container` protocol from [Generics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics):*

대조적으로 불투명 타입은 기본 타입의 ID를 유지합니다. Swift는 관련 타입을 추론할 수 있으므로 프로토콜 타입을 반환 값으로 사용할 수 없는 위치에서 불투명 리턴 값을 사용할 수 있습니다. 예를 들어 다음은 [링크]의 `Container` 프로토콜 버전입니다.

```swift
protocol Container {
    associatedtype Item
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
extension Array: Container { }
```

*You can’t use `Container` as the return type of a function because that protocol has an associated type. You also can’t use it as constraint in a generic return type because there isn’t enough information outside the function body to infer what the generic type needs to be.*

프로토콜에 연결 타입이 있으므로 함수의 반환 타입으로 `Container`를 사용할 수 없습니다. 또한 제네릭 타입이 무엇이어야 하는지 추론할 수 있는 정보가 함수 본문 외부에 충분하지 않기 때문에 제네릭 리턴 타입에서 제약 조건으로 사용할 수 없습니다.

```swift
// Error: Protocol with associated types can't be used as a return type.
func makeProtocolContainer<T>(item: T) -> Container {
    return [item]
}

// Error: Not enough information to infer C.
func makeProtocolContainer<T, C: Container>(item: T) -> C {
    return [item]
}
```

*Using the opaque type `some Container` as a return type expresses the desired API contract — the function returns a container, but declines to specify the container’s type:*

반환 타입으로 불투명 타입 `some Container`를 사용하면 원하는 API 계약을 표현합니다. 함수는 컨테이너를 반환하지만 컨테이너 타입 지정을 거부합니다.

```swift
func makeOpaqueContainer<T>(item: T) -> some Container {
    return [item]
}
let opaqueContainer = makeOpaqueContainer(item: 12)
let twelve = opaqueContainer[0]
print(type(of: twelve))
// Prints "Int"
```

*The type of `twelve` is inferred to be `Int`, which illustrates the fact that type inference works with opaque types. In the implementation of `makeOpaqueContainer(item:)`, the underlying type of the opaque container is `[T]`. In this case, `T` is `Int`, so the return value is an array of integers and the `Item` associated type is inferred to be `Int`. The subscript on `Container` returns `Item`, which means that the type of `twelve` is also inferred to be `Int`.*

`twelve`의 타입은 `Int`로 유추되며 타입 유추는 불투명 타입에서 작동한다는 사실을 보여줍니다. `makeOpaqueContainer(item:)` 구현에서 불투명 컨테이너의 기본 타입은 `[T]`입니다. 이 경우 `T`는 `Int`이므로 반환 값은 정수 배열이고 `Item` 연관 타입은 `Int`로 유추됩니다. `Container`의 서브스크립트는 `Item`을 반환합니다. 즉, `twelve` 타입도 `Int`로 유추됩니다.
