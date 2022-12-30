## *Iterating over Enumeration Cases*

*For some enumerations, it’s useful to have a collection of all of that enumeration’s cases. You enable this by writing `: CaseIterable` after the enumeration’s name. Swift exposes a collection of all the cases as an `allCases` property of the enumeration type. Here’s an example:*

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}
let numberOfChoices = Beverage.allCases.count
print("\(numberOfChoices) beverages available")
// Prints "3 beverages available"
```

*In the example above, you write `Beverage.allCases` to access a collection that contains all of the cases of the `Beverage` enumeration. You can use `allCases` like any other collection—the collection’s elements are instances of the enumeration type, so in this case they’re `Beverage` values. The example above counts how many cases there are, and the example below uses a `for`-`in` loop to iterate over all the cases.*

```swift
for beverage in Beverage.allCases {
    print(beverage)
}
// coffee
// tea
// juice
```

*The syntax used in the examples above marks the enumeration as conforming to the [`CaseIterable`](https://developer.apple.com/documentation/swift/caseiterable) protocol. For information about protocols, see [Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).*


