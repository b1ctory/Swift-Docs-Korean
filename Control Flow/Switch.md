### *Switch*

*A `switch` statement considers a value and compares it against several possible matching patterns. It then executes an appropriate block of code, based on the first pattern that matches successfully. A `switch` statement provides an alternative to the `if` statement for responding to multiple potential states.*

*In its simplest form, a `switch` statement compares a value against one or more values of the same type.*

```swift
switch some value to consider {
case value 1:
    respond to value 1
case value 2,
     value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
}
```

*Every `switch` statement consists of multiple possible cases, each of which begins with the `case` keyword. In addition to comparing against specific values, Swift provides several ways for each case to specify more complex matching patterns. These options are described later in this chapter.*

*Like the body of an `if` statement, each `case` is a separate branch of code execution. The `switch` statement determines which branch should be selected. This procedure is known as switching on the value that’s being considered.*

*Every `switch` statement must be exhaustive. That is, every possible value of the type being considered must be matched by one of the `switch` cases. If it’s not appropriate to provide a case for every possible value, you can define a default case to cover any values that aren’t addressed explicitly. This default case is indicated by the `default` keyword, and must always appear last.*

*This example uses a `switch` statement to consider a single lowercase character called `someCharacter`:*

```swift
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
// Prints "The last letter of the alphabet"
```

*The `switch` statement’s first case matches the first letter of the English alphabet, `a`, and its second case matches the last letter, `z`. Because the `switch` must have a case for every possible character, not just every alphabetic character, this `switch` statement uses a `default` case to match all characters other than `a` and `z`. This provision ensures that the `switch` statement is exhaustive.*

#### *No Implicit Fallthrough*

*In contrast with `switch` statements in C and Objective-C, `switch` statements in Swift don’t fall through the bottom of each case and into the next one by default. Instead, the entire `switch` statement finishes its execution as soon as the first matching `switch` case is completed, without requiring an explicit `break` statement. This makes the `switch` statement safer and easier to use than the one in C and avoids executing more than one `switch` case by mistake.*

> *NOTE*
> 
> *Although `break` isn’t required in Swift, you can use a `break` statement to match and ignore a particular case or to break out of a matched case before that case has completed its execution. For details, see [Break in a Switch Statement](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID139).*

*The body of each case must contain at least one executable statement. It isn’t valid to write the following code, because the first case is empty:*

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a": // Invalid, the case has an empty body
case "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// This will report a compile-time error.
```

*Unlike a `switch` statement in C, this `switch` statement doesn’t match both `"a"` and `"A"`. Rather, it reports a compile-time error that `case "a":` doesn’t contain any executable statements. This approach avoids accidental fallthrough from one case to another and makes for safer code that’s clearer in its intent.*

*To make a `switch` with a single case that matches both `"a"` and `"A"`, combine the two values into a compound case, separating the values with commas.*

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// Prints "The letter A"
```

*For readability, a compound case can also be written over multiple lines. For more information about compound cases, see [Compound Cases](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID548).*

> *NOTE*
> 
> *To explicitly fall through at the end of a particular `switch` case, use the `fallthrough` keyword, as described in [Fallthrough](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID140).*


