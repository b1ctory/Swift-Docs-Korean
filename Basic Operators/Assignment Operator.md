## *Assignment Operator*

*The assignment operator (`a = b`) initializes or updates the value of `a` with the value of `b`:*

```swift
let b = 10
var a = 5
a = b
// a is now equal to 10
```

*If the right side of the assignment is a tuple with multiple values, its elements can be decomposed into multiple constants or variab*les at once:

```swift
let (x, y) = (1, 2)
// x is equal to 1, and y is equal to 2
```

*Unlike the assignment operator in C and Objective-C, the assignment operator in Swift doesn’t itself return a value. The following statement isn’t valid:*

```swift
if x = y {
    // This isn't valid, because x = y doesn't return a value.
}
```

*This feature prevents the assignment operator (`=`) from being used by accident when the equal to operator (`==`) is actually intended. By making `if x = y` invalid, Swift helps you to avoid these kinds of errors in your code.*


