## *Enumeration Syntax*

*You introduce enumerations with the `enum` keyword and place their entire definition within a pair of braces:*

```swift
enum SomeEnumeration {
    // enumeration definition goes here
}
```

*Here’s an example for the four main points of a compass:*

```swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```

*The values defined in an enumeration (such as `north`, `south`, `east`, and `west`) are its enumeration cases. You use the `case` keyword to introduce new enumeration cases.*

> *NOTE*
> 
> *Swift enumeration cases don’t have an integer value set by default, unlike languages like C and Objective-C. In the `CompassPoint` example above, `north`, `south`, `east` and `west` don’t implicitly equal `0`, `1`, `2` and `3`. Instead, the different enumeration cases are values in their own right, with an explicitly defined type of `CompassPoint`.*

*Multiple cases can appear on a single line, separated by commas:*

```swift
enum Planet {
    case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

*Each enumeration definition defines a new type. Like other types in Swift, their names (such as `CompassPoint` and `Planet`) start with a capital letter. Give enumeration types singular rather than plural names, so that they read as self-evident:*

```swift
var directionToHead = CompassPoint.west
```

*The type of `directionToHead` is inferred when it’s initialized with one of the possible values of `CompassPoint`. Once `directionToHead` is declared as a `CompassPoint`, you can set it to a different `CompassPoint` value using a shorter dot syntax:*

```swift
directionToHead = .east
```

*The type of `directionToHead` is already known, and so you can drop the type when setting its value. This makes for highly readable code when working with explicitly typed enumeration values.*
