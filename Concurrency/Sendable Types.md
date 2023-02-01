## *Sendable Types*

*Tasks and actors let you divide a program into pieces that can safely run concurrently. Inside of a task or an instance of an actor, the part of a program that contains mutable state, like variables and properties, is called a concurrency domain. Some kinds of data can’t be shared between concurrency domains, because that data contains mutable state, but it doesn’t protect against overlapping access.*

*A type that can be shared from one concurrency domain to another is known as a sendable type. For example, it can be passed as an argument when calling an actor method or be returned as the result of a task. The examples earlier in this chapter didn’t discuss sendability because those examples use simple value types that are always safe to share for the data being passed between concurrency domains. In contrast, some types aren’t safe to pass across concurrency domains. For example, a class that contains mutable properties and doesn’t serialize access to those properties can produce unpredictable and incorrect results when you pass instances of that class between different tasks.*

*You mark a type as being sendable by declaring conformance to the `Sendable` protocol. That protocol doesn’t have any code requirements, but it does have semantic requirements that Swift enforces. In general, there are three ways for a type to be sendable:*

- *The type is a value type, and its mutable state is made up of other sendable data—for example, a structure with stored properties that are sendable or an enumeration with associated values that are sendable.*

- *The type doesn’t have any mutable state, and its immutable state is made up of other sendable data—for example, a structure or class that has only read-only properties.*

- *The type has code that ensures the safety of its mutable state, like a class that’s marked `@MainActor` or a class that serializes access to its properties on a particular thread or queue.*

*For a detailed list of the semantic requirements, see the [`Sendable`](https://developer.apple.com/documentation/swift/sendable) protocol reference.*

*Some types are always sendable, like structures that have only sendable properties and enumerations that have only sendable associated values. For example:*

```swift
struct TemperatureReading: Sendable {
    var measurement: Int
}

extension TemperatureLogger {
    func addReading(from reading: TemperatureReading) {
        measurements.append(reading.measurement)
    }
}

let logger = TemperatureLogger(label: "Tea kettle", measurement: 85)
let reading = TemperatureReading(measurement: 45)
await logger.addReading(from: reading)
```

*Because `TemperatureReading` is a structure that has only sendable properties, and the structure isn’t marked `public` or `@usableFromInline`, it’s implicitly sendable. Here’s a version of the structure where conformance to the `Sendable` protocol is implied:*

```swift
struct TemperatureReading {
    var measurement: Int
}
```
