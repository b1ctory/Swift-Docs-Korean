## *Referring to Nested Types*

*To use a nested type outside of its definition context, prefix its name with the name of the type it’s nested within:*

```swift
let heartsSymbol = BlackjackCard.Suit.hearts.rawValue
// heartsSymbol is "♡"

```

*For the example above, this enables the names of `Suit`, `Rank`, and `Values` to be kept deliberately short, because their names are naturally qualified by the context in which they’re defined.*


