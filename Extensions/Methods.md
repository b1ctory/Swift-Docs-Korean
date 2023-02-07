## Methods

Extensions can add new instance methods and type methods to existing types. The following example adds a new instance method called `repetitions` to the `Int` type:

```swift
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}
```

The `repetitions(task:)` method takes a single argument of type `() -> Void`, which indicates a function that has no parameters and doesn’t return a value.

After defining this extension, you can call the `repetitions(task:)` method on any integer to perform a task that many number of times:

```swift
3.repetitions {
    print("Hello!")
}
// Hello!
// Hello!
// Hello!
```

### Mutating Instance Methods

Instance methods added with an extension can also modify (or *mutate*) the instance itself. Structure and enumeration methods that modify `self` or its properties must mark the instance method as `mutating`, just like mutating methods from an original implementation.

The example below adds a new mutating method called `square` to Swift’s `Int` type, which squares the original value:

```swift
extension Int {
    mutating func square() {
        self = self * self
    }
}
var someInt = 3
someInt.square()
// someInt is now 9
```
