## *Method Requirements*

*Protocols can require specific instance methods and type methods to be implemented by conforming types. These methods are written as part of the protocol’s definition in exactly the same way as for normal instance and type methods, but without curly braces or a method body. Variadic parameters are allowed, subject to the same rules as for normal methods. Default values, however, can’t be specified for method parameters within a protocol’s definition.*

*As with type property requirements, you always prefix type method requirements with the `static` keyword when they’re defined in a protocol. This is true even though type method requirements are prefixed with the `class` or `static` keyword when implemented by a class:*

```swift
protocol SomeProtocol {
    static func someTypeMethod()
}
```

*The following example defines a protocol with a single instance method requirement:*

```swift
protocol RandomNumberGenerator {
    func random() -> Double
}
```

*This protocol, `RandomNumberGenerator`, requires any conforming type to have an instance method called `random`, which returns a `Double` value whenever it’s called. Although it’s not specified as part of the protocol, it’s assumed that this value will be a number from `0.0` up to (but not including) `1.0`.*

*The `RandomNumberGenerator` protocol doesn’t make any assumptions about how each random number will be generated—it simply requires the generator to provide a standard way to generate a new random number.*

*Here’s an implementation of a class that adopts and conforms to the `RandomNumberGenerator` protocol. This class implements a pseudorandom number generator algorithm known as a linear congruential generator:*

```swift
class LinearCongruentialGenerator: RandomNumberGenerator {
    var lastRandom = 42.0
    let m = 139968.0
    let a = 3877.0
    let c = 29573.0
    func random() -> Double {
        lastRandom = ((lastRandom * a + c)
            .truncatingRemainder(dividingBy:m))
        return lastRandom / m
    }
}
let generator = LinearCongruentialGenerator()
print("Here's a random number: \(generator.random())")
// Prints "Here's a random number: 0.3746499199817101"
print("And another one: \(generator.random())")
// Prints "And another one: 0.729023776863283"
```
