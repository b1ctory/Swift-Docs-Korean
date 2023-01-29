## *Handling Errors: 에러 핸들링*

*When an error is thrown, some surrounding piece of code must be responsible for handling the error—for example, by correcting the problem, trying an alternative approach, or informing the user of the failure.*

오류가 발생하면 주변 코드가 오류 처리를 담당해야 합니다. 예를 들어 문제를 수정하거나 다른 방법을 시도하거나 사용자에게 오류를 알려줍니다.

*There are four ways to handle errors in Swift. You can propagate the error from a function to the code that calls that function, handle the error using a `do`-`catch` statement, handle the error as an optional value, or assert that the error will not occur. Each approach is described in a section below.*

Swift는 4가지 오류 처리 방법이 있습니다. 함수에서 해당 함수를 호출하는 코드로 오류를 전파하거나, `do`-`catch` 문을 사용하여 오류를 처리하거나, 옵셔널 값으로 오류를 처리하거나, 오류가 발생하지 않을 것이라고 주장할 수 있습니다. 각 접근 방식은 아래 섹션에서 설명합니다.

*When a function throws an error, it changes the flow of your program, so it’s important that you can quickly identify places in your code that can throw errors. To identify these places in your code, write the `try` keyword—or the `try?` or `try!` variation—before a piece of code that calls a function, method, or initializer that can throw an error. These keywords are described in the sections below.*

함수가 오류를 발생시키면 프로그램 흐름이 변경되므로 코드에서 오류를 발생시킬 수 있는 위치를 빠르게 식별할 수 있어야 합니다. 코드에서 이러한 위치를 식별하려면 `try` 혹은 `try?` 혹은 `try!` 키워드를 쓰세요.—오류를 발생시킬 수 있는 함수, 메서드 또는 이니셜라이저를 호출하는 코드 앞에 있습니다. 이러한 키워드는 아래 절에 설명되어 있습니다

> *NOTE*
> 
> *Error handling in Swift resembles exception handling in other languages, with the use of the `try`, `catch` and `throw` keywords. Unlike exception handling in many languages—including Objective-C—error handling in Swift doesn’t involve unwinding the call stack, a process that can be computationally expensive. As such, the performance characteristics of a `throw` statement are comparable to those of a `return` statement.*
> 
> 스위프트의 오류 처리는 `try`, `catch` 및 `throw` 키워드를 사용하는 다른 언어의 예외 처리와 유사합니다. Objective-C를 포함한 여러 언어의 예외 처리와 달리 Swift의 오류 처리에는 계산 비용이 많이 들 수 있는 프로세스인 호출 스택의 해제가 포함되지 않습니다. 따라서 `throw`문의 성능 특성은 `return` 문의 성능 특성과 비슷합니다.

### *Propagating Errors Using Throwing Functions : 던지기 함수를 사용해서 오류 전파*

*To indicate that a function, method, or initializer can throw an error, you write the `throws` keyword in the function’s declaration after its parameters. A function marked with `throws` is called a throwing function. If the function specifies a return type, you write the `throws` keyword before the return arrow (`->`).*

함수, 메서드 또는 이니셜라이저가 오류를 발생시킬 수 있음을 나타내려면 함수의 선언에 해당 매개변수 뒤에 `throws` 키워드를 적습니다. `throws` 표시된 함수를 throwing 함수라고 합니다. 함수가 반환 타입을 지정하는 경우 반환 화살표(`->`) 앞에 `throws` 키워드를 씁니다.

```swift
func canThrowErrors() throws -> String

func cannotThrowErrors() -> String
```

*A throwing function propagates errors that are thrown inside of it to the scope from which it’s called.*

던지기 함수는 내부에 던져진 오류를 호출된 범위로 전파합니다.

> *NOTE*
> 
> *Only throwing functions can propagate errors. Any errors thrown inside a nonthrowing function must be handled inside the function.*
> 
> 던지기 함수만 오류를 전파할 수 있습니다. 던지지 않는 함수 내부에서 발생하는 모든 오류는 함수 내부에서 처리해야 합니다.

*In the example below, the `VendingMachine` class has a `vend(itemNamed:)` method that throws an appropriate `VendingMachineError` if the requested item isn’t available, is out of stock, or has a cost that exceeds the current deposited amount:*

아래 예에서 `VendingMachine` 클래스는 요청한 항목을 사용할 수 없거나 재고가 없거나 현재 입금된 금액을 초과하는 비용이 발생할 경우 적절한 `VendingMachineError`를 발생시키는 `vend(itemName:)` 메서드를 가집니다:

```swift
struct Item {
    var price: Int
    var count: Int
}

class VendingMachine {
    var inventory = [
        "Candy Bar": Item(price: 12, count: 7),
        "Chips": Item(price: 10, count: 4),
        "Pretzels": Item(price: 7, count: 11)
    ]
    var coinsDeposited = 0

    func vend(itemNamed name: String) throws {
        guard let item = inventory[name] else {
            throw VendingMachineError.invalidSelection
        }

        guard item.count > 0 else {
            throw VendingMachineError.outOfStock
        }

        guard item.price <= coinsDeposited else {
            throw VendingMachineError.insufficientFunds(coinsNeeded: item.price - coinsDeposited)
        }

        coinsDeposited -= item.price

        var newItem = item
        newItem.count -= 1
        inventory[name] = newItem

        print("Dispensing \(name)")
    }
}
```

*The implementation of the `vend(itemNamed:)` method uses `guard` statements to exit the method early and throw appropriate errors if any of the requirements for purchasing a snack aren’t met. Because a `throw` statement immediately transfers program control, an item will be vended only if all of these requirements are met.*

`vend(itemNamed:)` 방식의 구현은 `guard` 문구를 사용하여 스낵 구매 조건 중 하나라도 충족되지 않을 경우 해당 방식을 조기에 종료하고 적절한 오류를 발생시킵니다. `throw` 구문은 프로그램 제어를 즉시 이전하기 때문에 이러한 요구 사항이 모두 충족되는 경우에만 항목이 밴딩됩니다.

*Because the `vend(itemNamed:)` method propagates any errors it throws, any code that calls this method must either handle the errors—using a `do`-`catch` statement, `try?`, or `try!`—or continue to propagate them. For example, the `buyFavoriteSnack(person:vendingMachine:)` in the example below is also a throwing function, and any errors that the `vend(itemNamed:)` method throws will propagate up to the point where the `buyFavoriteSnack(person:vendingMachine:)` function is called.*

`vend(itemNamed:)` 메서드는 모든 오류를 전파하므로 이 메서드를 호출하는 코드는 `do`-`catch` 문, `try?` 혹은 `try!`를 사용하여 오류를 처리해야 합니다.—또는 계속 전파합니다. 예를 들어 아래 예제의 `buyFavoriteSnack(person:vendingMachine:)`도 던지기 함수이며, `vend(itemName:)` 메서드가 던지는 오류는 `buyFavoriteSnack(person:vendingMachine:)` 함수가 호출될 때까지 전파됩니다.

```swift
let favoriteSnacks = [
    "Alice": "Chips",
    "Bob": "Licorice",
    "Eve": "Pretzels",
]

func buyFavoriteSnack(person: String, vendingMachine: VendingMachine) throws {
    let snackName = favoriteSnacks[person] ?? "Candy Bar"
    try vendingMachine.vend(itemNamed: snackName)
}
```

*In this example, the `buyFavoriteSnack(person: vendingMachine:)` function looks up a given person’s favorite snack and tries to buy it for them by calling the `vend(itemNamed:)` method. Because the `vend(itemNamed:)` method can throw an error, it’s called with the `try` keyword in front of it.*

이 예에서 `buyFavoriteSnack(person: vendingMachine:)`함수는 특정 사용자가 좋아하는 스낵을 검색하고 `vend(itemNamed:)` 메서드를 호출하여 해당 사용자를 위해 구입하려고 합니다. `vend(itemNamed:)` 메서드는 오류를 발생시킬 수 있으므로 `try` 키워드를 앞에 두고 호출됩니다.

*Throwing initializers can propagate errors in the same way as throwing functions. For example, the initializer for the `PurchasedSnack` structure in the listing below calls a throwing function as part of the initialization process, and it handles any errors that it encounters by propagating them to its caller.*

이니셜라이저를 던지는 것은 던지기 함수와 동일한 방식으로 오류를 전파할 수 있습니다. 예를 들어, 아래 목록의 `PurchasedSnack`구조체의 이니셜라이저는 초기화 프로세스의 일부로 던지기 함수를 호출하며, 발생하는 모든 오류를 호출자에게 전파하여 처리합니다.

```swift
struct PurchasedSnack {
    let name: String
    init(name: String, vendingMachine: VendingMachine) throws {
        try vendingMachine.vend(itemNamed: name)
        self.name = name
    }
}
```

### *Handling Errors Using Do-Catch : Do-Catch를 사용해서 오류 처리*

*You use a `do`-`catch` statement to handle errors by running a block of code. If an error is thrown by the code in the `do` clause, it’s matched against the `catch` clauses to determine which one of them can handle the error.*

코드 블록을 실행하여 오류를 처리하려면 `do`-`catch` 문을 사용합니다. 만약 `do` 절의 코드에 의해 오류가 던져진다면, 그것은 `catch` 절과 비교하여 그들 중 어떤 것이 오류를 처리할 수 있는지 결정합니다.

*Here is the general form of a `do`-`catch` statement:*

다음은 `do`-`catch` 문의 일반적인 형태입니다:

```swift
do {
    try expression
    statements
} catch pattern 1 {
    statements
} catch pattern 2 where condition {
    statements
} catch pattern 3, pattern 4 where condition {
    statements
} catch {
    statements
}
```

*You write a pattern after `catch` to indicate what errors that clause can handle. If a `catch` clause doesn’t have a pattern, the clause matches any error and binds the error to a local constant named `error`. For more information about pattern matching, see [Patterns](https://docs.swift.org/swift-book/ReferenceManual/Patterns.html).*

`catch` 뒤에 패턴을 작성하여 해당 절이 처리할 수 있는 오류를 나타냅니다. `catch` 절에 패턴이 없는 경우의 절은 모든 오류와 일치하고 오류를 `error`라는 이름의 로컬 상수에 바인딩합니다. 패턴 일치에 대한 자세한 내용은 [링크]를 참조하십시오.

*For example, the following code matches against all three cases of the `VendingMachineError` enumeration.*

예를 들어, 다음 코드는 `VendingMachineError` 열거의 세 가지 사례와 모두 일치합니다.

```swift
var vendingMachine = VendingMachine()
vendingMachine.coinsDeposited = 8
do {
    try buyFavoriteSnack(person: "Alice", vendingMachine: vendingMachine)
    print("Success! Yum.")
} catch VendingMachineError.invalidSelection {
    print("Invalid Selection.")
} catch VendingMachineError.outOfStock {
    print("Out of Stock.")
} catch VendingMachineError.insufficientFunds(let coinsNeeded) {
    print("Insufficient funds. Please insert an additional \(coinsNeeded) coins.")
} catch {
    print("Unexpected error: \(error).")
}
// Prints "Insufficient funds. Please insert an additional 2 coins."
```

*In the above example, the `buyFavoriteSnack(person:vendingMachine:)` function is called in a `try` expression, because it can throw an error. If an error is thrown, execution immediately transfers to the `catch` clauses, which decide whether to allow propagation to continue. If no pattern is matched, the error gets caught by the final `catch` clause and is bound to a local `error` constant. If no error is thrown, the remaining statements in the `do` statement are executed.*

위의 예에서 `buyFavoriteSnack(person:vendingMachine:)`함수는 오류를 발생시킬 수 있으므로 `try` 표현으로 호출됩니다. 오류가 발생하면 즉시 실행이 `catch` 절로 전환되며, 이 절은 전파를 계속 허용할지 여부를 결정합니다. 일치하는 패턴이 없으면 오류는 최종 `catch` 절에 의해 걸리고 로컬 `error` 상수에 바인딩됩니다. 오류가 발생하지 않으면 `do` 문의 나머지 문이 실행됩니다.

*The `catch` clauses don’t have to handle every possible error that the code in the `do` clause can throw. If none of the `catch` clauses handle the error, the error propagates to the surrounding scope. However, the propagated error must be handled by some surrounding scope. In a nonthrowing function, an enclosing `do`-`catch` statement must handle the error. In a throwing function, either an enclosing `do`-`catch` statement or the caller must handle the error. If the error propagates to the top-level scope without being handled, you’ll get a runtime error.*

`catch` 절이 `do` 절의 코드가 던질 수 있는 모든 가능한 오류를 처리할 필요는 없습니다. 어떤 `catch` 절도 오류를 처리하지 않으면 오류는 주변 범위로 전파됩니다. 그러나 일부 주변 범위에서 전파된 오류를 처리해야 합니다. 던지지 않는 함수에서 `do`-`catch`문을 동봉하면 오류를 처리해야 합니다. 던지기 함수에서,  `do`-`catch`문을 둘러싸거나 호출자가 오류를 처리해야 합니다. 오류가 처리되지 않고 최상위 범위로 전파되면 런타임 오류가 발생합니다.

*For example, the above example can be written so any error that isn’t a `VendingMachineError` is instead caught by the calling function:*

예를 들어, 위의 예는 `VendingMachineError`가 아닌 모든 오류가 호출 함수에 의해 대신 잡히도록 작성될 수 있습니다:

```swift
func nourish(with item: String) throws {
    do {
        try vendingMachine.vend(itemNamed: item)
    } catch is VendingMachineError {
        print("Couldn't buy that from the vending machine.")
    }
}

do {
    try nourish(with: "Beet-Flavored Chips")
} catch {
    print("Unexpected non-vending-machine-related error: \(error)")
}
// Prints "Couldn't buy that from the vending machine."
```

*In the `nourish(with:)` function, if `vend(itemNamed:)` throws an error that’s one of the cases of the `VendingMachineError` enumeration, `nourish(with:)` handles the error by printing a message. Otherwise, `nourish(with:)` propagates the error to its call site. The error is then caught by the general `catch` clause.*

`nourish(with:)` 함수에서 `vend(itemName:)`가 `VendingMachineError` 열거형의 경우 중 하나인 오류를 발생시키면 `nourish(with:)`는 메시지를 출력하여 오류를 처리합니다. 그렇지 않으면 `nourish(with:)`가 해당 호출 사이트에 오류를 전파합니다. 그런 다음 오류는 일반적인 `catch` 절에 의해 잡힙니다.

*Another way to catch several related errors is to list them after `catch`, separated by commas. For example:*

여러 개의 관련 오류를 잡는 또 다른 방법은 `catch` 뒤에 쉼표로 구분하여 나열하는 것입니다. 예를 들어:

```swift
func eat(item: String) throws {
    do {
        try vendingMachine.vend(itemNamed: item)
    } catch VendingMachineError.invalidSelection, VendingMachineError.insufficientFunds, VendingMachineError.outOfStock {
        print("Invalid selection, out of stock, or not enough money.")
    }
}
```

*The `eat(item:)` function lists the vending machine errors to catch, and its error text corresponds to the items in that list. If any of the three listed errors are thrown, this `catch` clause handles them by printing a message. Any other errors are propagated to the surrounding scope, including any vending-machine errors that might be added later.*

`eat(item:)` 함수는 잡아야 할 자판기 오류를 나열하고 오류 텍스트는 해당 목록의 항목에 해당합니다. 나열된 세 가지 오류 중 하나라도 발생하면 이 `catch` 절은 메시지를 인쇄하여 처리합니다. 나중에 추가될 수 있는 자동판매기 오류를 포함하여 다른 모든 오류는 주변 범위로 전파됩니다.

### *Converting Errors to Optional Values : 오류를 옵셔널 값으로 변환합니다.*

*You use `try?` to handle an error by converting it to an optional value. If an error is thrown while evaluating the `try?` expression, the value of the expression is `nil`. For example, in the following code `x` and `y` have the same value and behavior:*

`try?`를 사용하여 오류를 옵셔널 값으로 변환하여 처리합니다. `try?` 표현식을 평가하는 동안 오류가 발생하면 표현식의 값은 `nil`입니다. 예를 들어, 다음 코드에서 `x`와 `y`는 동일한 값과 동작을 가집니다:

```swift
func someThrowingFunction() throws -> Int {
    // ...
}

let x = try? someThrowingFunction()

let y: Int?
do {
    y = try someThrowingFunction()
} catch {
    y = nil
}
```

*If `someThrowingFunction()` throws an error, the value of `x` and `y` is `nil`. Otherwise, the value of `x` and `y` is the value that the function returned. Note that `x` and `y` are an optional of whatever type `someThrowingFunction()` returns. Here the function returns an integer, so `x` and `y` are optional integers.*

`someThrowingFunction()`가 에러를 던지면, `x`와 `y`의 값은 `nil` 입니다. 그렇지 않으면 `x`와 `y`의 값은 함수가 반환한 값입니다. `x`와 `y`는 `someThrowingFunction()` 가 반환하는 타입의 옵셔널 타입입니다. 던지기 함수()'가 반환됩니다. 여기서 함수는 정수를 반환하므로 `x`와 `y`는 옵셔널 정수입니다.

*Using `try?` lets you write concise error handling code when you want to handle all errors in the same way. For example, the following code uses several approaches to fetch data, or returns `nil` if all of the approaches fail.*

`try?`를 사용해서 모든 오류를 동일한 방식으로 처리하려는 경우 오류 처리 코드를 간결하게 작성할 수 있습니다. 예를 들어, 다음 코드는 여러 가지 접근법을 사용하여 데이터를 가져오거나 모든 접근법이 실패할 경우 `nil`을 반환합니다.

```swift
func fetchData() -> Data? {
    if let data = try? fetchDataFromDisk() { return data }
    if let data = try? fetchDataFromServer() { return data }
    return nil
}
```

### *Disabling Error Propagation: 오류 전파를 사용하지 않도록 설정*

*Sometimes you know a throwing function or method won’t, in fact, throw an error at runtime. On those occasions, you can write `try!` before the expression to disable error propagation and wrap the call in a runtime assertion that no error will be thrown. If an error actually is thrown, you’ll get a runtime error.*

때때로 당신은 던지기 함수나 방법이 실제로 런타임에 오류를 던지지 않는다는 것을 알고 있습니다. 그런 경우에는 표현식 앞에 `try!`를 써서 오류 전파를 비활성화하고 오류가 발생하지 않을 것이라는 런타임 어설션으로 호출을 마무리할 수 있습니다. 실제로 오류가 발생하면 런타임 오류가 발생합니다.

*For example, the following code uses a `loadImage(atPath:)` function, which loads the image resource at a given path or throws an error if the image can’t be loaded. In this case, because the image is shipped with the application, no error will be thrown at runtime, so it’s appropriate to disable error propagation.*

예를 들어, 다음 코드는 `loadImage(atPath:)` 함수를 사용하여 주어진 경로에 이미지 리소스를 로드하거나 이미지를 로드할 수 없는 경우 오류를 발생시킵니다. 이 경우 이미지는 응용 프로그램과 함께 제공되어 런타임에 오류가 발생하지 않으므로 오류 전파를 사용하지 않도록 설정하는 것이 좋습니다.

```swift
let photo = try! loadImage(atPath: "./Resources/John Appleseed.jpg")
```
