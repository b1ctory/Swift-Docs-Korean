# *Function Parameters and Return Values : 기능 매개변수 및 반환값*

*Function parameters and return values are extremely flexible in Swift. You can define anything from a simple utility function with a single unnamed parameter to a complex function with expressive parameter names and different parameter options.*

Swift에서는 기능 매개변수 및 반환값이 매우 유연합니다. 이름 없는 단일 매개 변수를 사용하는 단순 유틸리티 함수부터 표현식 매개변수 이름과 다른 매개변수 옵션을 사용하는 복잡한 함수까지 모든 것을 정의할 수 있습니다.

### *Functions Without Parameters : 매개변수가 없는 함수*

*Functions aren’t required to define input parameters. Here’s a function with no input parameters, which always returns the same `String` message whenever it’s called:*

입력 파라미터를 정의하는 기능은 필요하지 않습니다. 다음은 입력 매개변수가 없는 함수입니다. 이 함수는 호출될 때마다 항상 동일한 `String` 메세지를 반환합니다.

```swift
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
// Prints "hello, world"
```

*The function definition still needs parentheses after the function’s name, even though it doesn’t take any parameters. The function name is also followed by an empty pair of parentheses when the function is called.*

함수 정의는 매개변수를 사용하지 않더라도 함수 이름 뒤에 괄호가 필요합니다. 함수를 호출할 때 함수 이름 뒤에 빈 괄호 쌍이 표시됩니다.

### *Functions With Multiple Parameters : 여러 매개변수를 사용하는 함수*

*Functions can have multiple input parameters, which are written within the function’s parentheses, separated by commas.*

함수는 여러개의 입력 매개변수를 가질 수 있으며, 이는 쉼표로 구분된 함수의 괄호 안에 기록됩니다.

*This function takes a person’s name and whether they have already been greeted as input, and returns an appropriate greeting for that person:*

이 기능은 사용자의 이름과 이미 입력으로 인사를 받았는지 여부를 선택하고 해당 사용자에게 적합한 인사말을 반환합니다.

```swift
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))
// Prints "Hello again, Tim!"
```

*You call the `greet(person:alreadyGreeted:)` function by passing it both a `String` argument value labeled `person` and a `Bool` argument value labeled `alreadyGreeted` in parentheses, separated by commas. Note that this function is distinct from the `greet(person:)` function shown in an earlier section. Although both functions have names that begin with `greet`, the `greet(person:alreadyGreeted:)` function takes two arguments but the `greet(person:)` function takes only one.*

`greet(person:alreadyGreeted:)` 함수를 호출하려면 `person`이라는 레이블이 붙은 문자열 인수 값과 괄호 안에 있는 `alreadyGreeted`이라는 레이블이 붙은 `Bool` 인수 값을 모두 전달하고 쉼표로 구분해서 호출합니다. 이 기능은 이전 섹션에 나와 있는 `greet(person:)` 기능과는 다릅니다. 두 함수 모두 greet로 시작하는 이름이 있지만  `greet(person:alreadyGreeted:)` 함수는 두 개의 인수를 사용하고 `greet(person:)` 함수는 하나의 인수만 사용합니다.

### *Functions Without Return Values : 반환값이 없는 함수*

*Functions aren’t required to define a return type. Here’s a version of the `greet(person:)` function, which prints its own `String` value rather than returning it:*

반환 타입을 정의하기 위해 기능이 필요하지 않습니다. 다음은 값을 반환하지 않고 고유한 `String` 값을 출력하는 `greet(person:)`함수의 버전입니다.

```swift
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave")
// Prints "Hello, Dave!"
```

*Because it doesn’t need to return a value, the function’s definition doesn’t include the return arrow (`->`) or a return type.*

값을 반환할 필요가 없기 때문에 함수의 정의에는 반환 화살표 (`->`)나 반환 타입이 포함되지 않습니다.

> *NOTE*
> 
> *Strictly speaking, this version of the `greet(person:)` function does still return a value, even though no return value is defined. Functions without a defined return type return a special value of type `Void`. This is simply an empty tuple, which is written as `()`.*
> 
> 엄밀하게 말하면, 이 버전의 `greet(person:)`함수는 반환 값이 정의되지 않더라도 값을 반환합니다. 반환 타입이 정의되지 않은 함수는 `Void` 타입의 특수 값을 반환합니다. 이거은 단순히 빈 튜플이며 `()` 로 쓰여집니다.

*The return value of a function can be ignored when it’s called:*

함수의 반환값은 다음과 같이 호출될 때 무시할 수 있습니다.

```swift
func printAndCount(string: String) -> Int {
    print(string)
    return string.count
}
func printWithoutCounting(string: String) {
    let _ = printAndCount(string: string)
}
printAndCount(string: "hello, world")
// prints "hello, world" and returns a value of 12
printWithoutCounting(string: "hello, world")
// prints "hello, world" but doesn't return a value
```

*The first function, `printAndCount(string:)`, prints a string, and then returns its character count as an `Int`. The second function, `printWithoutCounting(string:)`, calls the first function, but ignores its return value. When the second function is called, the message is still printed by the first function, but the returned value isn’t used.*

첫번째 함수인 `printAndCount(string:)`는 문자열을 출력한 다음 해당 문자 수를 Int 로 반환합니다. 두번째 함수 `printWithoutCounting(string:)`는 첫번째 함수를 호출하지만 반환 값은 무시합니다. 두번째 함수가 호출될 때 메세지는 첫번째 함수에 의해 계속 출력되지만 반환된 값은 사용되지 않습니다.

> *NOTE*
> 
> *Return values can be ignored, but a function that says it will return a value must always do so. A function with a defined return type can’t allow control to fall out of the bottom of the function without returning a value, and attempting to do so will result in a compile-time error.*
> 
> 리턴 타입은 무시할 수 있지만, 반환값을 반환한다는 함수는 항상 그렇게 해야합니다. 반환 타입이 정의된 함수는 값을 반환하지 않고 함수의 맨 아래에서 컨트롤이 빠지는 것을 허용할 수 없으며 이를 시도하면 컴파일 타임 에러가 발생합니다.

### *Functions with Multiple Return Values : 복수 반환 값이 있는 함수*

*You can use a tuple type as the return type for a function to return multiple values as part of one compound return value.*

복합체 반환값의 일부로 여러 값을 반환하는 함수의 반환 타입으로 튜플 타입을 사용할 수 있습니다.

*The example below defines a function called `minMax(array:)`, which finds the smallest and largest numbers in an array of `Int` values:*

아래의 예시는 Int 값의 배열에서 가장 작은 숫자와 가장 큰 숫자를 찾는 `minMax(array:)`라는 함수를 정의합니다.

```swift
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

*The `minMax(array:)` function returns a tuple containing two `Int` values. These values are labeled `min` and `max` so that they can be accessed by name when querying the function’s return value.*

`minMax(array:)`함수는 두개의 `Int`값을 포함하는 튜플을 반환합니다. 이 값들은 함수의 반환 값을 쿼리할 때 이름으로 접근할 수 있도록 `min`과 `max`라는 레이블이 붙습니다. 

*The body of the `minMax(array:)` function starts by setting two working variables called `currentMin` and `currentMax` to the value of the first integer in the array. The function then iterates over the remaining values in the array and checks each value to see if it’s smaller or larger than the values of `currentMin` and `currentMax` respectively. Finally, the overall minimum and maximum values are returned as a tuple of two `Int` values.*

`minMax(array:)` 함수의 본문은 `currentMin`과 `currentMax`라는 두 개의 작업 변수를 배열의 첫번째 정수 값으로 설정하는 것으로 시작합니다. 그런 다음 이 함수는 배열의 나머지 값에 대해 반복하고 각 값이 각각 `currentMin`과 `currentMax`의 값보다 작은지 큰지 확인합니다. 마지막으로, 전체 최소값과 최대값은 두 개의 `Int` 값의 튜플로 반환됩니다.

*Because the tuple’s member values are named as part of the function’s return type, they can be accessed with dot syntax to retrieve the minimum and maximum found values:*

튜플의 멤버 값은 함수의 반환 타입의 일부로 지정되기 때문에 도트 구문을 사용해서 최소 및 최대 발견 값을 검색할 수 있습니다.

```swift
let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")
// Prints "min is -6 and max is 109"
```

*Note that the tuple’s members don’t need to be named at the point that the tuple is returned from the function, because their names are already specified as part of the function’s return type.*

튜플의 구성원들의 이름은 이미 함수의 반환 타입의 일부로 지정되어있기 때문에 함수에서 반환되는 지점에서 이름을 지정할 필요가 없습니다. 

#### *Optional Tuple Return Types : 옵셔널 튜플 반환 타입*

*If the tuple type to be returned from a function has the potential to have “no value” for the entire tuple, you can use an optional tuple return type to reflect the fact that the entire tuple can be `nil`. You write an optional tuple return type by placing a question mark after the tuple type’s closing parenthesis, such as `(Int, Int)?` or `(String, Int, Bool)?`.*

함수에서 반환될 튜플 타입이 전체 튜플에 대해 "값이 없을" 가능성이 있는 경우, 옵셔널 튜플 반환 타입을 이용해서 전체 튜플이 nil일 수 있다는 사실을 반영할 수 있습니다. 옵셔널 튜플 반환 타입은 `(Int, Int)?`이나  `(String, Int, Bool)?`와 같이 튜플 타입의 닫힘 괄호 뒤에 물음표를 배치해서 작성합니다.

> *NOTE*
> 
> *An optional tuple type such as `(Int, Int)?` is different from a tuple that contains optional types such as `(Int?, Int?)`. With an optional tuple type, the entire tuple is optional, not just each individual value within the tuple.*
> 
> `(Int, Int)?`와 같은 옵셔널 튜플 타입은 `(Int?, Int?)` 와 같은 옵셔널 타입을 포함하는 튜플과는 다릅니다. 옵셔널 튜플 타입의 경우, 튜플 내의 각 개별 값만 옵셔널인 것이 아니라 전체 튜플은 옵셔널 입니다.

*The `minMax(array:)` function above returns a tuple containing two `Int` values. However, the function doesn’t perform any safety checks on the array it’s passed. If the `array` argument contains an empty array, the `minMax(array:)` function, as defined above, will trigger a runtime error when attempting to access `array[0]`.*

위의 `minMax(array:)` 함수는 두 개의 `Int` 값을 포함하는 튜플을 반환합니다. 그러나 전달된 배열에 대해서는 안전 체크가 수행되지 않습니다. `array` 인수에 빈 배열이 포함된 경우 위에서 정의한 대로 `minMax(array:)` 함수는 `array[0]`에 엑세스하려고 할 때 런타임 오류를 발생시킵니다.

*To handle an empty array safely, write the `minMax(array:)` function with an optional tuple return type and return a value of `nil` when the array is empty:*

빈 배열을 안전하게 처리하려면 옵셔널 튜플 반환 타입으로 `minMax(array:)` 함수를 작성하고 배열이 비어있을 때 `nil` 값을 반환합니다.

```swift
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil }
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

*You can use optional binding to check whether this version of the `minMax(array:)` function returns an actual tuple value or `nil`:*

옵셔널 바인딩을 사용해서 이 버전의  `minMax(array:)` 함수가 실제 튜플 값을 반환하는지 혹은 nil을 반환하는지 확인할 수 있습니다.

```swift
if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
    print("min is \(bounds.min) and max is \(bounds.max)")
}
// Prints "min is -6 and max is 109"
```

### *Functions With an Implicit Return : 함수의 암묵적 반환*

*If the entire body of the function is a single expression, the function implicitly returns that expression. For example, both functions below have the same behavior:*

함수의 전체 본문이 단일 표현식인 경우 함수는 암시적으로 해당 표현식을 반환합니다. 예를 들어, 아래의 두 함수는 동일한 동작을 참조하세요:

```swift
func greeting(for person: String) -> String {
    "Hello, " + person + "!"
}
print(greeting(for: "Dave"))
// Prints "Hello, Dave!"

func anotherGreeting(for person: String) -> String {
    return "Hello, " + person + "!"
}
print(anotherGreeting(for: "Dave"))
// Prints "Hello, Dave!"
```

*The entire definition of the `greeting(for:)` function is the greeting message that it returns, which means it can use this shorter form. The `anotherGreeting(for:)` function returns the same greeting message, using the `return` keyword like a longer function. Any function that you write as just one `return` line can omit the `return`.*

`greeting(for:)`함수의 전체 정의는 반환되는 인사말 메세지이며 이는 이 짧은 타입을 사용할 수 있음을 의미합니다. `anotherGreeting(for:)` 함수는 `return` 키워드를 더 긴 함수처럼 사용해서 동일한 인사말 메세지를 반환합니다. 한 줄의 `return`으로 쓰는 함수는 `return`을 생략할 수 있습니다.

*As you’ll see in [Shorthand Getter Declaration](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID608), property getters can also use an implicit return.*

[링크]에서 볼 수 있듯이, 프로퍼티 getter 도 암묵적 반환을 사용할 수 있습니다.

> *NOTE*
> 
> *The code you write as an implicit return value needs to return some value. For example, you can’t use `print(13)` as an implicit return value. However, you can use a function that never returns like `fatalError("Oh no!")` as an implicit return value, because Swift knows that the implicit return doesn’t happen.*
> 
> 암시적 반환값으로 작성하는 코드는 일부 값을 반환해야 합니다. 예를 들어 암시적 반환 값으로 `print(13)`을 사용할 수 없습니다. 그러나 Swift는 암묵적 변환이 발생하지 않는 다는 것을 알고있기 때문에 `fatalError("Oh no!")`와 같이 절대 반환되지 않는 함수를 암묵적 반환 값으로 사용할 수 있습니다.
