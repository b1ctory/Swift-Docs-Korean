## *Autoclosures : 자동클로저*

*An autoclosure is a closure that’s automatically created to wrap an expression that’s being passed as an argument to a function. It doesn’t take any arguments, and when it’s called, it returns the value of the expression that’s wrapped inside of it. This syntactic convenience lets you omit braces around a function’s parameter by writing a normal expression instead of an explicit closure.*

자동클로저는 함수에 인수로 전달되는 식을 감싸기 위해 자동으로 생성되는 클로저입니다. 인수를 사용하지 않으며, 인수를 호출할 때 내부에 감싸진 표현식의 값을 반환합니다. 이 구문을 사용하면 명시적 클로저 대신 정규식을 작성해서 함수 매개변수 주변에 대괄호를 생략할 수 있습니다.

*It’s common to call functions that take autoclosures, but it’s not common to implement that kind of function. For example, the `assert(condition:message:file:line:)` function takes an autoclosure for its `condition` and `message` parameters; its `condition` parameter is evaluated only in debug builds and its `message` parameter is evaluated only if `condition` is `false`.*

자동 클로저를 취하는 함수를 호출하는 것은 일반적이지만, 그런 함수를 구현하는 것은 일반적이지 않습니다. 예를 들어, `assert(condition:message:file:line:)` 함수는 `condition`과 `message` 매개변수는 `condition`이 `false`인 경우에만 평가됩니다.

*An autoclosure lets you delay evaluation, because the code inside isn’t run until you call the closure. Delaying evaluation is useful for code that has side effects or is computationally expensive, because it lets you control when that code is evaluated. The code below shows how a closure delays evaluation.*

자동클로저를 사용하면 내부 코드가 클로저를 호출할 때까지 실행되지 않으므로 평가를 지연시킬 수 있습니다. 평가 지연은 코드가 평가되는 시기를 제어할 수 있기 때문에 부작용이 있거나 계산 비용이 많이 드는 코드에 유용합니다. 아래 코드는 클로저가 평가를 지연시키는 방법을 보여줍니다.

```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
print(customersInLine.count)
// Prints "5"

let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
// Prints "5"

print("Now serving \(customerProvider())!")
// Prints "Now serving Chris!"
print(customersInLine.count)
// Prints "4"
```

*Even though the first element of the `customersInLine` array is removed by the code inside the closure, the array element isn’t removed until the closure is actually called. If the closure is never called, the expression inside the closure is never evaluated, which means the array element is never removed. Note that the type of `customerProvider` isn’t `String` but `() -> String`—a function with no parameters that returns a string.*

`customersInLine`의 첫번째 요소임에도 불구하고 배열은 클로저 내부 코드에 의해 제거되며, 클로저가 실제로 호출될 때까지 배열  요소는 제거되지 않습니다. 클로저를 호출하지 않으면 클로저 내부의 식을 계산하지 않으므로 배열 요소가 절대 제거되지 않습니다. `customerProvider`의 타입은 문자열을 반환하는 매개변수가 없는 함수인 `String`이 아니라 `() -> String`입니다.

*You get the same behavior of delayed evaluation when you pass a closure as an argument to a function.*

클로저를 함수에 인수로 전달할 때도 평가 지연과 동일한 동작이 발생합니다.

```swift
// customersInLine is ["Alex", "Ewa", "Barry", "Daniella"]
func serve(customer customerProvider: () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: { customersInLine.remove(at: 0) } )
// Prints "Now serving Alex!"
```

*The `serve(customer:)` function in the listing above takes an explicit closure that returns a customer’s name. The version of `serve(customer:)` below performs the same operation but, instead of taking an explicit closure, it takes an autoclosure by marking its parameter’s type with the `@autoclosure` attribute. Now you can call the function as if it took a `String` argument instead of a closure. The argument is automatically converted to a closure, because the `customerProvider` parameter’s type is marked with the `@autoclosure` attribute.*

위 목록의 `serve(customer:)` 함수는 고객의 이름을 반환하는 명시적인 클로저를 취합니다. 아래의 `serve(customer:)` 버전은 동일한 작업을 수행하지만 명시적 클로저를 취하는 대신 매개변수의 타입을 `@autoclosure` 속성으로 표시해서 자동클로저를 수행합니다. 이제 클로저 대신 `String` 인수를 사용한 것처럼 함수를 호출할 수 있습니다. `customerProvider` 매개변수의 타입이 `@autoclosure` 특성으로 표시되므로 인수는 자동으로 클로저로 변환됩니다.

```swift
// customersInLine is ["Ewa", "Barry", "Daniella"]
func serve(customer customerProvider: @autoclosure () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: customersInLine.remove(at: 0))
// Prints "Now serving Ewa!"
```

> *NOTE*
> 
> *Overusing autoclosures can make your code hard to understand. The context and function name should make it clear that evaluation is being deferred.*
> 
> 자동클로저를 과도하게 사용하면 코드를 이해하기 어려울 수 있습니다. 컨텍스트 및 함수 이름은 평가가 지연되고 있음을 분명히 해야 합니다.

*If you want an autoclosure that’s allowed to escape, use both the `@autoclosure` and `@escaping` attributes. The `@escaping` attribute is described above in [Escaping Closures](https://docs.swift.org/swift-book/LanguageGuide/Closures.html#ID546).*

탈출을 허용하는 자동클로저를 원할 경우 `@autoclosure` 과 `@escaping` 속성을 모두 사용하세요. `@escaping` 속성에 대한 설명은 [링크]에 설명되어 있습니다.

```swift
// customersInLine is ["Barry", "Daniella"]
var customerProviders: [() -> String] = []
func collectCustomerProviders(_ customerProvider: @autoclosure @escaping () -> String) {
    customerProviders.append(customerProvider)
}
collectCustomerProviders(customersInLine.remove(at: 0))
collectCustomerProviders(customersInLine.remove(at: 0))

print("Collected \(customerProviders.count) closures.")
// Prints "Collected 2 closures."
for customerProvider in customerProviders {
    print("Now serving \(customerProvider())!")
}
// Prints "Now serving Barry!"
// Prints "Now serving Daniella!"
```

*In the code above, instead of calling the closure passed to it as its `customerProvider` argument, the `collectCustomerProviders(_:)` function appends the closure to the `customerProviders` array. The array is declared outside the scope of the function, which means the closures in the array can be executed after the function returns. As a result, the value of the `customerProvider` argument must be allowed to escape the function’s scope.*

위의 코드에서 전달된 클로저를 `customerProvider` 인수로 부르는 대신 `collectCustomerProviders(_:)` 함수는 클로저를 `customerProviders` 배열에 추가합니다. 배열이 함수 밖에서 선언되고, 함수가 반환된 후 배열에서 클로저를 실행할 수 있습니다. 즉, 함수가 반환된 후에 배열에서 클로저를 실행할 수 있습니다. 따라서 함수의 범위를 벗어나려면 `customerProvider` 인수 값이 허용되어야 합니다.
