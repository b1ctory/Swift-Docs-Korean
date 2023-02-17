## *Protocol Extensions : 프로토콜 확장*

*Protocols can be extended to provide method, initializer, subscript, and computed property implementations to conforming types. This allows you to define behavior on protocols themselves, rather than in each type’s individual conformance or in a global function.*

프로토콜은 타입을 준수하는 메서드, 이니셜라이저, 서브스크립트 및 연산 프로퍼티 구현을 제공하도록 확장될 수 있습니다. 이를 통해 각 타입의 개별 적합성 또는 전역 함수가 아닌 프로토콜 자체에서 동작을 정의할 수 있습니다.

*For example, the `RandomNumberGenerator` protocol can be extended to provide a `randomBool()` method, which uses the result of the required `random()` method to return a random `Bool` value:*

예를 들어, `RandomNumberGenerator` 프로토콜은 임의의 `Bool` 값을 반환하기 위해 필수 `random()` 메소드의 결과를 사용하는 `randomBool()` 메소드를 제공하도록 확장될 수 있습니다.

```swift
extension RandomNumberGenerator {
    func randomBool() -> Bool {
        return random() > 0.5
    }
}
```

*By creating an extension on the protocol, all conforming types automatically gain this method implementation without any additional modification.*

프로토콜에 확장을 생성함으로써 모든 준수 타입은 추가 수정 없이 이 메서드 구현을 자동으로 얻습니다.

```swift
let generator = LinearCongruentialGenerator()
print("Here's a random number: \(generator.random())")
// Prints "Here's a random number: 0.3746499199817101"
print("And here's a random Boolean: \(generator.randomBool())")
// Prints "And here's a random Boolean: true"
```

*Protocol extensions can add implementations to conforming types but can’t make a protocol extend or inherit from another protocol. Protocol inheritance is always specified in the protocol declaration itself.*

프로토콜 확장은 준수 유형에 구현을 추가할 수 있지만 프로토콜을 확장하거나 다른 프로토콜에서 상속하도록 만들 수는 없습니다. 프로토콜 상속은 항상 프로토콜 선언 자체에 지정됩니다.

### *Providing Default Implementations : 기본 구현 제공*

*You can use protocol extensions to provide a default implementation to any method or computed property requirement of that protocol. If a conforming type provides its own implementation of a required method or property, that implementation will be used instead of the one provided by the extension.*

프로토콜 확장을 사용하여 해당 프로토콜의 메서드 또는 연산 프로퍼티 요구 사항에 대한 기본 구현을 제공할 수 있습니다. 준수 타입이 필수 메서드 또는 프로퍼티의 자체 구현을 제공하는 경우 확장에서 제공하는 구현 대신 해당 구현이 사용됩니다.

> *NOTE*
> 
> *Protocol requirements with default implementations provided by extensions are distinct from optional protocol requirements. Although conforming types don’t have to provide their own implementation of either, requirements with default implementations can be called without optional chaining.*
> 
> 확장에서 제공하는 기본 구현이 있는 프로토콜 요구 사항은 옵셔널 프로토콜 요구 사항과 다릅니다. 타입을 준수하는 경우 자체 구현을 제공할 필요는 없지만 기본 구현이 있는 요구 사항은 옵셔널 체이닝 없이 호출할 수 있습니다.

*For example, the `PrettyTextRepresentable` protocol, which inherits the `TextRepresentable` protocol can provide a default implementation of its required `prettyTextualDescription` property to simply return the result of accessing the `textualDescription` property:*

예를 들어, `TextRepresentable` 프로토콜을 상속하는 `PrettyTextRepresentable` 프로토콜은 필수 `prettyTextualDescription` 프로퍼티의 기본 구현을 제공하여 단순히 `textualDescription` 프로퍼티에 액세스한 결과를 반환할 수 있습니다.

```swift
extension PrettyTextRepresentable  {
    var prettyTextualDescription: String {
        return textualDescription
    }
}
```

### *Adding Constraints to Protocol Extensions: 프로토콜 확장에 제약 추가*

*When you define a protocol extension, you can specify constraints that conforming types must satisfy before the methods and properties of the extension are available. You write these constraints after the name of the protocol you’re extending by writing a generic `where` clause. For more about generic `where` clauses, see [Generic Where Clauses](https://docs.swift.org/swift-book/LanguageGuide/Generics.html#ID192).*

프로토콜 확장을 정의할 때 준수 타입이 확장의 메서드 및 프로퍼티를 사용하기 전에 충족해야 하는 제약 조건을 지정할 수 있습니다. 일반적인 `where` 절을 작성하여 확장하려는 프로토콜의 이름 뒤에 이러한 제약 조건을 작성합니다. 일반적인 `where` 절에 대한 자세한 내용은 [링크]를 참조하세요.

*For example, you can define an extension to the `Collection` protocol that applies to any collection whose elements conform to the `Equatable` protocol. By constraining a collection’s elements to the `Equatable` protocol, a part of the standard library, you can use the `==` and `!=` operators to check for equality and inequality between two elements.*

예를 들어 요소가 `Equatable` 프로토콜을 준수하는 모든 컬렉션에 적용되는 `Collection` 프로토콜에 대한 확장을 정의할 수 있습니다. 컬렉션의 요소를 표준 라이브러리의 일부인 `Equatable` 프로토콜로 제한하면 `==` 및 `!=` 연산자를 사용하여 두 요소 사이의 동등 여부를 확인할 수 있습니다.

```swift
extension Collection where Element: Equatable {
    func allEqual() -> Bool {
        for element in self {
            if element != self.first {
                return false
            }
        }
        return true
    }
}
```

*The `allEqual()` method returns `true` only if all the elements in the collection are equal.*

`allEqual()` 메소드는 컬렉션의 모든 요소가 동일한 경우에만 `true`를 반환합니다.

*Consider two arrays of integers, one where all the elements are the same, and one where they aren’t:*

두 개의 정수 배열, 즉 모든 요소가 동일한 배열과 그렇지 않은 배열을 고려하세요.

```swift
let equalNumbers = [100, 100, 100, 100, 100]
let differentNumbers = [100, 100, 200, 100, 200]
```

*Because arrays conform to `Collection` and integers conform to `Equatable`, `equalNumbers` and `differentNumbers` can use the `allEqual()` method:*

배열은 `Collection`을 준수하고 정수는 `Equatable`을 준수하므로 `equalNumbers` 및 `differentNumbers`는 `allEqual()` 메서드를 사용할 수 있습니다.

```swift
print(equalNumbers.allEqual())
// Prints "true"
print(differentNumbers.allEqual())
// Prints "false"
```

> *NOTE*
> 
> *If a conforming type satisfies the requirements for multiple constrained extensions that provide implementations for the same method or property, Swift uses the implementation corresponding to the most specialized constraints.*
> 
> 일치하는 타입이 동일한 메서드 또는 프로퍼티에 대한 구현을 제공하는 여러 제약 확장에 대한 요구 사항을 충족하는 경우 Swift는 가장 특수화된 제약에 해당하는 구현을 사용합니다.
