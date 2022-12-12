## *Working with Characters*

*You can access the individual `Character` values for a `String` by iterating over the string with a `for`-`in` loop:*

```swift
for character in "Dog!🐶" {
    print(character)
}
// D
// o
// g
// !
// 🐶

```

*The `for`-`in` loop is described in [For-In Loops](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID121).*

*Alternatively, you can create a stand-alone `Character` constant or variable from a single-character string literal by providing a `Character` type annotation:*

```swift
let exclamationMark: Character = "!"
```

*`String` values can be constructed by passing an array of `Character` values as an argument to its initializer:*

```swift
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱"
```


