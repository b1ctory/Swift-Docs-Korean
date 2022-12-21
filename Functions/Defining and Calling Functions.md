## *Defining and Calling Functions*

*When you define a function, you can optionally define one or more named, typed values that the function takes as input, known as parameters. You can also optionally define a type of value that the function will pass back as output when it’s done, known as its return type.*

*Every function has a function name, which describes the task that the function performs. To use a function, you “call” that function with its name and pass it input values (known as arguments) that match the types of the function’s parameters. A function’s arguments must always be provided in the same order as the function’s parameter list.*

*The function in the example below is called `greet(person:)`, because that’s what it does—it takes a person’s name as input and returns a greeting for that person. To accomplish this, you define one input parameter—a `String` value called `person`—and a return type of `String`, which will contain a greeting for that person:*

```swift
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}
```

*All of this information is rolled up into the function’s definition, which is prefixed with the `func` keyword. You indicate the function’s return type with the return arrow `->` (a hyphen followed by a right angle bracket), which is followed by the name of the type to return.*

*The definition describes what the function does, what it expects to receive, and what it returns when it’s done. The definition makes it easy for the function to be called unambiguously from elsewhere in your code:*

```swift
print(greet(person: "Anna"))
// Prints "Hello, Anna!"
print(greet(person: "Brian"))
// Prints "Hello, Brian!"
```

*You call the `greet(person:)` function by passing it a `String` value after the `person` argument label, such as `greet(person: "Anna")`. Because the function returns a `String` value, `greet(person:)` can be wrapped in a call to the `print(_:separator:terminator:)` function to print that string and see its return value, as shown above.*

> *NOTE*
> 
> *The `print(_:separator:terminator:)` function doesn’t have a label for its first argument, and its other arguments are optional because they have a default value. These variations on function syntax are discussed below in [Function Argument Labels and Parameter Names](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID166) and [Default Parameter Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID169).*

*The body of the `greet(person:)` function starts by defining a new `String` constant called `greeting` and setting it to a simple greeting message. This greeting is then passed back out of the function using the `return` keyword. In the line of code that says `return greeting`, the function finishes its execution and returns the current value of `greeting`.*

*You can call the `greet(person:)` function multiple times with different input values. The example above shows what happens if it’s called with an input value of `"Anna"`, and an input value of `"Brian"`. The function returns a tailored greeting in each case.*

*To make the body of this function shorter, you can combine the message creation and the return statement into one line:*

```swift
func greetAgain(person: String) -> String {
    return "Hello again, " + person + "!"
}
print(greetAgain(person: "Anna"))
// Prints "Hello again, Anna!"
```


