## *Capturing Values*

*A closure can capture constants and variables from the surrounding context in which it’s defined. The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.*

*In Swift, the simplest form of a closure that can capture values is a nested function, written within the body of another function. A nested function can capture any of its outer function’s arguments and can also capture any constants and variables defined within the outer function.*

*Here’s an example of a function called `makeIncrementer`, which contains a nested function called `incrementer`. The nested `incrementer()` function captures two values, `runningTotal` and `amount`, from its surrounding context. After capturing these values, `incrementer` is returned by `makeIncrementer` as a closure that increments `runningTotal` by `amount` each time it’s called.*

```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}
```

*The return type of `makeIncrementer` is `() -> Int`. This means that it returns a function, rather than a simple value. The function it returns has no parameters, and returns an `Int` value each time it’s called. To learn how functions can return other functions, see [Function Types as Return Types](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID177).*

*The `makeIncrementer(forIncrement:)` function defines an integer variable called `runningTotal`, to store the current running total of the incrementer that will be returned. This variable is initialized with a value of `0`.*

*The `makeIncrementer(forIncrement:)` function has a single `Int` parameter with an argument label of `forIncrement`, and a parameter name of `amount`. The argument value passed to this parameter specifies how much `runningTotal` should be incremented by each time the returned incrementer function is called. The `makeIncrementer` function defines a nested function called `incrementer`, which performs the actual incrementing. This function simply adds `amount` to `runningTotal`, and returns the result.*

*When considered in isolation, the nested `incrementer()` function might seem unusual:*

```swift
func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
}
```

*The `incrementer()` function doesn’t have any parameters, and yet it refers to `runningTotal` and `amount` from within its function body. It does this by capturing a reference to `runningTotal` and `amount` from the surrounding function and using them within its own function body. Capturing by reference ensures that `runningTotal` and `amount` don’t disappear when the call to `makeIncrementer` ends, and also ensures that `runningTotal` is available the next time the `incrementer` function is called.*

> *NOTE*
> 
> *As an optimization, Swift may instead capture and store a copy of a value if that value isn’t mutated by a closure, and if the value isn’t mutated after the closure is created.*
> 
> *Swift also handles all memory management involved in disposing of variables when they’re no longer needed.*

*Here’s an example of `makeIncrementer` in action:*

```swift
let incrementByTen = makeIncrementer(forIncrement: 10)
```

*This example sets a constant called `incrementByTen` to refer to an incrementer function that adds `10` to its `runningTotal` variable each time it’s called. Calling the function multiple times shows this behavior in action:*

```swift
incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
```

*If you create a second incrementer, it will have its own stored reference to a new, separate `runningTotal` variable:*

```swift
let incrementBySeven = makeIncrementer(forIncrement: 7)
incrementBySeven()
// returns a value of 7
```

*Calling the original incrementer (`incrementByTen`) again continues to increment its own `runningTotal` variable, and doesn’t affect the variable captured by `incrementBySeven`:*

```swift
incrementByTen()
// returns a value of 40
```

> *NOTE*
> 
> *If you assign a closure to a property of a class instance, and the closure captures that instance by referring to the instance or its members, you will create a strong reference cycle between the closure and the instance. Swift uses capture lists to break these strong reference cycles. For more information, see [Strong Reference Cycles for Closures](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID56).*
