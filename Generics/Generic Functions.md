## *Generic Functions : 제네릭함수*

*Generic functions can work with any type. Here’s a generic version of the `swapTwoInts(_:_:)` function from above, called `swapTwoValues(_:_:)`:*

제네릭 함수는 모든 타입에서 작동할 수 있습니다. 다음은 위에서 언급한 `swapTwoInts(_:_:)` 함수의 제네릭 버전인 `swapTwoValues(_:_:)`입니다.

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

*The body of the `swapTwoValues(_:_:)` function is identical to the body of the `swapTwoInts(_:_:)` function. However, the first line of `swapTwoValues(_:_:)` is slightly different from `swapTwoInts(_:_:)`. Here’s how the first lines compare:*

`swapTwoValues(_:_:)` 함수의 본문은 `swapTwoInts(_:_:)` 함수의 본문과 동일합니다. 그러나 `swapTwoValues(_:_:)`의 첫 번째 줄은 `swapTwoInts(_:_:)`와 약간 다릅니다. 첫 번째 줄을 비교하는 방법은 다음과 같습니다.

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int)
func swapTwoValues<T>(_ a: inout T, _ b: inout T)The generic version of the function uses a placeholder type name (called `T`, in this case) instead of an actual type name (such as `Int`, `String`, or `Double`). The placeholder type name doesn’t say anything about what `T` must be, but it does say that both `a` and `b` must be of the same type `T`, whatever `T` represents. The actual type to use in place of `T` is determined each time the `swapTwoValues(_:_:)` function is called.
```

*The other difference between a generic function and a nongeneric function is that the generic function’s name (`swapTwoValues(_:_:)`) is followed by the placeholder type name (`T`) inside angle brackets (`<T>`). The brackets tell Swift that `T` is a placeholder type name within the `swapTwoValues(_:_:)` function definition. Because `T` is a placeholder, Swift doesn’t look for an actual type called `T`.*

제네릭 함수와 비제네릭 함수의 다른 차이점은 제네릭 함수의 이름(`swapTwoValues(_:_:)`) 뒤에 꺾쇠 괄호(`<T>` ), 대괄호는 Swift에 `T`가 `swapTwoValues(_:_:)` 함수 정의 내의 플레이스홀더 타입 이름임을 알려줍니다. `T`는 자리 표시자이므로 Swift는 `T`라는 실제 타입을 찾지 않습니다.

*The `swapTwoValues(_:_:)` function can now be called in the same way as `swapTwoInts`, except that it can be passed two values of any type, as long as both of those values are of the same type as each other. Each time `swapTwoValues(_:_:)` is called, the type to use for `T` is inferred from the types of values passed to the function.*

`swapTwoValues(_:_:)` 함수는 이제 `swapTwoInts`와 동일한 방식으로 호출할 수 있습니다. 단, 두 값이 모두 서로. `swapTwoValues(_:_:)`가 호출될 때마다 `T`에 사용할 타입이 함수에 전달된 값의 타입에서 유추됩니다.

*In the two examples below, `T` is inferred to be `Int` and `String` respectively:*

아래의 두 예에서 `T`는 각각 `Int` 및 `String`으로 유추됩니다.

```swift
var someInt = 3var anotherInt = 107swapTwoValues(&someInt, &anotherInt)// someInt is now 107, and anotherInt is now 3
var someString = "hello"var anotherString = "world"swapTwoValues(&someString, &anotherString)// someString is now "world", and anotherString is now "hello"
```

> *Note*
> 
> *The `swapTwoValues(_:_:)` function defined above is inspired by a generic function called `swap`, which is part of the Swift standard library, and is automatically made available for you to use in your apps. If you need the behavior of the `swapTwoValues(_:_:)` function in your own code, you can use Swift’s existing `swap(_:_:)` function rather than providing your own implementation.*
> 
> 위에서 정의한 `swapTwoValues(_:_:)` 함수는 Swift 표준 라이브러리의 일부인 `swap`이라는 일반 함수에서 영감을 얻었으며 앱에서 사용할 수 있도록 자동으로 제공됩니다. 자체 코드에서 `swapTwoValues(_:_:)` 함수의 동작이 필요한 경우 자체 구현을 제공하는 대신 Swift의 기존 `swap(_:_:)` 함수를 사용할 수 있습니다.


