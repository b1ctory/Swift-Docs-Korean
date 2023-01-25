## *Chaining on Methods with Optional Return Values*

*The previous example shows how to retrieve the value of a property of optional type through optional chaining. You can also use optional chaining to call a method that returns a value of optional type, and to chain on that method’s return value if needed.*

*The example below calls the `Address` class’s `buildingIdentifier()` method through optional chaining. This method returns a value of type `String?`. As described above, the ultimate return type of this method call after optional chaining is also `String?`:*

```swift
if let buildingIdentifier = john.residence?.address?.buildingIdentifier() {
    print("John's building identifier is \(buildingIdentifier).")
}
// Prints "John's building identifier is The Larches."
```

*If you want to perform further optional chaining on this method’s return value, place the optional chaining question mark after the method’s parentheses:*

```swift
if let beginsWithThe =
    john.residence?.address?.buildingIdentifier()?.hasPrefix("The") {
    if beginsWithThe {
        print("John's building identifier begins with \"The\".")
    } else {
        print("John's building identifier doesn't begin with \"The\".")
    }
}
// Prints "John's building identifier begins with "The"."
```

> *NOTE*
> 
> *In the example above, you place the optional chaining question mark after the parentheses, because the optional value you are chaining on is the `buildingIdentifier()` method’s return value, and not the `buildingIdentifier()` method itself.*


