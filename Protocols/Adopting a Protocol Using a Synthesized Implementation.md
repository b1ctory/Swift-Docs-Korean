## *Adopting a Protocol Using a Synthesized Implementation*

*Swift can automatically provide the protocol conformance for `Equatable`, `Hashable`, and `Comparable` in many simple cases. Using this synthesized implementation means you don’t have to write repetitive boilerplate code to implement the protocol requirements yourself.*

*Swift provides a synthesized implementation of `Equatable` for the following kinds of custom types:*

- *Structures that have only stored properties that conform to the `Equatable` protocol*

- *Enumerations that have only associated types that conform to the `Equatable` protocol*

- *Enumerations that have no associated types*

*To receive a synthesized implementation of `==`, declare conformance to `Equatable` in the file that contains the original declaration, without implementing an `==` operator yourself. The `Equatable` protocol provides a default implementation of `!=`.*

*The example below defines a `Vector3D` structure for a three-dimensional position vector `(x, y, z)`, similar to the `Vector2D` structure. Because the `x`, `y`, and `z` properties are all of an `Equatable` type, `Vector3D` receives synthesized implementations of the equivalence operators.*

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

- *Structures that have only stored properties that conform to the `Hashable` protocol*

- *Enumerations that have only associated types that conform to the `Hashable` protocol*

- *Enumerations that have no associated types*

*To receive a synthesized implementation of `hash(into:)`, declare conformance to `Hashable` in the file that contains the original declaration, without implementing a `hash(into:)` method yourself.*

*Swift provides a synthesized implementation of `Comparable` for enumerations that don’t have a raw value. If the enumeration has associated types, they must all conform to the `Comparable` protocol. To receive a synthesized implementation of `<`, declare conformance to `Comparable` in the file that contains the original enumeration declaration, without implementing a `<` operator yourself. The `Comparable` protocol’s default implementation of `<=`, `>`, and `>=` provides the remaining comparison operators.*

*The example below defines a `SkillLevel` enumeration with cases for beginners, intermediates, and experts. Experts are additionally ranked by the number of stars they have.*

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
