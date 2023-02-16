## *Checking for Protocol Conformance*

*You can use the `is` and `as` operators described in [Type Casting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html) to check for protocol conformance, and to cast to a specific protocol. Checking for and casting to a protocol follows exactly the same syntax as checking for and casting to a type:*

- *The `is` operator returns `true` if an instance conforms to a protocol and returns `false` if it doesn’t.*

- *The `as?` version of the downcast operator returns an optional value of the protocol’s type, and this value is `nil` if the instance doesn’t conform to that protocol.*

- *The `as!` version of the downcast operator forces the downcast to the protocol type and triggers a runtime error if the downcast doesn’t succeed.*

*This example defines a protocol called `HasArea`, with a single property requirement of a gettable `Double` property called `area`:*

```swift
protocol HasArea {
    var area: Double { get }
}
```

*Here are two classes, `Circle` and `Country`, both of which conform to the `HasArea` protocol:*

```swift
class Circle: HasArea {
    let pi = 3.1415927
    var radius: Double
    var area: Double { return pi * radius * radius }
    init(radius: Double) { self.radius = radius }
}
class Country: HasArea {
    var area: Double
    init(area: Double) { self.area = area }
}
```

*The `Circle` class implements the `area` property requirement as a computed property, based on a stored `radius` property. The `Country` class implements the `area` requirement directly as a stored property. Both classes correctly conform to the `HasArea` protocol.*

*Here’s a class called `Animal`, which doesn’t conform to the `HasArea` protocol:*

```swift
class Animal {
    var legs: Int
    init(legs: Int) { self.legs = legs }
}
```

*The `Circle`, `Country` and `Animal` classes don’t have a shared base class. Nonetheless, they’re all classes, and so instances of all three types can be used to initialize an array that stores values of type `AnyObject`:*

```swift
let objects: [AnyObject] = [
    Circle(radius: 2.0),
    Country(area: 243_610),
    Animal(legs: 4)
]
```

*The `objects` array is initialized with an array literal containing a `Circle` instance with a radius of 2 units; a `Country` instance initialized with the surface area of the United Kingdom in square kilometers; and an `Animal` instance with four legs.*

*The `objects` array can now be iterated, and each object in the array can be checked to see if it conforms to the `HasArea` protocol:*

```swift
for object in objects {
    if let objectWithArea = object as? HasArea {
        print("Area is \(objectWithArea.area)")
    } else {
        print("Something that doesn't have an area")
    }
}
// Area is 12.5663708
// Area is 243610.0
// Something that doesn't have an area
```

*Whenever an object in the array conforms to the `HasArea` protocol, the optional value returned by the `as?` operator is unwrapped with optional binding into a constant called `objectWithArea`. The `objectWithArea` constant is known to be of type `HasArea`, and so its `area` property can be accessed and printed in a type-safe way.*

*Note that the underlying objects aren’t changed by the casting process. They continue to be a `Circle`, a `Country` and an `Animal`. However, at the point that they’re stored in the `objectWithArea` constant, they’re only known to be of type `HasArea`, and so only their `area` property can be accessed.*
