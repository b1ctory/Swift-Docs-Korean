## *Comparing Structures and Classes*

*Structures and classes in Swift have many things in common. Both can:*

- *Define properties to store values*

- *Define methods to provide functionality*

- *Define subscripts to provide access to their values using subscript syntax*

- *Define initializers to set up their initial state*

- *Be extended to expand their functionality beyond a default implementation*

- *Conform to protocols to provide standard functionality of a certain kind*

*For more information, see [Properties](https://docs.swift.org/swift-book/LanguageGuide/Properties.html), [Methods](https://docs.swift.org/swift-book/LanguageGuide/Methods.html), [Subscripts](https://docs.swift.org/swift-book/LanguageGuide/Subscripts.html), [Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html), [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html), and [Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).*

*Classes have additional capabilities that structures don’t have:*

- *Inheritance enables one class to inherit the characteristics of another.*

- *Type casting enables you to check and interpret the type of a class instance at runtime.*

- *Deinitializers enable an instance of a class to free up any resources it has assigned.*

- *Reference counting allows more than one reference to a class instance.*

*For more information, see [Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html), [Type Casting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html), [Deinitialization](https://docs.swift.org/swift-book/LanguageGuide/Deinitialization.html), and [Automatic Reference Counting](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html).*

*The additional capabilities that classes support come at the cost of increased complexity. As a general guideline, prefer structures because they’re easier to reason about, and use classes when they’re appropriate or necessary. In practice, this means most of the custom data types you define will be structures and enumerations. For a more detailed comparison, see [Choosing Between Structures and Classes](https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes).*

> *NOTE*
> 
> *Classes and actors share many of the same characteristics and behaviors. For information about actors, see [Concurrency](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html).*

### *Definition Syntax*

*Structures and classes have a similar definition syntax. You introduce structures with the `struct` keyword and classes with the `class` keyword. Both place their entire definition within a pair of braces:*

```swift
struct SomeStructure {
    // structure definition goes here
}
class SomeClass {
    // class definition goes here
}
```

> *NOTE*
> 
> *Whenever you define a new structure or class, you define a new Swift type. Give types `UpperCamelCase` names (such as `SomeStructure` and `SomeClass` here) to match the capitalization of standard Swift types (such as `String`, `Int`, and `Bool`). Give properties and methods `lowerCamelCase` names (such as `frameRate` and `incrementCount`) to differentiate them from type names.*

*Here’s an example of a structure definition and a class definition:*

```swift
struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```

*The example above defines a new structure called `Resolution`, to describe a pixel-based display resolution. This structure has two stored properties called `width` and `height`. Stored properties are constants or variables that are bundled up and stored as part of the structure or class. These two properties are inferred to be of type `Int` by setting them to an initial integer value of `0`.*

*The example above also defines a new class called `VideoMode`, to describe a specific video mode for video display. This class has four variable stored properties. The first, `resolution`, is initialized with a new `Resolution` structure instance, which infers a property type of `Resolution`. For the other three properties, new `VideoMode` instances will be initialized with an `interlaced` setting of `false` (meaning “noninterlaced video”), a playback frame rate of `0.0`, and an optional `String` value called `name`. The `name` property is automatically given a default value of `nil`, or “no `name` value”, because it’s of an optional type.*

### *Structure and Class Instances*

*The `Resolution` structure definition and the `VideoMode` class definition only describe what a `Resolution` or `VideoMode` will look like. They themselves don’t describe a specific resolution or video mode. To do that, you need to create an instance of the structure or class.*

*The syntax for creating instances is very similar for both structures and classes:*

```swift
let someResolution = Resolution()
let someVideoMode = VideoMode()
```

Structures and classes both use initializer syntax for new instances. The simplest form of initializer syntax uses the type name of the class or structure followed by empty parentheses, such as `Resolution()` or `VideoMode()`. This creates a new instance of the class or structure, with any properties initialized to their default values. Class and structure initialization is described in more detail in [Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html).*

### *Accessing Properties*

*You can access the properties of an instance using dot syntax. In dot syntax, you write the property name immediately after the instance name, separated by a period (`.`), without any spaces:*

```swift
print("The width of someResolution is \(someResolution.width)")
// Prints "The width of someResolution is 0"
```

*In this example, `someResolution.width` refers to the `width` property of `someResolution`, and returns its default initial value of `0`.*

*You can drill down into subproperties, such as the `width` property in the `resolution` property of a `VideoMode`:*

```swift
print("The width of someVideoMode is \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is 0"
```

*You can also use dot syntax to assign a new value to a variable property:*

```swift
someVideoMode.resolution.width = 1280
print("The width of someVideoMode is now \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is now 1280"
```

### *Memberwise Initializers for Structure Types*

*All structures have an automatically generated memberwise initializer, which you can use to initialize the member properties of new structure instances. Initial values for the properties of the new instance can be passed to the memberwise initializer by name:*

```swift
let vga = Resolution(width: 640, height: 480)
```

*Unlike structures*, *class instances don’t receive a default memberwise initializer. Initializers are described in more detail in* [Initialization](https://docs.swift.org/swift-book*/LanguageGuide/Initialization.html).


