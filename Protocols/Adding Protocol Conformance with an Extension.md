## *Adding Protocol Conformance with an Extension : 확장을 사용하여 프로토콜 준수를 추가*

*You can extend an existing type to adopt and conform to a new protocol, even if you don’t have access to the source code for the existing type. Extensions can add new properties, methods, and subscripts to an existing type, and are therefore able to add any requirements that a protocol may demand. For more about extensions, see [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html).*

기존 타입에 대한 소스 코드에 액세스할 수 없는 경우에도 기존 타입을 확장하여 새 프로토콜을 채택하고 준수할 수 있습니다. 확장은 기존 타입에 새 프로퍼티, 메서드 및 서브스크립트를 추가할 수 있으므로 프로토콜이 요구할 수 있는 모든 요구 사항을 추가할 수 있습니다. 확장에 대한 자세한 내용은 [링크]를 참조하세요.

> *NOTE*
> 
> *Existing instances of a type automatically adopt and conform to a protocol when that conformance is added to the instance’s type in an extension.*
> 타입의 기존 인스턴스는 확장의 인스턴스 타입에 적합성이 추가될 때 프로토콜을 자동으로 채택하고 준수합니다.

*For example, this protocol, called `TextRepresentable`, can be implemented by any type that has a way to be represented as text. This might be a description of itself, or a text version of its current state:*

예를 들어, `TextRepresentable`이라고 하는 이 프로토콜은 텍스트로 표현되는 방법이 있는 모든 타입으로 구현될 수 있습니다. 자기 자신에 대한 설명이거나 현재 상태의 텍스트 버전일 수 있습니다:

```swift
protocol TextRepresentable {
    var textualDescription: String { get }
}
```

*The `Dice` class from above can be extended to adopt and conform to `TextRepresentable`:*

위의 `Dice` 클래스를 확장하여 `TextPresentable`을 채택하고 준수할 수 있습니다:

```swift
extension Dice: TextRepresentable {
    var textualDescription: String {
        return "A \(sides)-sided dice"
    }
}
```

*This extension adopts the new protocol in exactly the same way as if `Dice` had provided it in its original implementation. The protocol name is provided after the type name, separated by a colon, and an implementation of all requirements of the protocol is provided within the extension’s curly braces.*

이 확장은 `Dice`가 원래 구현에서 제공했던 것과 동일한 방식으로 새로운 프로토콜을 채택합니다. 프로토콜 이름은 타입 이름 뒤에 제공되며, 콜론으로 구분되며, 프로토콜의 모든 요구 사항에 대한 구현은 확장자의 중괄호 안에 제공됩니다.

*Any `Dice` instance can now be treated as `TextRepresentable`:*

이제 모든 `Dice` 인스턴스를 `TextPresentable`로 처리할 수 있습니다:

```swift
let d12 = Dice(sides: 12, generator: LinearCongruentialGenerator())
print(d12.textualDescription)
// Prints "A 12-sided dice"
```

*Similarly, the `SnakesAndLadders` game class can be extended to adopt and conform to the `TextRepresentable` protocol:*

마찬가지로, `SnakesAndLadders` 게임 클래스는 `TextRepresentable`프로토콜을 채택하고 준수하도록 확장될 수 있습니다:

```swift
extension SnakesAndLadders: TextRepresentable {
    var textualDescription: String {
        return "A game of Snakes and Ladders with \(finalSquare) squares"
    }
}
print(game.textualDescription)
// Prints "A game of Snakes and Ladders with 25 squares"
```

### *Conditionally Conforming to a Protocol*

*A generic type may be able to satisfy the requirements of a protocol only under certain conditions, such as when the type’s generic parameter conforms to the protocol. You can make a generic type conditionally conform to a protocol by listing constraints when extending the type. Write these constraints after the name of the protocol you’re adopting by writing a generic `where` clause. For more about generic `where` clauses, see [Generic Where Clauses](https://docs.swift.org/swift-book/LanguageGuide/Generics.html#ID192).*

일반 타입은 해당 타입의 일반 매개 변수가 프로토콜을 준수하는 경우와 같은 특정 조건에서만 프로토콜의 요구 사항을 충족할 수 있습니다. 타입을 확장할 때 제약 조건을 나열하여 일반 타입을 조건부로 프로토콜에 적합하게 만들 수 있습니다. 일반적인 `where` 절을 작성하여 채택하는 프로토콜의 이름 뒤에 이러한 제약 조건을 작성합니다. 일반적인 `where` 절에 대한 자세한 내용은 [링크]를 참조하세요.

*The following extension makes `Array` instances conform to the `TextRepresentable` protocol whenever they store elements of a type that conforms to `TextRepresentable`.*

다음 확장은 `Array` 인스턴스가 `TextPresentable`을 준수하는 타입의 요소를 저장할 때마다 `TextPresentable` 프로토콜을 준수하도록 합니다.

```swift
extension Array: TextRepresentable where Element: TextRepresentable {
    var textualDescription: String {
        let itemsAsText = self.map { $0.textualDescription }
        return "[" + itemsAsText.joined(separator: ", ") + "]"
    }
}
let myDice = [d6, d12]
print(myDice.textualDescription)
// Prints "[A 6-sided dice, A 12-sided dice]"
```

### *Declaring Protocol Adoption with an Extension : 확장을 통해 프로토콜 채택 선언*

*If a type already conforms to all of the requirements of a protocol, but hasn’t yet stated that it adopts that protocol, you can make it adopt the protocol with an empty extension:*

어떤 타입이 이미 프로토콜의 모든 요구 사항을 준수하지만 아직 해당 프로토콜을 채택한다고 명시하지 않은 경우, 다음과 같이 빈 확장명을 사용하여 프로토콜을 채택하도록 할 수 있습니다:

```swift
struct Hamster {
    var name: String
    var textualDescription: String {
        return "A hamster named \(name)"
    }
}
extension Hamster: TextRepresentable {}
```

*Instances of `Hamster` can now be used wherever `TextRepresentable` is the required type:*

이제 `Hamster`의 인스턴스는 `TextPresentable`이 필요한 타입이면 어디서나 사용할 수 있습니다:

```swift
let simonTheHamster = Hamster(name: "Simon")
let somethingTextRepresentable: TextRepresentable = simonTheHamster
print(somethingTextRepresentable.textualDescription)
// Prints "A hamster named Simon"
```

> *NOTE*
> 
> *Types don’t automatically adopt a protocol just by satisfying its requirements. They must always explicitly declare their adoption of the protocol.*
> 
> 타입은 요구 사항을 충족하는 것만으로 프로토콜을 자동으로 채택하지 않습니다. 그들은 항상 프로토콜의 채택을 명시적으로 선언해야 합니다.


