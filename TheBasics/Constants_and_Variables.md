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

### *Type Annotations : 타입 어노테이션*

*You can provide a type annotation when you declare a constant or variable, to be clear about the kind of values the constant or variable can store. Write a type annotation by placing a colon after the constant or variable name, followed by a space, followed by the name of the type to use.*

상수 혹은 변수가 저장될 값의 종류를 명확히 하기 위해 상수와 변수를 선언할 때 타입 어노테이션을 제공할 수 있습니다. 상수 또는 변수 이름 뒤에 콜론과 공백을 적어 사용할 유형의 이름을 입력합니다.



*This example provides a type annotation for a variable called `welcomeMessage`, to indicate that the variable can store `String` values:*

이 예시는 `welcomMessage`라는 변수에 타입 어노테이션을 제공하여 변수가 String 값을 저장할 수 있음을 나타내는 경우입니다 :

```swift
var welcomeMessage: String
```

*The colon in the declaration means “…of type…,” so the code above can be read as:*

선언문에서 콜론의 의미는 "..타입.." 이므로 위의 코드는 아래와 같이 읽을 수 있습니다.



*“Declare a variable called `welcomeMessage` that’s of type `String`.”*

"String 타입의 `welcomMessage` 라는 변수를 선언한다."



*The phrase “of type `String`” means “can store any `String` value.” Think of it as meaning “the type of thing” (or “the kind of thing”) that can be stored.*

“of type `String`” 이라는 문구의 의미는 "어떠한 `String` 값도 저장할 수 있다. " 입니다. 저장할 수 있는 "것의 종류"를 의미한다고 생각하면 됩니다.



*The `welcomeMessage` variable can now be set to any string value without error:*

이제 `welcomeMessage` 변수를 오류 없이 문자열 값으로 설정할 수 있습니다.

```swift
welcomeMessage = "Hello"
```



*You can define multiple related variables of the same type on a single line, separated by commas, with a single type annotation after the final variable name:*

콤마로 구분된 동일한 유형의 관련된 변수를 한 줄에 여러개 정의할 수 있으며, 최종 변수 이름 뒤에 단일 유형의 주석을 사용할 수 있습니다.

```swift
var red, green, blue: Double
```

> *NOTE*
> 
> *It’s rare that you need to write type annotations in practice. If you provide an initial value for a constant or variable at the point that it’s defined, Swift can almost always infer the type to be used for that constant or variable, as described in [Type Safety and Type Inference](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID322). In the `welcomeMessage` example above, no initial value is provided, and so the type of the `welcomeMessage` variable is specified with a type annotation rather than being inferre from an initial value.*
> 
> 타입 어노테이션을 실제로 작성해야 하는 경우는 거의 없습니다. 정의된 지점에서 상수 혹은 변수의 초기값을 제공하는 경우 Swift는 (링크)에 설명된 대로 거의 항상 해당 상수 혹은 변수에 사용할 유형을 추론할 수 있습니다. 위의 예제에서는 초기 값이 제공되지 않으므로 해당 변수의 유형은 초기값에서 추론되지 않고 타입 어노테이션으로 지정됩니다.



### *Naming Constants and Variables : 변수와 상수 네이밍*

*Constant and variable names can contain almost any character, including Unicode characters :*

상수와 변수명은 유니코드 문자를 포함해 대부분의 문자를 포함할 수 있습니다. 

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

*Constant and variable names can’t contain whitespace characters, mathematical symbols, arrows, private-use Unicode scalar values, or line- and box-drawing characters. Nor can they begin with a number, although numbers may be included elsewhere within the name.*

상수와 변수명은 공백 문자, 수학 기호, 화살표, 유니코드 스칼라값 혹은 줄 및 상자 그리기 문자를 표현할 수 없습니다. 뿐만아니라 숫자가 이름의 다른 부분에 포함될 수는 있지만 숫자로 시작할 수는 없습니다.



*Once you’ve declared a constant or variable of a certain type, you can’t declare it again with the same name, or change it to store values of a different type. Nor can you change a constant into a variable or a variable into a constant.*

특정 유형의 상수 혹은 변수를 선언한 후에는 동일한 이름으로 다시 선언하거나 다른 유형의 값을 저장하도록 변경할 수 없습니다. 뿐만아니라 변수를 상수로 변경하거나 상수를 변수로 변경할 수도 없습니다.



> *NOTE*
> 
> *If you need to give a constant or variable the same name as a reserved Swift keyword, surround the keyword with backticks (`` ` ``) when using it as a name. However, avoid using keywords as names unless you have absolutely no choice.*
> 
> 만약 상수나 변수명을 Swift 예약어로 사용해야 할 경우 백틱으로 키워드를 감싸줍니다. 그러나, 명백히 다른 선택지가 없지 않는 한 예약어를 이름으로 사용하는 것을 피합니다.



*You can change the value of an existing variable to another value of a compatible type. In this example, the value of `friendlyWelcome` is changed from `"Hello!"` to `"Bonjour!"`:*

기존 변수의 값을 호환되는 유형으로 변경할 수 있습니다. 아래의 예시에서 `friendlyWelcome`의 값은 `Hello!` 에서 `Bonjour!` 로 변경되었습니다.

```swift
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
```

*Unlike a variable, the value of a constant can’t be changed after it’s set. Attempting to do so is reported as an error when your code is compiled:*

변수와는 다르게, 상수의 값은 셋팅된 이후 변경될 수 없습니다. 변경을 시도하면 코드가 컴파일 될 때 에러로 인식됩니다.

```swift
let languageName = "Swift"
languageName = "Swift++"
// This is a compile-time error: languageName cannot be changed.
```

### *Printing Constants and Variables : 상수와 변수를 출력하기*

*You can print the current value of a constant or variable with the `print(_:separator:terminator:)` function:*

`print(_:separator:terminator:)` 함수를 사용하여 상수 혹은 변수의 현재 값을 출력할 수 있습니다.

```swift
print(friendlyWelcome)
// Prints "Bonjour!"
```

T*he `print(_:separator:terminator:)` function is a global function that prints one or more values to an appropriate output. In Xcode, for example, the `print(_:separator:terminator:)` function prints its output in Xcode’s “console” pane. The `separator` and `terminator` parameter have default values, so you can omit them when you call this function. By default, the function terminates the line it prints by adding a line break. To print a value without a line break after it, pass an empty string as the terminator—for example, `print(someValue, terminator: "")`. For information about parameters with default values, see [Default Parameter Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID169).*

`print(_:separator:terminator:)` 함수는 하나 혹은 여러개의 값을 적절한 결과물로 출력하는 전역 함수입니다. 예를 들면 Xcode 에서는  `print(_:separator:terminator:)` 함수는 Xcode의 Console창에 출력합니다. `separator` 와 `terminator`매개변수에는 기본값이 있으므로 이 함수를 호출할 때 생략할 수 있습니다. 기본적으로 함수는 줄바꿈을 추가해서 인쇄를 종료합니다. 줄 바꿈 없이 값을 인쇄하려면 빈 문자열을 종결자로 전달합니다. (예를 들면,  `print(someValue, terminator: "")`.) 기본값이 있는 매개변수에 대한 자세한 내용은 (링크) 를 참조하세요.



*Swift uses string interpolation to include the name of a constant or variable as a placeholder in a longer string, and to prompt Swift to replace it with the current value of that constant or variable. Wrap the name in parentheses and escape it with a backslash before the opening parenthesis:*

Swift는 문자열 보간법을 사용하여 더 긴 문자열에 placeholder로 상수 혹은 변수 이름을 포함하고, Swift가 해당 상수 혹은 변수의 현재 값으로 바꾸도록 요청합니다. 이름을 괄호로 묶고 괄호 앞에 백슬래쉬를 사용하여 탈출합니다. 

```swift
print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Prints "The current value of friendlyWelcome is Bonjour!"
```

> *NOTE*
> 
> *All options you can use with string interpolation are described in [String Interpolation](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html#ID292).*
> 
> 문자열 보간과 함께 사용할 수 있는 모든 옵션은 (링크) 에 설명되어 있습니다.
