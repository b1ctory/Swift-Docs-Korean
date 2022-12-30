## *Raw Values*

*The barcode example in [Associated Values](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html#ID148) shows how cases of an enumeration can declare that they store associated values of different types. As an alternative to associated values, enumeration cases can come prepopulated with default values (called raw values), which are all of the same type.*

*Here’s an example that stores raw ASCII values alongside named enumeration cases:*

```swift
enum ASCIIControlCharacter: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}
```

*Here, the raw values for an enumeration called `ASCIIControlCharacter` are defined to be of type `Character`, and are set to some of the more common ASCII control characters. `Character` values are described in [Strings and Characters](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html).*

*Raw values can be strings, characters, or any of the integer or floating-point number types. Each raw value must be unique within its enumeration declaration.*

> *NOTE*
> 
> *Raw values are not the same as associated values. Raw values are set to prepopulated values when you first define the enumeration in your code, like the three ASCII codes above. The raw value for a particular enumeration case is always the same. Associated values are set when you create a new constant or variable based on one of the enumeration’s cases, and can be different each time you do so.*

### *Implicitly Assigned Raw Values*

*When you’re working with enumerations that store integer or string raw values, you don’t have to explicitly assign a raw value for each case. When you don’t, Swift automatically assigns the values for you.*

*For example, when integers are used for raw values, the implicit value for each case is one more than the previous case. If the first case doesn’t have a value set, its value is `0`.*

*The enumeration below is a refinement of the earlier `Planet` enumeration, with integer raw values to represent each planet’s order from the sun:*

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

*In the example above, `Planet.mercury` has an explicit raw value of `1`, `Planet.venus` has an implicit raw value of `2`, and so on.*

*When strings are used for raw values, the implicit value for each case is the text of that case’s name.*

*The enumeration below is a refinement of the earlier `CompassPoint` enumeration, with string raw values to represent each direction’s name:*

```swift
enum CompassPoint: String {
    case north, south, east, west
}
```

*In the example above, `CompassPoint.south` has an implicit raw value of `"south"`, and so on.*

*You access the raw value of an enumeration case with its `rawValue` property:*

```swift
let earthsOrder = Planet.earth.rawValue
// earthsOrder is 3

let sunsetDirection = CompassPoint.west.rawValue
// sunsetDirection is "west"
```

### *Initializing from a Raw Value*

*If you define an enumeration with a raw-value type, the enumeration automatically receives an initializer that takes a value of the raw value’s type (as a parameter called `rawValue`) and returns either an enumeration case or `nil`. You can use this initializer to try to create a new instance of the enumeration.*

*This example identifies Uranus from its raw value of `7`:*

```swift
let possiblePlanet = Planet(rawValue: 7)
// possiblePlanet is of type Planet? and equals Planet.uranus
```

*Not all possible `Int` values will find a matching planet, however. Because of this, the raw value initializer always returns an optional enumeration case. In the example above, `possiblePlanet` is of type `Planet?`, or “optional `Planet`.”*

> *NOTE*
> 
> *The raw value initializer is a failable initializer, because not every raw value will return an enumeration case. For more information, see [Failable Initializers](https://docs.swift.org/swift-book/ReferenceManual/Declarations.html#ID376).*

*If you try to find a planet with a position of `11`, the optional `Planet` value returned by the raw value initializer will be `nil`:*

```swift
let positionToFind = 11
if let somePlanet = Planet(rawValue: positionToFind) {
    switch somePlanet {
    case .earth:
        print("Mostly harmless")
    default:
        print("Not a safe place for humans")
    }
} else {
    print("There isn't a planet at position \(positionToFind)")
}
// Prints "There isn't a planet at position 11"
```

*This example uses optional binding to try to access a planet with a raw value of `11`. The statement `if let somePlanet = Planet(rawValue: 11)` creates an optional `Planet`, and sets `somePlanet` to the value of that optional `Planet` if it can be retrieved. In this case, it isn’t possible to retrieve a planet with a position of `11`, and so the `else` branch is executed instead.*
