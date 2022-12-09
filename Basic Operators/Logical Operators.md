## *Logical Operators*

*Logical operators modify or combine the Boolean logic values `true` and `false`. Swift supports the three standard logical operators found in C-based languages:*

- *Logical NOT (`!a`)*

- *Logical AND (`a && b`)*

- *Logical OR (`a || b`)*

### *Logical NOT Operator*

*The logical NOT operator (`!a`) inverts a Boolean value so that `true` becomes `false`, and `false` becomes `true`.*

*The logical NOT operator is a prefix operator, and appears immediately before the value it operates on, without any white space. It can be read as “not `a`”, as seen in the following example:*

```swift
let allowedEntry = false
if !allowedEntry {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```

*The phrase `if !allowedEntry` can be read as “if not allowed entry.” The subsequent line is only executed if “not allowed entry” is true; that is, if `allowedEntry` is `false`.*

*As in this example, careful choice of Boolean constant and variable names can help to keep code readable and concise, while avoiding double negatives or confusing logic statements.*

### *Logical AND Operator*

*The logical AND operator (`a && b`) creates logical expressions where both values must be `true` for the overall expression to also be `true`.*

*If either value is `false`, the overall expression will also be `false`. In fact, if the first value is `false`, the second value won’t even be evaluated, because it can’t possibly make the overall expression equate to `true`. This is known as short-circuit evaluation.*

*This example considers two `Bool` values and only allows access if both values are `true`:*

```swift
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```

### *Logical OR Operator*

*The logical OR operator (`a || b`) is an infix operator made from two adjacent pipe characters. You use it to create logical expressions in which only one of the two values has to be `true` for the overall expression to be `true`.*

*Like the Logical AND operator above, the Logical OR operator uses short-circuit evaluation to consider its expressions. If the left side of a Logical OR expression is `true`, the right side isn’t evaluated, because it can’t change the outcome of the overall expression.*

*In the example below, the first `Bool` value (`hasDoorKey`) is `false`, but the second value (`knowsOverridePassword`) is `true`. Because one value is `true`, the overall expression also evaluates to `true`, and access is allowed:*

```swift
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

### *Combining Logical Operators*

*You can combine multiple logical operators to create longer compound expressions:*

```swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

*This example uses multiple `&&` and `||` operators to create a longer compound expression. However, the `&&` and `||` operators still operate on only two values, so this is actually three smaller expressions chained together. The example can be read as:*

*If we’ve entered the correct door code and passed the retina scan, or if we have a valid door key, or if we know the emergency override password, then allow access.*

*Based on the values of `enteredDoorCode`, `passedRetinaScan`, and `hasDoorKey`, the first two subexpressions are `false`. However, the emergency override password is known, so the overall compound expression still evaluates to `true`.*

> *NOTE*
> 
> *The Swift logical operators `&&` and `||` are left-associative, meaning that compound expressions with multiple logical operators evaluate the leftmost subexpression first.*

### *Explicit Parentheses*

*It’s sometimes useful to include parentheses when they’re not strictly needed, to make the intention of a complex expression easier to read. In the door access example above, it’s useful to add parentheses around the first part of the compound expression to make its intent explicit:*

```swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

*The parentheses make it clear that the first two values are considered as part of a separate possible state in the overall logic. The output of the compound expression doesn’t change, but the overall intention is clearer to the reader. Readability is always preferred over brevity; use parentheses where they help to make your intentions clear.*
