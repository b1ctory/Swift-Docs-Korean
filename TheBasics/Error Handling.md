## *Error Handling : 오류 처리*

*You use error handling to respond to error conditions your program may encounter during execution.*

오류 처리를 사용하여 프로그램 실행 중에 발생할 수 있는 오류 조건에 대응할 수 있습니다. 

*In contrast to optionals, which can use the presence or absence of a value to communicate success or failure of a function, error handling allows you to determine the underlying cause of failure, and, if necessary, propagate the error to another part of your program.*

값의 유무를 사용하여 함수의 성공 혹은 실패를 전달할 수 있는 옵셔널과 달리 오류 처리를 사용하면 오류의 근본 원인을 파악하고 필요한 경우 프로그램의 다른 부분으로 오류를 전파할 수 있습니다.

*When a function encounters an error condition, it throws an error. That function’s caller can then catch the error and respond appropriately.*

함수에 오류 조건이 발생하면 오류가 발생합니다. 그러면 해당 기능의 호출자가 오류를 감지하고 적절하게 응답할 수 있습니다. 

```swift
func canThrowAnError() throws {
    // this function may or may not throw an error
}
```

*A function indicates that it can throw an error by including the `throws` keyword in its declaration. When you call a function that can throw an error, you prepend the `try` keyword to the expression.*

함수는 선언문에 throws 키워드를 퐇마시켜 오류를 발생시킬 수 있음을 나타냅니다. 오류를 발생시킬 수 있는 함수를 호출할 때는 표현식에 try 키워드를 추가합니다.

*Swift automatically propagates errors out of their current scope until they’re handled by a `catch` clause.*

스위프트는 catch 문에 의해 처리될 때까지 현재 범위를 벗어난 오류를 자동으로 전파합니다.

```swift
do {
    try canThrowAnError()
    // no error was thrown
} catch {
    // an error was thrown
}
```

*A `do` statement creates a new containing scope, which allows errors to be propagated to one or more `catch` clauses.*

do 문은 하나 이상의 catch 절에 오류를 전파할 수 있는 새로운 포함 범위를 생성합니다.

*Here’s an example of how error handling can be used to respond to different error conditions:*

다음은 다양한 오류 조건에 대응하기 위해 오류 처리를 사용하는 방법에 대한 예시입니다.

```swift
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

*In this example, the `makeASandwich()` function will throw an error if no clean dishes are available or if any ingredients are missing. Because `makeASandwich()` can throw an error, the function call is wrapped in a `try` expression. By wrapping the function call in a `do` statement, any errors that are thrown will be propagated to the provided `catch` clauses.*

이 예시에서 makeSandwitch() 메소드는 깨끗한 접시가 없거나 재료가 누락된 경우 오류를 발생시킵니다. makeSandwich() 메소드는 오류를 발생시킬 수 있으므로 함수 호출은 try 표현으로 감싸집니다. 함수 호출을 do 문으로 감싸서 어떤 에러든 제공된 catch 절로 전파됩니다.

*If no error is thrown, the `eatASandwich()` function is called. If an error is thrown and it matches the `SandwichError.outOfCleanDishes` case, then the `washDishes()` function will be called. If an error is thrown and it matches the `SandwichError.missingIngredients` case, then the `buyGroceries(_:)` function is called with the associated `[String]` value captured by the `catch` pattern.*

오류가 발생하지 않으면 eatSandwich() 메소드가 호출됩니다. 오류가 발생해서 `SandwichError.outOfCleanDishes` 케이스와 일치하면, `buyGroceries(_:)` 메소드가 catch 패턴에 의해 캡쳐된 관련 [String] 값과 함께 호출됩니다. 

*Throwing, catching, and propagating errors is covered in greater detail in [Error Handling](https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html).*

Throwing, catching, 그리고 propagating하는 오류는 다음 [링크]에서 더 자세히 다뤄집니다.

(Throwing - 던짐 / catching - 잡아냄 / propagating - 전파함)




