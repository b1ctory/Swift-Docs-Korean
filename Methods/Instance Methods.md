## *Instance Methods*

*Instance methods are functions that belong to instances of a particular class, structure, or enumeration. They support the functionality of those instances, either by providing ways to access and modify instance properties, or by providing functionality related to the instance’s purpose. Instance methods have exactly the same syntax as functions, as described in [Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html).*

*You write an instance method within the opening and closing braces of the type it belongs to. An instance method has implicit access to all other instance methods and properties of that type. An instance method can be called only on a specific instance of the type it belongs to. It can’t be called in isolation without an existing instance.*

*Here’s an example that defines a simple `Counter` class, which can be used to count the number of times an action occurs:*

```swift
class Counter {
    var count = 0
    func increment() {
        count += 1
    }
    func increment(by amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}
```

*The `Counter` class defines three instance methods:*

- *`increment()` increments the counter by `1`.*

- *`increment(by: Int)` increments the counter by a specified integer amount.*

- *`reset()` resets the counter to zero.*

*The `Counter` class also declares a variable property, `count`, to keep track of the current counter value.*

*You call instance methods with the same dot syntax as properties:*

```swift
let counter = Counter()
// the initial counter value is 0
counter.increment()
// the counter's value is now 1
counter.increment(by: 5)
// the counter's value is now 6
counter.reset()
// the counter's value is now 0
```

*Function parameters can have both a name (for use within the function’s body) and an argument label (for use when calling the function), as described in [Function Argument Labels and Parameter Names](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID166). The same is true for method parameters, because methods are just functions that are associated with a type.*

### *The self Property*

*Every instance of a type has an implicit property called `self`, which is exactly equivalent to the instance itself. You use the `self` property to refer to the current instance within its own instance methods.*

*The `increment()` method in the example above could have been written like this:*

```swift
func increment() {
    self.count += 1
}
```

*In practice, you don’t need to write `self` in your code very often. If you don’t explicitly write `self`, Swift assumes that you are referring to a property or method of the current instance whenever you use a known property or method name within a method. This assumption is demonstrated by the use of `count` (rather than `self.count`) inside the three instance methods for `Counter`.*

*The main exception to this rule occurs when a parameter name for an instance method has the same name as a property of that instance. In this situation, the parameter name takes precedence, and it becomes necessary to refer to the property in a more qualified way. You use the `self` property to distinguish between the parameter name and the property name.*

*Here, `self` disambiguates between a method parameter called `x` and an instance property that’s also called `x`:*

```swift
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOf(x: Double) -> Bool {
        return self.x > x
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOf(x: 1.0) {
    print("This point is to the right of the line where x == 1.0")
}
// Prints "This point is to the right of the line where x == 1.0"
```

*Without the `self` prefix, Swift would assume that both uses of `x` referred to the method parameter called `x`.*

### *Modifying Value Types from Within Instance Methods*

*Structures and enumerations are value types. By default, the properties of a value type can’t be modified from within its instance methods.*

*However, if you need to modify the properties of your structure or enumeration within a particular method, you can opt in to mutating behavior for that method. The method can then mutate (that is, change) its properties from within the method, and any changes that it makes are written back to the original structure when the method ends. The method can also assign a completely new instance to its implicit `self` property, and this new instance will replace the existing one when the method ends.*

*You can opt in to this behavior by placing the `mutating` keyword before the `func` keyword for that method:*

```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
// Prints "The point is now at (3.0, 4.0)"
```

*The `Point` structure above defines a mutating `moveBy(x:y:)` method, which moves a `Point` instance by a certain amount. Instead of returning a new point, this method actually modifies the point on which it’s called. The `mutating` keyword is added to its definition to enable it to modify its properties.*

*Note that you can’t call a mutating method on a constant of structure type, because its properties can’t be changed, even if they’re variable properties, as described in [Stored Properties of Constant Structure Instances](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID256):*

```swift
let fixedPoint = Point(x: 3.0, y: 3.0)
fixedPoint.moveBy(x: 2.0, y: 3.0)
// this will report an error
```

### *Assigning to self Within a Mutating Method*

*Mutating methods can assign an entirely new instance to the implicit `self` property. The `Point` example shown above could have been written in the following way instead:*

```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}
```

*This version of the mutating `moveBy(x:y:)` method creates a new structure whose `x` and `y` values are set to the target location. The end result of calling this alternative version of the method will be exactly the same as for calling the earlier version.*

*Mutating methods for enumerations can set the implicit `self` parameter to be a different case from the same enumeration:*

```swift
enum TriStateSwitch {
    case off, low, high
    mutating func next() {
        switch self {
        case .off:
            self = .low
        case .low:
            self = .high
        case .high:
            self = .off
        }
    }
}
var ovenLight = TriStateSwitch.low
ovenLight.next()
// ovenLight is now equal to .high
ovenLight.next()
// ovenLight is now equal to .off
```

*This example defines an enumeration for a three-state switch. The switch cycles between three different power states (`off`, `low` and `high`) every time its `next()` method is called.*


