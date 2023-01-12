## *Overriding*

*A subclass can provide its own custom implementation of an instance method, type method, instance property, type property, or subscript that it would otherwise inherit from a superclass. This is known as overriding.*

*To override a characteristic that would otherwise be inherited, you prefix your overriding definition with the `override` keyword. Doing so clarifies that you intend to provide an override and haven’t provided a matching definition by mistake. Overriding by accident can cause unexpected behavior, and any overrides without the `override` keyword are diagnosed as an error when your code is compiled.*

*The `override` keyword also prompts the Swift compiler to check that your overriding class’s superclass (or one of its parents) has a declaration that matches the one you provided for the override. This check ensures that your overriding definition is correct.*

### *Accessing Superclass Methods, Properties, and Subscripts*

*When you provide a method, property, or subscript override for a subclass, it’s sometimes useful to use the existing superclass implementation as part of your override. For example, you can refine the behavior of that existing implementation, or store a modified value in an existing inherited variable.*

*Where this is appropriate, you access the superclass version of a method, property, or subscript by using the `super` prefix:*

- *An overridden method named `someMethod()` can call the superclass version of `someMethod()` by calling `super.someMethod()` within the overriding method implementation.*

- *An overridden property called `someProperty` can access the superclass version of `someProperty` as `super.someProperty` within the overriding getter or setter implementation.*

- *An overridden subscript for `someIndex` can access the superclass version of the same subscript as `super[someIndex]` from within the overriding subscript implementation.*

### *Overriding Methods*

*You can override an inherited instance or type method to provide a tailored or alternative implementation of the method within your subclass.*

*The following example defines a new subclass of `Vehicle` called `Train`, which overrides the `makeNoise()` method that `Train` inherits from `Vehicle`:*

```swift
class Train: Vehicle {
    override func makeNoise() {
        print("Choo Choo")
    }
}
```

*If you create a new instance of `Train` and call its `makeNoise()` method, you can see that the `Train` subclass version of the method is called:*

```swift
let train = Train()
train.makeNoise()
// Prints "Choo Choo"
```

### *Overriding Properties*

*You can override an inherited instance or type property to provide your own custom getter and setter for that property, or to add property observers to enable the overriding property to observe when the underlying property value changes.*

#### *Overriding Property Getters and Setters*

*You can provide a custom getter (and setter, if appropriate) to override any inherited property, regardless of whether the inherited property is implemented as a stored or computed property at source. The stored or computed nature of an inherited property isn’t known by a subclass—it only knows that the inherited property has a certain name and type. You must always state both the name and the type of the property you are overriding, to enable the compiler to check that your override matches a superclass property with the same name and type.*

*You can present an inherited read-only property as a read-write property by providing both a getter and a setter in your subclass property override. You can’t, however, present an inherited read-write property as a read-only property.*

> *NOTE*
> 
> *If you provide a setter as part of a property override, you must also provide a getter for that override. If you don’t want to modify the inherited property’s value within the overriding getter, you can simply pass through the inherited value by returning `super.someProperty` from the getter, where `someProperty` is the name of the property you are overriding.*

*The following example defines a new class called `Car`, which is a subclass of `Vehicle`. The `Car` class introduces a new stored property called `gear`, with a default integer value of `1`. The `Car` class also overrides the `description` property it inherits from `Vehicle`, to provide a custom description that includes the current gear:*

```swift
class Car: Vehicle {
    var gear = 1
    override var description: String {
        return super.description + " in gear \(gear)"
    }
}
```

*The override of the `description` property starts by calling `super.description`, which returns the `Vehicle` class’s `description` property. The `Car` class’s version of `description` then adds some extra text onto the end of this description to provide information about the current gear.*

*If you create an instance of the `Car` class and set its `gear` and `currentSpeed` properties, you can see that its `description` property returns the tailored description defined within the `Car` class:*

```swift
let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("Car: \(car.description)")
// Car: traveling at 25.0 miles per hour in gear 3
```

#### *Overriding Property Observers*

*You can use property overriding to add property observers to an inherited property. This enables you to be notified when the value of an inherited property changes, regardless of how that property was originally implemented. For more information on property observers, see [Property Observers](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID262).*

> *NOTE*
> 
> *You can’t add property observers to inherited constant stored properties or inherited read-only computed properties. The value of these properties can’t be set, and so it isn’t appropriate to provide a `willSet` or `didSet` implementation as part of an override.*
> 
> *Note also that you can’t provide both an overriding setter and an overriding property observer for the same property. If you want to observe changes to a property’s value, and you are already providing a custom setter for that property, you can simply observe any value changes from within the custom setter.*

*The following example defines a new class called `AutomaticCar`, which is a subclass of `Car`. The `AutomaticCar` class represents a car with an automatic gearbox, which automatically selects an appropriate gear to use based on the current speed:*

```swift
class AutomaticCar: Car {
    override var currentSpeed: Double {
        didSet {
            gear = Int(currentSpeed / 10.0) + 1
        }
    }
}
```

*Whenever you set the `currentSpeed` property of an `AutomaticCar` instance, the property’s `didSet` observer sets the instance’s `gear` property to an appropriate choice of gear for the new speed. Specifically, the property observer chooses a gear that’s the new `currentSpeed` value divided by `10`, rounded down to the nearest integer, plus `1`. A speed of `35.0` produces a gear of `4`:*

```swift
let automatic = AutomaticCar()
automatic.currentSpeed = 35.0
print("AutomaticCar: \(automatic.description)")
// AutomaticCar: traveling at 35.0 miles per hour in gear 4
```
