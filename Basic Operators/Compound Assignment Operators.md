## *Compound Assignment Operators*

*Like C, Swift provides compound assignment operators that combine assignment (`=`) with another operation. One example is the addition assignment operator (`+=`):*

```swift
var a = 1
a += 2
// a is now equal to 3
```

*The expression `a += 2` is shorthand for `a = a + 2`. Effectively, the addition and the assignment are combined into one operator that performs both tasks at the same time.*

> *NOTE*
> 
> *The compound assignment operators don’t return a value. For example, you can’t write `let b = a += 2`.*

*For information about the operators provided by the Swift standard library, see [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations).*


