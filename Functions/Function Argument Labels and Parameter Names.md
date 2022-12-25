## *Function Argument Labels and Parameter Names : 함수 인수 레이블 및 매개변수 이름*

*Each function parameter has both an argument label and a parameter name. The argument label is used when calling the function; each argument is written in the function call with its argument label before it. The parameter name is used in the implementation of the function. By default, parameters use their parameter name as their argument label.*

각 함수 매개 변수에는 인수 레이블과 매개변수 이름이 모두 있습니다. 인수 레이블은 함수를 호출할 때 사용되며, 각 인수는 함수 호출 앞에 인수 레이블을 붙여 작성됩니다. 매개변수 이름은 함수 구현에 사용됩니다.기본적으로 매개 변수는 매개변수 이름을 인수레이블로 사용합니다.

```swift
func someFunction(firstParameterName: Int, secondParameterName: Int) {
    // In the function body, firstParameterName and secondParameterName
    // refer to the argument values for the first and second parameters.
}
someFunction(firstParameterName: 1, secondParameterName: 2)
```

*All parameters must have unique names. Although it’s possible for multiple parameters to have the same argument label, unique argument labels help make your code more readable.*

모든 매개변수에는 고유한 이름이 있어야 합니다. 여러 매개 변수에 동일한 인수레이블이 있을 수 있지만 고유한 인수 레이블을 사용하면 코드를 더 쉽게 읽을 수 있습니다.

### *Specifying Argument Labels : 인수 레이블 지정*

*You write an argument label before the parameter name, separated by a space:*

매개변수 이름 앞에 인수 레이블을 쓰고 공백으로 구분합니다.

```swift
func someFunction(argumentLabel parameterName: Int) {
    // In the function body, parameterName refers to the argument value
    // for that parameter.
}
```

*Here’s a variation of the `greet(person:)` function that takes a person’s name and hometown and returns a greeting:*

다음은 사람의 이름과 고향을 입력하고 인사말을 반환하는 `greet(person:)` 함수의 변형입니다.

```swift
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)!  Glad you could visit from \(hometown)."
}
print(greet(person: "Bill", from: "Cupertino"))
// Prints "Hello Bill!  Glad you could visit from Cupertino."
```

*The use of argument labels can allow a function to be called in an expressive, sentence-like manner, while still providing a function body that’s readable and clear in intent.*

인수 레이블을 사용하면 함수를 표면적이고 문장과 같은 방식으로 호출하는 동시에 읽기 쉽고 명확한 의도를 가진 함수 본문을 제공할 수 있습니다.

### *Omitting Argument Labels : 인수 레이블 생략*

*If you don’t want an argument label for a parameter, write an underscore (`_`) instead of an explicit argument label for that parameter.*

파라미터에 대한 인수 레이블을 사용하지 않으려면 해당 파라미터에 대한 명시적 인수 레이블 대신 밑줄(`_`)을 작성합니다.

```swift
func someFunction(_ firstParameterName: Int, secondParameterName: Int) {
    // In the function body, firstParameterName and secondParameterName
    // refer to the argument values for the first and second parameters.
}
someFunction(1, secondParameterName: 2)
```

*If a parameter has an argument label, the argument must be labeled when you call the function.*

파라미터에 인수 레이블이 있는 경우 함수를 호출할 때 인수에 레이블을 붙여야 합니다.

### *Default Parameter Values : 기본 매개변수 값*

*You can define a default value for any parameter in a function by assigning a value to the parameter after that parameter’s type. If a default value is defined, you can omit that parameter when calling the function.*

매개변수 타입 뒤에 있는 매개변수에 값을 할당해서 함수의 매개변수에 대한 기본값을 정의할 수 있습니다. 기본값이 정의되어 있으면 함수를 호출할 때 해당 매개변수를 생략할 수 있습니다.

```swift
func someFunction(parameterWithoutDefault: Int, parameterWithDefault: Int = 12) {
    // If you omit the second argument when calling this function, then
    // the value of parameterWithDefault is 12 inside the function body.
}
someFunction(parameterWithoutDefault: 3, parameterWithDefault: 6) // parameterWithDefault is 6
someFunction(parameterWithoutDefault: 4) // parameterWithDefault is 12
```

*Place parameters that don’t have default values at the beginning of a function’s parameter list, before the parameters that have default values. Parameters that don’t have default values are usually more important to the function’s meaning—writing them first makes it easier to recognize that the same function is being called, regardless of whether any default parameters are omitted.*

기본값이 없는 매개변수를 함수의 매개변수 목록 시작 부분에 기본값이 있는 매개변수 앞에 배치합니다. 기본값이 없는 매개변수는 일반적으로 함수의 의미에 더 중요합니다. 먼저 작성하면 기본 매개변수가 생략되었는지 여부에 관계없이 동일한 함수가 호출되고 있음을 쉽게 인식할 수 있습니다.

### *Variadic Parameters : 가변 매개변수*

*A variadic parameter accepts zero or more values of a specified type. You use a variadic parameter to specify that the parameter can be passed a varying number of input values when the function is called. Write variadic parameters by inserting three period characters (`...`) after the parameter’s type name.*

가변 매개변수는 지정된 타입의 값을 0개 이상 허용합니다. 가변 매개변수를 사용해서 함수가 호출될 때 매개변수가 다양한 수의 입력 값을 전달할 수 있도록 지정할 수 있습니다. 매개변수의 타입 이름 뒤에 마침표 문자 (`...`)를 세개 삽입해서 가변 매개변수를 작성합니다.

*The values passed to a variadic parameter are made available within the function’s body as an array of the appropriate type. For example, a variadic parameter with a name of `numbers` and a type of `Double...` is made available within the function’s body as a constant array called `numbers` of type `[Double]`.*

가변 매개변수에 전달된 값은 함수 본문 내에서 적절한 타입의 배열로 사용할 수 있습니다. 예를 들어, 이름이 `numbers`이고, 타입이 `Double`인 가변매개변수가 있습니다. 함수의 본문 내에서 `[Double]` 타입의 `numbers`라는 상수 배열로 사용할 수 있습니다.

*The example below calculates the arithmetic mean (also known as the average) for a list of numbers of any length:*

아래 예제는 임의의 길이의 숫자 목록에 대한 산술 평균 (평균이라고도 함)을 계산합니다.

```swift
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8.25, 18.75)
// returns 10.0, which is the arithmetic mean of these three numbers
```

*A function can have multiple variadic parameters. The first parameter that comes after a variadic parameter must have an argument label. The argument label makes it unambiguous which arguments are passed to the variadic parameter and which arguments are passed to the parameters that come after the variadic parameter.*

한 함수에 여러 가변 매개변수가 있을 수 있습니다. 가변매개변수 다음에 오는 첫번째 매개변수에는 인수 레이블이 있어야 합니다. 인수 레이블은 가변 매개변수에 전달되는 인수와 가변매개변수 다음에 오는 매개변수에 전달되는 인수를 명확하게 합니다.

### *In-Out Parameters : In-out 매개변수*

*Function parameters are constants by default. Trying to change the value of a function parameter from within the body of that function results in a compile-time error. This means that you can’t change the value of a parameter by mistake. If you want a function to modify a parameter’s value, and you want those changes to persist after the function call has ended, define that parameter as an in-out parameter instead.*

함수 매개변수는 기본적으로 상수입니다. 함수 매개변수의 값을 해당 함수의 본문 내에서 변경하려고 하면 컴파일 타임 오류가 발생합니다. 즉, 실수로 매개변수 값을 변경할 수 없습니다. 함수가 매개변수의 값을 수정하고 함수 호출이 종료된 후에도 이러한 변경 사항이 지속되도록 하려면 대신 해당 매개변수를 인아웃 매개변수로 정의하세요.

*You write an in-out parameter by placing the `inout` keyword right before a parameter’s type. An in-out parameter has a value that’s passed in to the function, is modified by the function, and is passed back out of the function to replace the original value. For a detailed discussion of the behavior of in-out parameters and associated compiler optimizations, see [In-Out Parameters](https://docs.swift.org/swift-book/ReferenceManual/Declarations.html#ID545).*

`inout` 키워드를 매개변수 타입 바로 앞에 배치해서 `in-out` 매개변수를 작성합니다. 인아웃 매개변수는 함수에 전달된 값을 가지며, 함수에 의해 수정된 후 원래 값을 대체하기 위해 함수에서 다시 전달됩니다. 인아웃 매개변수의 동작 및 관련 커파일러 최적화에 대한 자세한 내용은 [링크]를 참조하세요.

*You can only pass a variable as the argument for an in-out parameter. You can’t pass a constant or a literal value as the argument, because constants and literals can’t be modified. You place an ampersand (`&`) directly before a variable’s name when you pass it as an argument to an in-out parameter, to indicate that it can be modified by the function.*

변수는 인아웃 매개변수의 인수로만 전달할 수 있습니다. 상수 및 리터럴은 수정할 수 없으므로 상수 혹은 리터럴 값을 인수로 전달할 수 없습니다. 변수 이름 바로 앞에 앰퍼샌드(`&`) 를 입력 매개변수에 인수로 전달해서 함수에 의해 수정될 수 있음을 나타냅니다.

> *NOTE*
> 
> *In-out parameters can’t have default values, and variadic parameters can’t be marked as `inout`.*
> 
> 인아웃 매개변수는 기본값을 가질 수 없으며 가변매개변수는 `inout`으로 표시할 수 없습니다.

*Here’s an example of a function called `swapTwoInts(_:_:)`, which has two in-out integer parameters called `a` and `b`:*

다음은 `a`와 `b`라는 두 개의 인아웃 정수 매개변수를 갖는 `swapTwoInts(_:)`라는 함수의 예입니다.

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

*The `swapTwoInts(_:_:)` function simply swaps the value of `b` into `a`, and the value of `a` into `b`. The function performs this swap by storing the value of `a` in a temporary constant called `temporaryA`, assigning the value of `b` to `a`, and then assigning `temporaryA` to `b`.*

`swapTwoInts(_:_:)` 함수는 단순히 `b`의 값을` a`로, `a`의 값을 `b`로 바꿉니다. 이 함수는 `temporaryA`라는 임시 상수에 `a`값을 저장하고, `b`의 값을 `a`에 할당한 다음 `temporaryA`를 할당해서 `b`에서 `a`로 스왑할 수 있습니다.

*You can call the `swapTwoInts(_:_:)` function with two variables of type `Int` to swap their values. Note that the names of `someInt` and `anotherInt` are prefixed with an ampersand when they’re passed to the `swapTwoInts(_:_:)` function:*

두 변수 타입이 `Int`인 `swapTwoInts(_:_:)`함수를 호출해서 값을 스왑할 수 있습니다. `someInt`와 `anotherInt`의 이름은 `swapTwoInts(_:_:)` 함수로 전달될 때 앰퍼샌드 앞에 붙는다는 점을 참고하세요.

```swift
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// Prints "someInt is now 107, and anotherInt is now 3"
```

*The example above shows that the original values of `someInt` and `anotherInt` are modified by the `swapTwoInts(_:_:)` function, even though they were originally defined outside of the function.*

위의 예는 someInt와 anotherInt의 원본 값은 함수 외부에서 정의되었지만, `swapTwoInts(_:_:)`함수에 의해 수정됩니다.

> *NOTE*
> 
> *In-out parameters aren’t the same as returning a value from a function. The `swapTwoInts` example above doesn’t define a return type or return a value, but it still modifies the values of `someInt` and `anotherInt`. In-out parameters are an alternative way for a function to have an effect outside of the scope of its function body.*
> 
> 인아웃 매개변수는 함수에서 값을 반환하는 것과 다릅니다. 위의 `swapTwoInts` 예제는 반환 타입이나 반환 값을 정의하지 않지만 `someInt`와 `anotherInt`의 값을 수정합니다. 인아웃 매개변수는 함수가 함수 본체의 범위를 벗어나는 효과를 갖는 대체 방법입니다.
