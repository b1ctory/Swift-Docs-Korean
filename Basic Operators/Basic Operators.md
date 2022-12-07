# *Basic Operators*

*An operator is a special symbol or phrase that you use to check, change, or combine values. For example, the addition operator (`+`) adds two numbers, as in `let i = 1 + 2`, and the logical AND operator (`&&`) combines two Boolean values, as in `if enteredDoorCode && passedRetinaScan`.*

*Swift supports the operators you may already know from languages like C, and improves several capabilities to eliminate common coding errors. The assignment operator (`=`) doesn’t return a value, to prevent it from being mistakenly used when the equal to operator (`==`) is intended. Arithmetic operators (`+`, `-`, `*`, `/`, `%` and so forth) detect and disallow value overflow, to avoid unexpected results when working with numbers that become larger or smaller than the allowed value range of the type that stores them. You can opt in to value overflow behavior by using Swift’s overflow operators, as described in [Overflow Operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID37).*

*Swift also provides range operators that aren’t found in C, such as `a..<b` and `a...b`, as a shortcut for expressing a range of values.*

*This chapter describes the common operators in Swift. [Advanced Operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html) covers Swift’s advanced operators, and describes how to define your own custom operators and implement the standard operators for your own custom types.*


