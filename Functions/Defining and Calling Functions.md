## *Defining and Calling Functions : 함수 정의 및 호출*

*When you define a function, you can optionally define one or more named, typed values that the function takes as input, known as parameters. You can also optionally define a type of value that the function will pass back as output when it’s done, known as its return type.*

함수를 정의할 떄 선택적으로 함수가 매개변수라고 하는 입력으로 사용하는 이름이 지정되고 타입이 지정된 값을 하나 이상 정의할 수 있습니다. 또한 선택적으로 함수가 완료될 때 출력으로 전달할 값의 타입 (반환 타입이라고도 하는)을 정의할 수도 있습니다.

*Every function has a function name, which describes the task that the function performs. To use a function, you “call” that function with its name and pass it input values (known as arguments) that match the types of the function’s parameters. A function’s arguments must always be provided in the same order as the function’s parameter list.*

모든 함수에는 기능이 수행하는 작업을 설명하는 함수 이름이 있습니다. 함수를 사용하려면 함수 이름으로 함수를 호출하고 함수 매개변수 타입과 일치하는 입력값 (인수)를 전달합니다. 함수의 인수는 함수의 매개변수 목록과 같은 순서로 제공되어야 합니다.

*The function in the example below is called `greet(person:)`, because that’s what it does—it takes a person’s name as input and returns a greeting for that person. To accomplish this, you define one input parameter—a `String` value called `person`—and a return type of `String`, which will contain a greeting for that person:*

아래 예제의 함수를 `greet(person:)`이라고 하는데, 이 함수는 사용자의 이름을 입력으로 사용해서 해당 사용자에게 인사말을 반환하기 때문입니다. 이를 수행하려면 하나의 입력 매개 변수 (`person` 이라고 불리는 `String` 값)와 해당 사용자에 대한 인사말을 포함하는 `String`의 반환 타입을 정의합니다.

```swift
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}
```

*All of this information is rolled up into the function’s definition, which is prefixed with the `func` keyword. You indicate the function’s return type with the return arrow `->` (a hyphen followed by a right angle bracket), which is followed by the name of the type to return.*

이 모든 정보는 func 키워드가 앞에 붙은 함수의 정의로 롤업됩니다. 함수의 반환 타입을 반환 화살표 `->` (하이픈 뒤에 오른쪽 각도 괄호가 있습니다.)로 표시하고 반환할 타입의 이름을 입력합니다.

*The definition describes what the function does, what it expects to receive, and what it returns when it’s done. The definition makes it easy for the function to be called unambiguously from elsewhere in your code:*

정의는 함수가 수행하는 작업 및 완료시 반환되는 작업을 설명합니다. 이 정의를 사용하면 코드의 다른 위치에서 함수를 쉽게 호출할 수 있습니다.

```swift
print(greet(person: "Anna"))
// Prints "Hello, Anna!"
print(greet(person: "Brian"))
// Prints "Hello, Brian!"
```

*You call the `greet(person:)` function by passing it a `String` value after the `person` argument label, such as `greet(person: "Anna")`. Because the function returns a `String` value, `greet(person:)` can be wrapped in a call to the `print(_:separator:terminator:)` function to print that string and see its return value, as shown above.*

`greet(person:)` 함수는 `greet(person: "Anna")`와 같이 person 인수 레이블 뒤에 `String` 값을 전달합니다. 함수가 `String` 값을 반환하기 때문에, 위와 같이  `greet(person:)`을 `print(_:separator:terminator:)` 함수에 호출해서 해당 문자열을 인쇄하고 반환 값을 확인할 수 있습니다.

> *NOTE*
> 
> *The `print(_:separator:terminator:)` function doesn’t have a label for its first argument, and its other arguments are optional because they have a default value. These variations on function syntax are discussed below in [Function Argument Labels and Parameter Names](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID166) and [Default Parameter Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID169).*
> 
>  `print(_:separator:terminator:)` 함수에는 첫번째 인수에 대한 레이블이 없으며 다른 인수에는 기본값이 있으므로 해당 인수는 선택 사항입니다. 함수 구문에 대한 이러한 변형은 [링크] 및 [링크]에서 설명합니다.

*The body of the `greet(person:)` function starts by defining a new `String` constant called `greeting` and setting it to a simple greeting message. This greeting is then passed back out of the function using the `return` keyword. In the line of code that says `return greeting`, the function finishes its execution and returns the current value of `greeting`.*

`greet(person:)` 함수의 본문은 `greeting`이라는 새로운 `String` 상수를 정의하고 간단한 `greeting` 메세지로 설정하는 것으로 시작합니다. 그런 다음 이 인사말은 `return` 키워드를 사용해서 함수에서 다시 전달됩니다. `return greeting` 이라는 코드 행에서 이 함수는 실행을 마치고 `greeting`의 현재 값을 반환합니다.

*You can call the `greet(person:)` function multiple times with different input values. The example above shows what happens if it’s called with an input value of `"Anna"`, and an input value of `"Brian"`. The function returns a tailored greeting in each case.*

다른 입력 값으로 `greet(person:)` 함수를 여러번 호출할 수 있습니다. 위의 예는 입력값 `"Anna"`와 입력값 `Brian`으로 호출되면 어떻게 되는지 보여줍니다. 함수는 각 경우에 사용자 지정된 인사말을 반환합니다.

*To make the body of this function shorter, you can combine the message creation and the return statement into one line:*

이 기능의 본문을 더 짧게 만들기 위해 메세지 작성과 반환문을 한 줄로 묶을 수 있습니다.

```swift
func greetAgain(person: String) -> String {
    return "Hello again, " + person + "!"
}
print(greetAgain(person: "Anna"))
// Prints "Hello again, Anna!"
```
