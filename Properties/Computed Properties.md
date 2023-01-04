## *Computed Properties*

*In addition to stored properties, classes, structures, and enumerations can define computed properties, which don’t actually store a value. Instead, they provide a getter and an optional setter to retrieve and set other properties and values indirectly.*

```swift
struct Point {
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
                  size: Size(width: 10.0, height: 10.0))
let initialSquareCenter = square.center
// initialSquareCenter is at (5.0, 5.0)
square.center = Point(x: 15.0, y: 15.0)
print("square.origin is now at (\(square.origin.x), \(square.origin.y))")
// Prints "square.origin is now at (10.0, 10.0)"
```

*This example defines three structures for working with geometric shapes:*

- *`Point` encapsulates the x- and y-coordinate of a point.*

- *`Size` encapsulates a `width` and a `height`.*

- *`Rect` defines a rectangle by an origin point and a size.*

*The `Rect` structure also provides a computed property called `center`. The current center position of a `Rect` can always be determined from its `origin` and `size`, and so you don’t need to store the center point as an explicit `Point` value. Instead, `Rect` defines a custom getter and setter for a computed variable called `center`, to enable you to work with the rectangle’s `center` as if it were a real stored property.*

*The example above creates a new `Rect` variable called `square`. The `square` variable is initialized with an origin point of `(0, 0)`, and a width and height of `10`. This square is represented by the light green square in the diagram below.*

*The `square` variable’s `center` property is then accessed through dot syntax (`square.center`), which causes the getter for `center` to be called, to retrieve the current property value. Rather than returning an existing value, the getter actually calculates and returns a new `Point` to represent the center of the square. As can be seen above, the getter correctly returns a center point of `(5, 5)`.*

*The `center` property is then set to a new value of `(15, 15)`, which moves the square up and to the right, to the new position shown by the dark green square in the diagram below. Setting the `center` property calls the setter for `center`, which modifies the `x` and `y` values of the stored `origin` property, and moves the square to its new position.*

![](https://docs.swift.org/swift-book/_images/computedProperties_2x.png)

### *Shorthand Setter Declaration*

*If a computed property’s setter doesn’t define a name for the new value to be set, a default name of `newValue` is used. Here’s an alternative version of the `Rect` structure that takes advantage of this shorthand notation:*

```swift
struct AlternativeRect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }
    }
}
```

### *Shorthand Getter Declaration*

*If the entire body of a getter is a single expression, the getter implicitly returns that expression. Here’s an another version of the `Rect` structure that takes advantage of this shorthand notation and the shorthand notation for setters:*

```swift
struct CompactRect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            Point(x: origin.x + (size.width / 2),
                  y: origin.y + (size.height / 2))
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }
    }
}
```

*Omitting the `return` from a getter follows the same rules as omitting `return` from a function, as described in [Functions With an Implicit Return](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID607).*

### *Read-Only Computed Properties*

*A computed property with a getter but no setter is known as a read-only computed property. A read-only computed property always returns a value, and can be accessed through dot syntax, but can’t be set to a different value.*

> *NOTE*
> 
> *You must declare computed properties—including read-only computed properties—as variable properties with the `var` keyword, because their value isn’t fixed. The `let` keyword is only used for constant properties, to indicate that their values can’t be changed once they’re set as part of instance initialization.*

*You can simplify the declaration of a read-only computed property by removing the `get` keyword and its braces:*

```swift
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
        return width * height * depth
    }
}
let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
print("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
// Prints "the volume of fourByFiveByTwo is 40.0"
```

*This example defines a new structure called `Cuboid`, which represents a 3D rectangular box with `width`, `height`, and `depth` properties. This structure also has a read-only computed property called `volume`, which calculates and returns the current volume of the cuboid. It doesn’t make sense for `volume` to be settable, because it would be ambiguous as to which values of `width`, `height`, and `depth` should be used for a particular `volume` value*. Nonetheless, it’s useful for a `Cuboid` to provide a read-only computed property to enable external users to discover its current calculated volume.
