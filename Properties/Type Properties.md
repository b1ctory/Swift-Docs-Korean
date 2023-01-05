## *Type Properties*

*Instance properties are properties that belong to an instance of a particular type. Every time you create a new instance of that type, it has its own set of property values, separate from any other instance.*

*You can also define properties that belong to the type itself, not to any one instance of that type. There will only ever be one copy of these properties, no matter how many instances of that type you create. These kinds of properties are called type properties.*

*Type properties are useful for defining values that are universal to all instances of a particular type, such as a constant property that all instances can use (like a static constant in C), or a variable property that stores a value that’s global to all instances of that type (like a static variable in C).*

*Stored type properties can be variables or constants. Computed type properties are always declared as variable properties, in the same way as computed instance properties.*

> *NOTE*
> 
> *Unlike stored instance properties, you must always give stored type properties a default value. This is because the type itself doesn’t have an initializer that can assign a value to a stored type property at initialization time.*
> 
> *Stored type properties are lazily initialized on their first access. They’re guaranteed to be initialized only once, even when accessed by multiple threads simultaneously, and they don’t need to be marked with the `lazy` modifier.*

### *Type Property Syntax*

*In C and Objective-C, you define static constants and variables associated with a type as global static variables. In Swift, however, type properties are written as part of the type’s definition, within the type’s outer curly braces, and each type property is explicitly scoped to the type it supports.*

*You define type properties with the `static` keyword. For computed type properties for class types, you can use the `class` keyword instead to allow subclasses to override the superclass’s implementation. The example below shows the syntax for stored and computed type properties:*

```swift
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 1
    }
}
enum SomeEnumeration {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 6
    }
}
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 27
    }
    class var overrideableComputedTypeProperty: Int {
        return 107
    }
}
```

> *NOTE*
> 
> *The computed type property examples above are for read-only computed type properties, but you can also define read-write computed type properties with the same syntax as for computed instance properties.*

### *Querying and Setting Type Properties*

*Type properties are queried and set with dot syntax, just like instance properties. However, type properties are queried and set on the type, not on an instance of that type. For example:*

```swift
print(SomeStructure.storedTypeProperty)
// Prints "Some value."
SomeStructure.storedTypeProperty = "Another value."
print(SomeStructure.storedTypeProperty)
// Prints "Another value."
print(SomeEnumeration.computedTypeProperty)
// Prints "6"
print(SomeClass.computedTypeProperty)
// Prints "27"
```

*The examples that follow use two stored type properties as part of a structure that models an audio level meter for a number of audio channels. Each channel has an integer audio level between `0` and `10` inclusive.*

*The figure below illustrates how two of these audio channels can be combined to model a stereo audio level meter. When a channel’s audio level is `0`, none of the lights for that channel are lit. When the audio level is `10`, all of the lights for that channel are lit. In this figure, the left channel has a current level of `9`, and the right channel has a current level of `7`:*

![](https://docs.swift.org/swift-book/_images/staticPropertiesVUMeter_2x.png)

*The audio channels described above are represented by instances of the `AudioChannel` structure:*

```swift
struct AudioChannel {
    static let thresholdLevel = 10
    static var maxInputLevelForAllChannels = 0
    var currentLevel: Int = 0 {
        didSet {
            if currentLevel > AudioChannel.thresholdLevel {
                // cap the new audio level to the threshold level
                currentLevel = AudioChannel.thresholdLevel
            }
            if currentLevel > AudioChannel.maxInputLevelForAllChannels {
                // store this as the new overall maximum input level
                AudioChannel.maxInputLevelForAllChannels = currentLevel
            }
        }
    }
}
```

*The `AudioChannel` structure defines two stored type properties to support its functionality. The first, `thresholdLevel`, defines the maximum threshold value an audio level can take. This is a constant value of `10` for all `AudioChannel` instances. If an audio signal comes in with a higher value than `10`, it will be capped to this threshold value (as described below).*

*The second type property is a variable stored property called `maxInputLevelForAllChannels`. This keeps track of the maximum input value that has been received by any `AudioChannel` instance. It starts with an initial value of `0`.*

*The `AudioChannel` structure also defines a stored instance property called `currentLevel`, which represents the channel’s current audio level on a scale of `0` to `10`.*

*The `currentLevel` property has a `didSet` property observer to check the value of `currentLevel` whenever it’s set. This observer performs two checks:*

- *If the new value of `currentLevel` is greater than the allowed `thresholdLevel`, the property observer caps `currentLevel` to `thresholdLevel`.*

- *If the new value of `currentLevel` (after any capping) is higher than any value previously received by any `AudioChannel` instance, the property observer stores the new `currentLevel` value in the `maxInputLevelForAllChannels` type property.*

> *NOTE*
> 
> *In the first of these two checks, the `didSet` observer sets `currentLevel` to a different value. This doesn’t, however, cause the observer to be called again.*

*You can use the `AudioChannel` structure to create two new audio channels called `leftChannel` and `rightChannel`, to represent the audio levels of a stereo sound system:*

```swift
var leftChannel = AudioChannel()
var rightChannel = AudioChannel()
```

*If you set the `currentLevel` of the left channel to `7`, you can see that the `maxInputLevelForAllChannels` type property is updated to equal `7`:*

```swift
leftChannel.currentLevel = 7
print(leftChannel.currentLevel)
// Prints "7"
print(AudioChannel.maxInputLevelForAllChannels)
// Prints "7"
```

*If you try to set the `currentLevel` of the right channel to `11`, you can see that the right channel’s `currentLevel` property is capped to the maximum value of `10`, and the `maxInputLevelForAllChannels` type property is updated to equal `10`:*

```swift

```
