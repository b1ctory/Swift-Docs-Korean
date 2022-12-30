## *Matching Enumeration Values with a Switch Statement*

*You can match individual enumeration values with a `switch` statement:*

```swift
directionToHead = .south
switch directionToHead {
case .north:
    print("Lots of planets have a north")
case .south:
    print("Watch out for penguins")
case .east:
    print("Where the sun rises")
case .west:
    print("Where the skies are blue")
}
// Prints "Watch out for penguins"
```

*You can read this code as:*

*“Consider the value of `directionToHead`. In the case where it equals `.north`, print `"Lots of planets have a north"`. In the case where it equals `.south`, print `"Watch out for penguins"`.”…and so on.*

*As described in [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html), a `switch` statement must be exhaustive when considering an enumeration’s cases. If the `case` for `.west` is omitted, this code doesn’t compile, because it doesn’t consider the complete list of `CompassPoint` cases. Requiring exhaustiveness ensures that enumeration cases aren’t accidentally omitted.*

*When it isn’t appropriate to provide a `case` for every enumeration case, you can provide a `default` case to cover any cases that aren’t addressed explicitly:*

```swift
let somePlanet = Planet.earth
switch somePlanet {
case .earth:
    print("Mostly harmless")
default:
    print("Not a safe place for humans")
}
// Prints "Mostly harmless"
Iterating over Enumera
```
