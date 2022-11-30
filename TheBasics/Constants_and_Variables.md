## *Constants and Variables* : 상수와 변수

*Constants and variables associate a name (such as `maximumNumberOfLoginAttempts` or `welcomeMessage`) with a value of a particular type (such as the number `10` or the string `"Hello"`). The value of a constant can’t be changed once it’s set, whereas a variable can be set to a different value in the future.*

상수 및 변수는 이름 (`maximumNumberOfLoginAttempts` 혹은 `welcomeMessage` 같은) 을 특정한 유형의 값 (숫자 10이나 "Hello")과 연결합니다. 상수 값은 한번 설정되면 바꿀 수 없지만 변수는 나중에 다른 값으로 설정할 수 있습니다.

 

### Declaring Constants and Variables : 상수 및 변수 선언

*Constants and variables must be declared before they’re used. You declare constants with the `let` keyword and variables with the `var` keyword. Here’s an example of how constants and variables can be used to track the number of login attempts a user has made:*

상수와 변수는 반드시 사용되기 전에 선언해야 합니다. 상수는 `let` 키워드로 선언하고 변수는 `var` 키워드로 선언합니다. 다음은 사용자가 로긍니을 시도한 횟수를 추적하는데 상수와 변수를 사용하는 방법에 대한 예시입니다.

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

*This code can be read as:*

*“Declare a new constant called `maximumNumberOfLoginAttempts`, and give it a value of `10`. Then, declare a new variable called `currentLoginAttempt`, and give it an initial value of `0`.”*

이 코드는 이렇게 읽힐겁니다: 

"`maximumNumberOfLoginAttempts` 라는 새로운 상수를 선언하고, 10이라는 값을 할당한다. 그리고 나서, `currentLoginAttempt`라는 변수를 선언하고 초깃값으로 0을 할당한다."



*In this example, the maximum number of allowed login attempts is declared as a constant, because the maximum value never changes. The current login attempt counter is declared as a variable, because this value must be incremented after each failed login attempt.*

이 예시에서, 최대값은 절대 바뀌지 않기 때문에 로그인 최대 시도 횟수는 상수로 선언되었습니다. 최근 로그인 시도 카운터 값은 반드시 로그인 시도가 실패할 때마다 증가해야 하기 때문에 변수로 선언되었습니다.



*You can declare multiple constants or multiple variables on a single line, separated by commas:*

여러개의 상수나 변수를 한 줄에 쉼표로 분기하여 선언할 수 있습니다.

```swift
var x = 0.0, y = 0.0, z = 0.0
```

> *NOTE*
> 
> *If a stored value in your code won’t change, always declare it as a constant with the `let` keyword. Use variables only for storing values that need to be able to change.*
> 
> 코드에 저장된 값이 바뀌지 않는다면 항상 `let` 키워드로 상수를 선언하세요. 변수는 저장된 값이 변할 수 있는 경우에만 사용하세요.

### *Type Annotations*

*You can provide a type annotation when you declare a constant or variable, to be clear about the kind of values the constant or variable can store. Write a type annotation by placing a colon after the constant or variable name, followed by a space, followed by the name of the type to use.*

*This example provides a type annotation for a variable called `welcomeMessage`, to indicate that the variable can store `String` values:*

```swift
var welcomeMessage: String
```

*The colon in the declaration means “…of type…,” so the code above can be read as:*

*“Declare a variable called `welcomeMessage` that’s of type `String`.”*

*The phrase “of type `String`” means “can store any `String` value.” Think of it as meaning “the type of thing” (or “the kind of thing”) that can be stored.*

*The `welcomeMessage` variable can now be set to any string value without error:*

```swift
welcomeMessage = "Hello"
```

*You can define multiple related variables of the same type on a single line, separated by commas, with a single type annotation after the final variable name:*

```swift
var red, green, blue: Double
```

> *NOTE*
> 
> *It’s rare that you need to write type annotations in practice. If you provide an initial value for a constant or variable at the point that it’s defined, Swift can almost always infer the type to be used for that constant or variable, as described in [Type Safety and Type Inference](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID322). In the `welcomeMessage` example above, no initial value is provided, and so the type of the `welcomeMessage` variable is specified with a type annotation rather than being inferre from an initial value.*

### *Naming Constants and Variables*

*Constant and variable names can contain almost any character, including Unicode characters : *

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

*Constant and variable names can’t contain whitespace characters, mathematical symbols, arrows, private-use Unicode scalar values, or line- and box-drawing characters. Nor can they begin with a number, although numbers may be included elsewhere within the name.*

*Once you’ve declared a constant or variable of a certain type, you can’t declare it again with the same name, or change it to store values of a different type. Nor can you change a constant into a variable or a variable into a constant.*

> *NOTE*
> 
> *If you need to give a constant or variable the same name as a reserved Swift keyword, surround the keyword with backticks (`` ` ``) when using it as a name. However, avoid using keywords as names unless you have absolutely no choice.*

*You can change the value of an existing variable to another value of a compatible type. In this example, the value of `friendlyWelcome` is changed from `"Hello!"` to `"Bonjour!"`:*

```swift
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
```

*Unlike a variable, the value of a constant can’t be changed after it’s set. Attempting to do so is reported as an error when your code is compiled:*

```swift
let languageName = "Swift"
languageName = "Swift++"
// This is a compile-time error: languageName cannot be changed.
```

### *Printing Constants and Variables*

*You can print the current value of a constant or variable with the `print(_:separator:terminator:)` function:*

```swift
print(friendlyWelcome)
// Prints "Bonjour!"
```

T*he `print(_:separator:terminator:)` function is a global function that prints one or more values to an appropriate output. In Xcode, for example, the `print(_:separator:terminator:)` function prints its output in Xcode’s “console” pane. The `separator` and `terminator` parameter have default values, so you can omit them when you call this function. By default, the function terminates the line it prints by adding a line break. To print a value without a line break after it, pass an empty string as the terminator—for example, `print(someValue, terminator: "")`. For information about parameters with default values, see [Default Parameter Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID169).*

*Swift uses string interpolation to include the name of a constant or variable as a placeholder in a longer string, and to prompt Swift to replace it with the current value of that constant or variable. Wrap the name in parentheses and escape it with a backslash before the opening parenthesis:*

```swift
print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Prints "The current value of friendlyWelcome is Bonjour!"
```

> *NOTE*
> 
> *All options you can use with string interpolation are described in [String Interpolation](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html#ID292).*
