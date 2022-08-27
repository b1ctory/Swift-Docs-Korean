## *For-In Loops*

*You use the `for`-`in` loop to iterate over a sequence, such as items in an array, ranges of numbers, or characters in a string.*

*This example uses a `for`-`in` loop to iterate over the items in an array:*

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!
```

*You can also iterate over a dictionary to access its key-value pairs. Each item in the dictionary is returned as a `(key, value)` tuple when the dictionary is iterated, and you can decompose the `(key, value)` tuple’s members as explicitly named constants for use within the body of the `for`-`in` loop. In the code example below, the dictionary’s keys are decomposed into a constant called `animalName`, and the dictionary’s values are decomposed into a constant called `legCount`.*

```swift
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// cats have 4 legs
// ants have 6 legs
// spiders have 8 legs
```

*The contents of a `Dictionary` are inherently unordered, and iterating over them doesn’t guarantee the order in which they will be retrieved. In particular, the order you insert items into a `Dictionary` doesn’t define the order they’re iterated. For more about arrays and dictionaries, see [Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html).*

*You can also use `for`-`in` loops with numeric ranges. This example prints the first few entries in a five-times table:*

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

*The sequence being iterated over is a range of numbers from `1` to `5`, inclusive, as indicated by the use of the closed range operator (`...`). The value of `index` is set to the first number in the range (`1`), and the statements inside the loop are executed. In this case, the loop contains only one statement, which prints an entry from the five-times table for the current value of `index`. After the statement is executed, the value of `index` is updated to contain the second value in the range (`2`), and the `print(_:separator:terminator:)` function is called again. This process continues until the end of the range is reached.*

*In the example above, `index` is a constant whose value is automatically set at the start of each iteration of the loop. As such, `index` doesn’t have to be declared before it’s used. It’s implicitly declared simply by its inclusion in the loop declaration, without the need for a `let` declaration keyword.*

*If you don’t need each value from a sequence, you can ignore the values by using an underscore in place of a variable name.*

```swift
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// Prints "3 to the power of 10 is 59049"
```

*The example above calculates the value of one number to the power of another (in this case, `3` to the power of `10`). It multiplies a starting value of `1` (that is, `3` to the power of `0`) by `3`, ten times, using a closed range that starts with `1` and ends with `10`. For this calculation, the individual counter values each time through the loop are unnecessary—the code simply executes the loop the correct number of times. The underscore character (`_`) used in place of a loop variable causes the individual values to be ignored and doesn’t provide access to the current value during each iteration of the loop.*

*In some situations, you might not want to use closed ranges, which include both endpoints. Consider drawing the tick marks for every minute on a watch face. You want to draw `60` tick marks, starting with the `0` minute. Use the half-open range operator (`..<`) to include the lower bound but not the upper bound. For more about ranges, see [Range Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html#ID73).*

```swift
let minutes = 60
for tickMark in 0..<minutes {
    // render the tick mark each minute (60 times)
}
```

*Some users might want fewer tick marks in their UI. They could prefer one mark every `5` minutes instead. Use the `stride(from:to:by:)` function to skip the unwanted marks.*

```swift
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}
```

*Closed ranges are also available, by using `stride(from:through:by:)` instead:*

```swift
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)
}
```

*The examples above use a `for`-`in` loop to iterate ranges, arrays, dictionaries, and strings. However, you can use this syntax to iterate any collection, including your own classes and collection types, as long as those types conform to the [`Sequence`](https://developer.apple.com/documentation/swift/sequence) protocol.*
