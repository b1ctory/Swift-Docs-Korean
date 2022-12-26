# *Closures*

*Closures are self-contained blocks of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and to lambdas in other programming languages.*

*Closures can capture and store references to any constants and variables from the context in which they’re defined. This is known as closing over those constants and variables. Swift handles all of the memory management of capturing for you.*

> *NOTE*
> 
> *Don’t worry if you aren’t familiar with the concept of capturing. It’s explained in detail below in [Capturing Values](https://docs.swift.org/swift-book/LanguageGuide/Closures.html#ID103).*

*Global and nested functions, as introduced in [Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html), are actually special cases of closures. Closures take one of three forms:*

- *Global functions are closures that have a name and don’t capture any values.*

- *Nested functions are closures that have a name and can capture values from their enclosing function.*

- *Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.*

*Swift’s closure expressions have a clean, clear style, with optimizations that encourage brief, clutter-free syntax in common scenarios. These optimizations include:*

- *Inferring parameter and return value types from context*

- *Implicit returns from single-expression closures*

- *Shorthand argument names*

- **Trailing closure syntax


