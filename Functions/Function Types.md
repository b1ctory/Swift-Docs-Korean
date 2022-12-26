## *Function Types : 함수 타입*

*Every function has a specific function type, made up of the parameter types and the return type of the function.*

모든 함수에는 매개변수 타입과 함수의 반환 타입으로 구성된 특정 함수 타입이 있습니다.

*For example:*

예를 들어:

```swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}
func multiplyTwoInts(_ a: Int, _ b: Int) -> Int {
    return a * b
}
```

*This example defines two simple mathematical functions called `addTwoInts` and `multiplyTwoInts`. These functions each take two `Int` values, and return an `Int` value, which is the result of performing an appropriate mathematical operation.*

이 예제는 `addTwoInts`와 `multiplyTwoInts`라는 두 개의 간단한 수학적 함수를 정의합니다. 이 함수들은 각각 두개의 `Int`값을 취하고, 적절한 수학적 연산을 수행한 결과인 `Int`를 반환합니다.

*The type of both of these functions is `(Int, Int) -> Int`. This can be read as:*

이 두 함수의 타입은 `(Int, Int) -> Int`입니다. 이 값은 이렇게 읽힐 수 있습니다:

*“A function that has two parameters, both of type `Int`, and that returns a value of type `Int`.”*

`Int`타입인 두개의 매개변수를 가지며, 타입 `Int`의 값을 반환하는 함수

*Here’s another example, for a function with no parameters or return value:*

다음은 매개변수 혹은 반환값이 없는 함수에 대한 다른 예시입니다:

```swift
func printHelloWorld() {
    print("hello, world")
}
```

*The type of this function is `() -> Void`, or “a function that has no parameters, and returns `Void`.”*

이 함수의 타입은 `() -> Void` 혹은 "파라미터가 없고 `Void` 를 반환하는 함수입니다."

### *Using Function Types : 함수 타입 사용*

*You use function types just like any other types in Swift. For example, you can define a constant or variable to be of a function type and assign an appropriate function to that variable:*

Swift의 다른 타입과 마찬가지로 함수 타입을 사용합니다. 예를 들어, 함수 타입의 상수 혹은 변수를 정의하고 해당 변수에 적절한 함수를 할당할 수 있습니다.

```swift
var mathFunction: (Int, Int) -> Int = addTwoInts
```

*This can be read as:*

이것은 이렇게 읽을 수 있습니다:

*“Define a variable called `mathFunction`, which has a type of ‘a function that takes two `Int` values, and returns an `Int` value.’ Set this new variable to refer to the function called `addTwoInts`.”*

"두 개의 `Int` 값을 취해 `Int` 값을 반환하는 `mathFunction` 라는 변수를 정의합니다. `addTwoInts` 라는 함수를 참조하도록 새 변수를 설정합니다."

*The `addTwoInts(_:_:)` function has the same type as the `mathFunction` variable, and so this assignment is allowed by Swift’s type-checker.*

`addTwoInts(_:_:)`함수는 mathFunction 변수와 같은 타입을 가지고 있으므로 Swift의 타입-검사기에서 이 할당을 허용합니다.

*You can now call the assigned function with the name `mathFunction`:*

이제 `mathFunction`라는 이름으로 할당된 함수를 호출할 수 있습니다.

```swift
print("Result: \(mathFunction(2, 3))")
// Prints "Result: 5"
```

*A different function with the same matching type can be assigned to the same variable, in the same way as for nonfunction types:*

비기능 타입과 동일한 방식으로 동일한 일치 타입의 다른 함수를 동일한 변수에 할당할 수 있습니다.

```swift
mathFunction = multiplyTwoInts
print("Result: \(mathFunction(2, 3))")
// Prints "Result: 6"
```

*As with any other type, you can leave it to Swift to infer the function type when you assign a function to a constant or variable:*

다른 타입과 마찬가지로, 함수를 상수 혹은 변수에 할당할 때 함수 타입을 유추하려면 Swift에 맡길 수 있습니다.

```swift
let anotherMathFunction = addTwoInts
// anotherMathFunction is inferred to be of type (Int, Int) -> Int
```

### *Function Types as Parameter Types : 매개변수 타입으로서의 함수 타입*

*You can use a function type such as `(Int, Int) -> Int` as a parameter type for another function. This enables you to leave some aspects of a function’s implementation for the function’s caller to provide when the function is called.*

`(Int, Int) -> Int`와 같은 함수 타입을 다른 함수의 매개변수 타입으로 사용할 수 있습니다. 이렇게하면 함수가 호출될 때 함수 호출자가 제공할 함수 구현의 일부 측면을 넘길 수 있습니다.

*Here’s an example to print the results of the math functions from above:*

다음은 위에서 연산 함수의 결과를 출력하는 예시입니다.

```swift
func printMathResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
    print("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)
// Prints "Result: 8"
```

*This example defines a function called `printMathResult(_:_:_:)`, which has three parameters. The first parameter is called `mathFunction`, and is of type `(Int, Int) -> Int`. You can pass any function of that type as the argument for this first parameter. The second and third parameters are called `a` and `b`, and are both of type `Int`. These are used as the two input values for the provided math function.*

이 예제는 세 개의 변수가 있는 `printMathResult(_:_:_:)`라는 함수를 정의합니다. 첫번째 매개변수는 `mathFunction`이라고 하며 타입은 `(Int, Int) -> Int`입니다. 이 첫번째 매개변수에 대한 인수로 해당 타입의 함수를 전달할 수 있습니다. 두번째와 세번째 매개변수는 `a`와 `b`라고 하며 둘 다 `Int` 타입입니다. 이들 값은 제공된 산술 함수에 대한 두 개의 입력값으로 사용됩니다.

*When `printMathResult(_:_:_:)` is called, it’s passed the `addTwoInts(_:_:)` function, and the integer values `3` and `5`. It calls the provided function with the values `3` and `5`, and prints the result of `8`.*

`printMathResult(_:_:)`를 호출하면 `addTwoInts(_:_:)`함수와 정수 값 3 및 5를 전달합니다. 제공된 함수를 `3`과 `5`와 함께 호출하고 결과 `8`을 출력합니다.

*The role of `printMathResult(_:_:_:)` is to print the result of a call to a math function of an appropriate type. It doesn’t matter what that function’s implementation actually does—it matters only that the function is of the correct type. This enables `printMathResult(_:_:_:)` to hand off some of its functionality to the caller of the function in a type-safe way.*

`printMathResult(_:_:)`의 역할은 적절한 타입의 산술 함수에 호출된 결과를 인쇄하는 것입니다. 함수의 구현이 실제로 무엇을 하는지는 중요하지 않습니다. 함수가 올바른 타입인지만 중요합니다. 이를 통해 `printMathResult(_:_:)`는 함수의 일부를 타입에 안전한 방식으로 함수 호출자에게 전달할 수 있습니다.

### *Function Types as Return Types : 반환 타입으로서의 함수 타입*

*You can use a function type as the return type of another function. You do this by writing a complete function type immediately after the return arrow (`->`) of the returning function.*

다른 함수의 반환 타입으로 함수 타입을 사용할 수 있습니다. 반환 함수의 반환 화살표 (`->`) 바로 뒤에 완전한 함수 타입을 작성해서 이 작업을 수행합니다.

*The next example defines two simple functions called `stepForward(_:)` and `stepBackward(_:)`. The `stepForward(_:)` function returns a value one more than its input value, and the `stepBackward(_:)` function returns a value one less than its input value. Both functions have a type of `(Int) -> Int`:*

다음 예제는 `stepForward(_:)` 와 `stepBackward(_:)`라는 두 개의 간단한 함수를 정의합니다. `stepForward(_:)` 함수는 입력값보다 하나 더 많은 값을 반환하고, `stepBackward(_:)` 함수는 입력값보다 하나 더 작은 값을 반환합니다. 두 함수 모두 `(Int) -> Int` 타입을 가집니다.

```swift
func stepForward(_ input: Int) -> Int {
    return input + 1
}
func stepBackward(_ input: Int) -> Int {
    return input - 1
}
```

*Here’s a function called `chooseStepFunction(backward:)`, whose return type is `(Int) -> Int`. The `chooseStepFunction(backward:)` function returns the `stepForward(_:)` function or the `stepBackward(_:)` function based on a Boolean parameter called `backward`:*

여기에 `(Int) -> Int`의 리턴타입을 가지는 `chooseStepFunction(backward:)` 함수가 있습니다. `chooseStepFunction(backward:)` 함수는 `backward`라고 불리는 Boolean 매개변수를 기반으로 하는 `stepForward(_:) `혹은 `stepBackward(_:)`를 반환합니다. 

```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    return backward ? stepBackward : stepForward
}
```

*You can now use `chooseStepFunction(backward:)` to obtain a function that will step in one direction or the other:*

이제 `chooseStepFunction(backward:)`를 사용해서 한 방향 혹은 다른 방향으로 이동하는 함수를 얻을 수 있습니다.

```swift
var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero now refers to the stepBackward() function
```

*The example above determines whether a positive or negative step is needed to move a variable called `currentValue` progressively closer to zero. `currentValue` has an initial value of `3`, which means that `currentValue > 0` returns `true`, causing `chooseStepFunction(backward:)` to return the `stepBackward(_:)` function. A reference to the returned function is stored in a constant called `moveNearerToZero`.*

위의 예시는 `currentValue`라는 변수를 점진적으로 0에 가깝게 이동하기 위해 양의 단계가 필요한지 음의 단계가 필요한지 여부를 결정합니다. `currentValue`의 초기값은 `3`이며, 이는 `currentValue > 0`이 true를 반환함을 의미하며, 이로인해 `chooseStepFunction(backward:)`이 `stepBackward(_:)`함수를 반환하게 됩니다. 반환된 함수에 대한 참조는 `moveNearerToZero`라고 불리는 상수에 저장됩니다.

*Now that `moveNearerToZero` refers to the correct function, it can be used to count to zero:*

이제 그 `moveNearerToZero`는 올바른 함수를 가리키며, 0까지 셀 때 사용할 수 있습니다.

```swift
print("Counting to zero:")
// Counting to zero:
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// 3...
// 2...
// 1...
// zero!
```
