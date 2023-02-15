## *Collections of Protocol Types : 프로토콜 타입 컬렉션*

*A protocol can be used as the type to be stored in a collection such as an array or a dictionary, as mentioned in [Protocols as Types](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html#ID275). This example creates an array of `TextRepresentable` things:*

[링크]에서 언급한 바와 같이 배열 또는 딕셔너리와 같은 컬렉션에 저장할 타입으로 프로토콜을 사용할 수 있습니다. 이 예에서는 `TextRepresentable`의 배열을 만듭니다:

```swift
let things: [TextRepresentable] = [game, d12, simonTheHamster]
```

*It’s now possible to iterate over the items in the array, and print each item’s textual description:*

이제 배열의 항목을 반복하고 각 항목의 텍스트 설명을 출력할 수 있습니다:

```swift
for thing in things {
    print(thing.textualDescription)
}
// A game of Snakes and Ladders with 25 squares
// A 12-sided dice
// A hamster named Simon
```

*Note that the `thing` constant is of type `TextRepresentable`. It’s not of type `Dice`, or `DiceGame`, or `Hamster`, even if the actual instance behind the scenes is of one of those types. Nonetheless, because it’s of type `TextRepresentable`, and anything that’s `TextRepresentable` is known to have a `textualDescription` property, it’s safe to access `thing.textualDescription` each time through the loop.*

`thing` 상수는 `TextPresentable` 타입입니다. 실제 인스턴스가 이러한 타입 중 하나인 경우에도 `Dice`, `DiceGame` 또는 `Hamster` 타입이 아닙니다. 그럼에도 불구하고 `TextRepresentable` 타입이고 `TextRepresentable`인 모든 항목은 `textualDescription` 프로퍼티가 있는 것으로 알려져 있으므로 루프를 통해 매번 `thing.textualDescription`에 액세스하는 것이 안전합니다.


