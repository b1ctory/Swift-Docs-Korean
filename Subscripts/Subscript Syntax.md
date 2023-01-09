## *Subscript Syntax*

*Subscripts enable you to query instances of a type by writing one or more values in square brackets after the instance name. Their syntax is similar to both instance method syntax and computed property syntax. You write subscript definitions with the `subscript` keyword, and specify one or more input parameters and a return type, in the same way as instance methods. Unlike instance methods, subscripts can be read-write or read-only. This behavior is communicated by a getter and setter in the same way as for computed properties:*

```swift
subscript(index: Int) -> Int {
    get {
        // Return an appropriate subscript value here.
    }
    set(newValue) {
        // Perform a suitable setting action here.
    }
}
```

*The type of `newValue` is the same as the return value of the subscript. As with computed properties, you can choose not to specify the setter’s `(newValue)` parameter. A default parameter called `newValue` is provided to your setter if you don’t provide one yourself.*

*As with read-only computed properties, you can simplify the declaration of a read-only subscript by removing the `get` keyword and its braces:*

```swift
subscript(index: Int) -> Int {
    // Return an appropriate subscript value here.
}
```

*Here’s an example of a read-only subscript implementation, which defines a `TimesTable` structure to represent an n-times-table of integers:*

```swift
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
print("six times three is \(threeTimesTable[6])")
// Prints "six times three is 18"
```

*In this example, a new instance of `TimesTable` is created to represent the three-times-table. This is indicated by passing a value of `3` to the structure’s `initializer` as the value to use for the instance’s `multiplier` parameter.*

*You can query the `threeTimesTable` instance by calling its subscript, as shown in the call to `threeTimesTable[6]`. This requests the sixth entry in the three-times-table, which returns a value of `18`, or `3` times `6`.*

> *NOTE*
> 
> *An n-times-table is based on a fixed mathematical rule. It isn’t appropriate to set `threeTimesTable[someIndex]` to a new value, and so the subscript for `TimesTable` is defined as a read-only subscript.*


