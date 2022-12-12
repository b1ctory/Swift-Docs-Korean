## *Concatenating Strings and Characters*

`String` values can be added together (or *concatenated*) with the addition operator (`+`) to create a new `String` value:

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome now equals "hello there"
```

*You can also append a `String` value to an existing `String` variable with the addition assignment operator (`+=`):*

```swift
var instruction = "look over"
instruction += string2
// instruction now equals "look over there"
```

*You can append a `Character` value to a `String` variable with the `String` type’s `append()` method:*

```swift
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome now equals "hello there!"
```

> *NOTE*
> 
> *You can’t append a `String` or `Character` to an existing `Character` variable, because a `Character` value must contain a single character only.*

*If you’re using multiline string literals to build up the lines of a longer string, you want every line in the string to end with a line break, including the last line. For example:*

```swift
let badStart = """
one
two
"""
let end = """
three
"""
print(badStart + end)
// Prints two lines:
// one
// twothree

let goodStart = """
one
two

"""
print(goodStart + end)
// Prints three lines:
// one
// two
// three
```

*In the code above, concatenating `badStart` with `end` produces a two-line string, which isn’t the desired result. Because the last line of `badStart` doesn’t end with a line break, that line gets combined with the first line of `end`. In contrast, both lines of `goodStart` end with a line break, so when it’s combined with `end` the result has three lines, as expected.*


