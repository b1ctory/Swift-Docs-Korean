## *Adopting a Protocol Using a Synthesized Implementation : 합성된 구현을 사용하여 프로토콜 채택*

*Swift can automatically provide the protocol conformance for `Equatable`, `Hashable`, and `Comparable` in many simple cases. Using this synthesized implementation means you don’t have to write repetitive boilerplate code to implement the protocol requirements yourself.*

Swift는 많은 간단한 경우에 `Equatable`, `Hashable`및 `Comparable`에 대한 프로토콜 적합성을 자동으로 제공할 수 있습니다. 이 합성 구현을 사용하면 프로토콜 요구 사항을 직접 구현하기 위해 반복적인 상용 코드를 작성할 필요가 없습니다.

*Swift provides a synthesized implementation of `Equatable` for the following kinds of custom types:*

Swift는 다음과 같은 사용자 정의 유형에 대해 `Equatable`의 합성된 구현을 제공합니다:

- *Structures that have only stored properties that conform to the `Equatable` protocol*
  
  `Equatable` 프로토콜을 준수하는 프로퍼티만 저장된 구조체입니다.

- *Enumerations that have only associated types that conform to the `Equatable` protocol*
  
  `Equatable` 프로토콜을 준수하는 연관된 타입만 있는 열거형입니다.

- *Enumerations that have no associated types*
  
  관련 타입이 없는 열거형입니다.

*To receive a synthesized implementation of `==`, declare conformance to `Equatable` in the file that contains the original declaration, without implementing an `==` operator yourself. The `Equatable` protocol provides a default implementation of `!=`.*

`==`의 합성 구현을 받으려면 `==` 연산자를 직접 구현하지 않고 원래 선언이 포함된 파일에서 `Equatable`에 대한 적합성을 선언하세요. `Equatable` 프로토콜은 `!=`의 기본 구현을 제공합니다.

*The example below defines a `Vector3D` structure for a three-dimensional position vector `(x, y, z)`, similar to the `Vector2D` structure. Because the `x`, `y`, and `z` properties are all of an `Equatable` type, `Vector3D` receives synthesized implementations of the equivalence operators.*

아래 예는 3차원 위치 벡터 `(x, y, z)`에 대한 `Vector3D` 구조체를 정의하며 `Vector2D` 구조체와 유사합니다. `x`, `y` 및 `z` 프로퍼티는 모두 `Equatable` 타입이므로 `Vector3D`는 등가 연산자의 합성된 구현을 수신합니다.

```swift
struct Vector3D: Equatable {
    var x = 0.0, y = 0.0, z = 0.0
}

let twoThreeFour = Vector3D(x: 2.0, y: 3.0, z: 4.0)
let anotherTwoThreeFour = Vector3D(x: 2.0, y: 3.0, z: 4.0)
if twoThreeFour == anotherTwoThreeFour {
    print("These two vectors are also equivalent.")
}
// Prints "These two vectors are also equivalent."
```

*Swift provides a synthesized implementation of `Hashable` for the following kinds of custom types:*

Swift는 다음과 같은 사용자 정의 유형에 대해 `Hashable`의 합성된 구현을 제공합니다:

- *Structures that have only stored properties that conform to the `Hashable` protocol*
  
  `Hashable` 프로토콜을 준수하는 프로퍼티만 저장된 구조체입니다.

- *Enumerations that have only associated types that conform to the `Hashable` protocol*
  
  `Hashable` 프로토콜을 준수하는 연관된 타입만 있는 열거형입니다.

- *Enumerations that have no associated types*
  
  관련 타입이 없는 열거형입니다.

*To receive a synthesized implementation of `hash(into:)`, declare conformance to `Hashable` in the file that contains the original declaration, without implementing a `hash(into:)` method yourself.*

`hash(into:)`의 합성된 구현을 수신하려면 `hash(into:)` 메서드를 직접 구현하지 않고 원래 선언이 포함된 파일에서 `Hashable`에 대한 적합성을 선언합니다.

*Swift provides a synthesized implementation of `Comparable` for enumerations that don’t have a raw value. If the enumeration has associated types, they must all conform to the `Comparable` protocol. To receive a synthesized implementation of `<`, declare conformance to `Comparable` in the file that contains the original enumeration declaration, without implementing a `<` operator yourself. The `Comparable` protocol’s default implementation of `<=`, `>`, and `>=` provides the remaining comparison operators.*

Swift는 원시 값이 없는 열거형에 대해 `Comparable`의 합성된 구현을 제공합니다. 열거형에 연결된 타입이 있는 경우 모두 `Comparable` 프로토콜을 준수해야 합니다. `<`의 합성된 구현을 수신하려면 `<` 연산자를 직접 구현하지 않고 원래 열거형 선언이 포함된 파일에서 `Comparable`에 대한 적합성을 선언합니다. `Comparable` 프로토콜의 기본 구현인 `<=`, `>` 및 `>=`는 나머지 비교 연산자를 제공합니다.

*The example below defines a `SkillLevel` enumeration with cases for beginners, intermediates, and experts. Experts are additionally ranked by the number of stars they have.*

아래 예시는 초심자, 중급자, 전문가를 위한 사례로 `SkillLevel` 열거형을 정의합니다. 전문가는 보유한 별의 수에 따라 추가로 순위가 매겨집니다.

```swift
enum SkillLevel: Comparable {
    case beginner
    case intermediate
    case expert(stars: Int)
}
var levels = [SkillLevel.intermediate, SkillLevel.beginner,
              SkillLevel.expert(stars: 5), SkillLevel.expert(stars: 3)]
for level in levels.sorted() {
    print(level)
}
// Prints "beginner"
// Prints "intermediate"
// Prints "expert(stars: 3)"
// Prints "expert(stars: 5)"
```
