## *Arithmetic Operators*

*Swift supports the four standard arithmetic operators for all number types:*

- *Addition (`+`)*

- *Subtraction (`-`)*

- *__Multiplication (`*`)__*

- *Division (`/`)*

```swift
1 + 2       // equals 3
5 - 3       // equals 2
2 * 3       // equals 6
10.0 / 2.5  // equals 4.0
```

*Unlike the arithmetic operators in C and Objective-C, the Swift arithmetic operators don’t allow values to overflow by default. You can opt in to value overflow behavior by using Swift’s overflow operators (such as `a &+ b`). See [Overflow Operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID37).*

*The addition operator is also supported for `String` concatenation:*

```swift
"hello, " + "world"  // equals "hello, world"
```



### *Remainder Operator*

*The remainder operator (`a % b`) works out how many multiples of `b` will fit inside `a` and returns the value that’s left over (known as the remainder).*

> NOTE
> 
> The remainder operator (`%`) is also known as a *modulo operator* in other languages. However, its behavior in Swift for negative numbers means that, strictly speaking, it’s a remainder rather than a modulo operation.

*Here’s how the remainder operator works. To calculate `9 % 4`, you first work out how many `4`s will fit inside `9`:*

![](https://docs.swift.org/swift-book/_images/remainderInteger_2x.png)

*You can fit two `4`s inside `9`, and the remainder is `1` (shown in orange).*

*In Swift, this would be written as:*

```swift
9 % 4 // equals 1
```

*To determine the answer for `a % b`, the `%` operator calculates the following equation and returns `remainder` as its output:*

> `a` = (`b` x `some multiplier`) + `remainder`

*where `some multiplier` is the largest number of multiples of `b` that will fit inside `a`.*

*Inserting `9` and `4` into this equation yields:*

> `9` = (`4` x `2`) + `1`

*The same method is applied when calculating the remainder for a negative value of `a`:*

```swift
-9 % 4 // equals -1
```

*Inserting `-9` and `4` into the equation yields:*

> `-9` = (`4` x `-2`) + `-1`

*giving a remainder value of `-1`.*

*The sign of `b` is ignored for negative values of `b`. This means that `a % b` and `a % -b` always give the same answer.*



### *Unary Minus Operator*

*The sign of a numeric value can be toggled using a prefixed `-`, known as the unary minus operator:*

```swift
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three"
```

*The unary minus operator (`-`) is prepended directly before the value it operates on, without any white space.*



### *Unary Plus Operator*

*The unary plus operator (`+`) simply returns the value it operates on, without any change:*

```swift
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
```

*Although the unary plus operator doesn’t actually do anything, you can use it to provide symmetry in your code for positive numbers when also using the unary minus operator for negative numbers.*


