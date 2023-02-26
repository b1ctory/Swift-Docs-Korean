## *ARC in Action*

*Here’s an example of how Automatic Reference Counting works. This example starts with a simple class called `Person`, which defines a stored constant property called `name`:*

```swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}
```

*The `Person` class has an initializer that sets the instance’s `name` property and prints a message to indicate that initialization is underway. The `Person` class also has a deinitializer that prints a message when an instance of the class is deallocated.*

*The next code snippet defines three variables of type `Person?`, which are used to set up multiple references to a new `Person` instance in subsequent code snippets. Because these variables are of an optional type (`Person?`, not `Person`), they’re automatically initialized with a value of `nil`, and don’t currently reference a `Person` instance.*

```swift
var reference1: Person?
var reference2: Person?
var reference3: Person?
```

*You can now create a new `Person` instance and assign it to one of these three variables:*

```swift
reference1 = Person(name: "John Appleseed")
// Prints "John Appleseed is being initialized"
```

*Note that the message `"John Appleseed is being initialized"` is printed at the point that you call the `Person` class’s initializer. This confirms that initialization has taken place.*

*Because the new `Person` instance has been assigned to the `reference1` variable, there’s now a strong reference from `reference1` to the new `Person` instance. Because there’s at least one strong reference, ARC makes sure that this `Person` is kept in memory and isn’t deallocated.*

*If you assign the same `Person` instance to two more variables, two more strong references to that instance are established:*

```swift
reference2 = reference1
reference3 = reference1
```

*There are now three strong references to this single `Person` instance.*

*If you break two of these strong references (including the original reference) by assigning `nil` to two of the variables, a single strong reference remains, and the `Person` instance isn’t deallocated:*

```swift
reference1 = nil
reference2 = nil
```

*ARC doesn’t deallocate the `Person` instance until the third and final strong reference is broken, at which point it’s clear that you are no longer using the `Person` instance:*

```swift
reference3 = nil
// Prints "John Appleseed is being deinitialized"
```
