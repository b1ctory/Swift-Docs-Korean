# *Advanced Operators*

*Define custom operators, perform bitwise operations, and use builder syntax.*

*In addition to the operators described in [Basic Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators), Swift provides several advanced operators that perform more complex value manipulation. These include all of the bitwise and bit shifting operators you will be familiar with from C and Objective-C.*

*Unlike arithmetic operators in C, arithmetic operators in Swift don’t overflow by default. Overflow behavior is trapped and reported as an error. To opt in to overflow behavior, use Swift’s second set of arithmetic operators that overflow by default, such as the overflow addition operator (`&+`). All of these overflow operators begin with an ampersand (`&`).*

*When you define your own structures, classes, and enumerations, it can be useful to provide your own implementations of the standard Swift operators for these custom types. Swift makes it easy to provide tailored implementations of these operators and to determine exactly what their behavior should be for each type you create.*

*You’re not limited to the predefined operators. Swift gives you the freedom to define your own custom infix, prefix, postfix, and assignment operators, with custom precedence and associativity values. These operators can be used and adopted in your code like any of the predefined operators, and you can even extend existing types to support the custom operators you define.*
