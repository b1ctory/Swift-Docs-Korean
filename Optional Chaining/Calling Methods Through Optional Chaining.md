## *Calling Methods Through Optional Chaining*

*You can use optional chaining to call a method on an optional value, and to check whether that method call is successful. You can do this even if that method doesn’t define a return value.*

*The `printNumberOfRooms()` method on the `Residence` class prints the current value of `numberOfRooms`. Here’s how the method looks:*

```swift
func printNumberOfRooms() {
    print("The number of rooms is \(numberOfRooms)")
}

```

*This method doesn’t specify a return type. However, functions and methods with no return type have an implicit return type of `Void`, as described in [Functions Without Return Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID163). This means that they return a value of `()`, or an empty tuple.*

*If you call this method on an optional value with optional chaining, the method’s return type will be `Void?`, not `Void`, because return values are always of an optional type when called through optional chaining. This enables you to use an `if` statement to check whether it was possible to call the `printNumberOfRooms()` method, even though the method doesn’t itself define a return value. Compare the return value from the `printNumberOfRooms` call against `nil` to see if the method call was successful:*

```swift
if john.residence?.printNumberOfRooms() != nil {
    print("It was possible to print the number of rooms.")
} else {
    print("It was not possible to print the number of rooms.")
}
// Prints "It was not possible to print the number of rooms."
```

*The same is true if you attempt to set a property through optional chaining. The example above in [Accessing Properties Through Optional Chaining](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html#ID248) attempts to set an `address` value for `john.residence`, even though the `residence` property is `nil`. Any attempt to set a property through optional chaining returns a value of type `Void?`, which enables you to compare against `nil` to see if the property was set successfully:*

```swift
if (john.residence?.address = someAddress) != nil {
    print("It was possible to set the address.")
} else {
    print("It was not possible to set the address.")
}
// Prints "It was not possible to set the address."
```


