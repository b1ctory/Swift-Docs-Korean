## *Early Exit : 조기 종료*

*A `guard` statement, like an `if` statement, executes statements depending on the Boolean value of an expression. You use a `guard` statement to require that a condition must be true in order for the code after the `guard` statement to be executed. Unlike an `if` statement, a `guard` statement always has an `else` clause—the code inside the `else` clause is executed if the condition isn’t true.*

`guard` 문은, if문과 마찬가지로 식의 Boolean 값에 따라 구문을 실행합니다. `guard`문을 사용하면 `guard`문 다음에 코드가 실행되려면 조건이 참이어야 합니다. `guard` 문은 `if`문과 달리 항상 `else` 절을 가지고 있는데, `else` 절 안의 코드는 조건이 참이 아닐 때 실행됩니다.

```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }

    print("Hello \(name)!")

    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }

    print("I hope the weather is nice in \(location).")
}

greet(person: ["name": "John"])
// Prints "Hello John!"
// Prints "I hope the weather is nice near you."
greet(person: ["name": "Jane", "location": "Cupertino"])
// Prints "Hello Jane!"
// Prints "I hope the weather is nice in Cupertino."
```

*If the `guard` statement’s condition is met, code execution continues after the `guard` statement’s closing brace. Any variables or constants that were assigned values using an optional binding as part of the condition are available for the rest of the code block that the `guard` statement appears in.*

`guard` 구문의 조건이 충족되면 `guard` 구문의 닫힘 괄호 후에도 코드 실행이 계속됩니다. 조건의 일부로 옵셔널 바인딩을 사용해서 값이 할당된 변수 혹은 상수는 `guard` 구문이 나타나는 나머지 코드 블록에 사용할 수 있습니다.

*If that condition isn’t met, the code inside the `else` branch is executed. That branch must transfer control to exit the code block in which the `guard` statement appears. It can do this with a control transfer statement such as `return`, `break`, `continue`, or `throw`, or it can call a function or method that doesn’t return, such as `fatalError(_:file:line:)`.*

이 조건이 충족되지 않으면 `else` 분기 내의 코드가 실행됩니다. 해당 분기는 `guard` 문이 나타나는 코드 블록을 종료하려면 제어를 전송해야만 합니다. 이는 `return`, `break`, `continue`, 혹은 `throw`와 같은 제어 전송 문을 사용하거나 `fatalError(_:file:line:)`와 같이 반환되지 않는 함수 혹은 메서드를 호출할 수 있습니다.

*Using a `guard` statement for requirements improves the readability of your code, compared to doing the same check with an `if` statement. It lets you write the code that’s typically executed without wrapping it in an `else` block, and it lets you keep the code that handles a violated requirement next to the requirement.*

요구사항에 `guard` 구문을 사용하면 `if` 문으로 동일한 검사를 수행하는 것에 비해 코드의 가독성이 향상됩니다. 일반적으로 실행되는 코드를 `else` 블록으로 래핑하지 않고 작성할 수 있으며 위반된 요구사항을 처리하는 코드를 요구사항을 처리하는 코드를 요구사항 옆에 보관할 수 있습니다.
