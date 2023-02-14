## *Collections of Protocol Types*

*A protocol can be used as the type to be stored in a collection such as an array or a dictionary, as mentioned in [Protocols as Types](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html#ID275). This example creates an array of `TextRepresentable` things:*

```swift
let things: [TextRepresentable] = [game, d12, simonTheHamster]
```

*It’s now possible to iterate over the items in the array, and print each item’s textual description:*

```swift
for thing in things {
    print(thing.textualDescription)
}
// A game of Snakes and Ladders with 25 squares
// A 12-sided dice
// A hamster named Simon
```

*Note that the `thing` constant is of type `TextRepresentable`. It’s not of type `Dice`, or `DiceGame`, or `Hamster`, even if the actual instance behind the scenes is of one of those types. Nonetheless, because it’s of type `TextRepresentable`, and anything that’s `TextRepresentable` is known to have a `textualDescription` property, it’s safe to access `thing.textualDescription` each time through the loop.*
