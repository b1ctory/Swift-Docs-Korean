## *Defining a Base Class*

*Any class that doesn’t inherit from another class is known as a base class.*

> *NOTE*
> 
> *Swift classes don’t inherit from a universal base class. Classes you define without specifying a superclass automatically become base classes for you to build upon.*

*The example below defines a base class called `Vehicle`. This base class defines a stored property called `currentSpeed`, with a default value of `0.0` (inferring a property type of `Double`). The `currentSpeed` property’s value is used by a read-only computed `String` property called `description` to create a description of the vehicle.*

*The `Vehicle` base class also defines a method called `makeNoise`. This method doesn’t actually do anything for a base `Vehicle` instance, but will be customized by subclasses of `Vehicle` later on:*

```swift
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    func makeNoise() {
        // do nothing - an arbitrary vehicle doesn't necessarily make a noise
    }
}
```

*You create a new instance of `Vehicle` with initializer syntax, which is written as a type name followed by empty parentheses:*

```swift
let someVehicle = Vehicle()
```

*Having created a new `Vehicle` instance, you can access its `description` property to print a human-readable description of the vehicle’s current speed:*

```swift
print("Vehicle: \(someVehicle.description)")
// Vehicle: traveling at 0.0 miles per hour
```

*The `Vehicle` class defines common characteristics for an arbitrary vehicle, but isn’t much use in itself. To make it more useful, you need to refine it to describe more specific kinds of vehicles.*


