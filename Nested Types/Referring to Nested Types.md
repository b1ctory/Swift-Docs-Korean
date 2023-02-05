## *Referring to Nested Types: 중첩 타입 참조*

*To use a nested type outside of its definition context, prefix its name with the name of the type it’s nested within:*

정의 컨텍스트 외부에서 중첩된 타입을 사용하려면 이름 앞에 중첩된 타입의 이름을 붙입니다.

```swift
let heartsSymbol = BlackjackCard.Suit.hearts.rawValue
// heartsSymbol is "♡"
```

*For the example above, this enables the names of `Suit`, `Rank`, and `Values` to be kept deliberately short, because their names are naturally qualified by the context in which they’re defined.*

위의 예에서  `Suit`, `Rank`, 그리고 `Values`의 이름은 정의된 컨텍스트에 따라 자연스럽게 한정되기 때문에 이름을 의도적으로 짧게 유지할 수 있습니다.
