## *The Problem That Generics Solve : 제네릭이 해결하는 문제*

*Here’s a standard, nongeneric function called `swapTwoInts(_:_:)`, which swaps two `Int` values:*

다음은 두 개의 `Int` 값을 교환하는 `swapTwoInts(_:_:)`라는 제네릭이 아닌 표준 함수입니다.

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

*This function makes use of in-out parameters to swap the values of `a` and `b`, as described in [In-Out Parameters](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID173).*

이 함수는 [링크]에 설명된 대로 In-Out 파라메터를 사용하여 `a`와 `b`의 값을 교환합니다.

*The `swapTwoInts(_:_:)` function swaps the original value of `b` into `a`, and the original value of `a` into `b`. You can call this function to swap the values in two `Int` variables:*

`swapTwoInts(_:_:)` 함수는 `b`의 원래 값을 `a`로, `a`의 원래 값을 `b`로 바꿉니다. 이 함수를 호출하여 두 개의 `Int` 변수의 값을 바꿀 수 있습니다.

```swift
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// Prints "someInt is now 107, and anotherInt is now 3"
```

*The `swapTwoInts(_:_:)` function is useful, but it can only be used with `Int` values. If you want to swap two `String` values, or two `Double` values, you have to write more functions, such as the `swapTwoStrings(_:_:)` and `swapTwoDoubles(_:_:)` functions shown below:*

`swapTwoInts(_:_:)` 함수는 유용하지만 `Int` 값에만 사용할 수 있습니다. 2개의 `String` 값 또는 2개의 `Double` 값을 교환하려면 아래 표시된 `swapTwoStrings(_:_:)` 및 `swapTwoDoubles(_:_:)` 함수와 같은 추가 함수를 작성해야 합니다. :

```swift
func swapTwoStrings(_ a: inout String, _ b: inout String) {
    let temporaryA = a
    a = b
    b = temporaryA
}

func swapTwoDoubles(_ a: inout Double, _ b: inout Double) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

*You may have noticed that the bodies of the `swapTwoInts(_:_:)`, `swapTwoStrings(_:_:)`, and `swapTwoDoubles(_:_:)` functions are identical. The only difference is the type of the values that they accept (`Int`, `String`, and `Double`).*

`swapTwoInts(_:_:)`, `swapTwoStrings(_:_:)` 및 `swapTwoDoubles(_:_:)` 함수의 본문이 동일하다는 것을 알아보았을 겁니다. 유일한 차이점은 허용하는 값의 타입(`Int`, `String` 및 `Double`)입니다.

*It’s more useful, and considerably more flexible, to write a single function that swaps two values of any type. Generic code enables you to write such a function. (A generic version of these functions is defined below.)*

모든 타입의 두 값을 교환하는 단일 함수를 작성하는 것이 더 유용하고 훨씬 더 유연합니다. 제네릭 코드를 사용하면 이러한 함수를 작성할 수 있습니다. (이러한 함수의 일반 버전은 아래에 정의되어 있습니다.)

> *NOTE*
> 
> *In all three functions, the types of `a` and `b` must be the same. If `a` and `b` aren’t of the same type, it isn’t possible to swap their values. Swift is a type-safe language, and doesn’t allow (for example) a variable of type `String` and a variable of type `Double` to swap values with each other. Attempting to do so results in a compile-time error.*
> 
> 세 함수 모두에서 `a`와 `b`의 타입이 동일해야 합니다. `a`와 `b`가 같은 타입이 아닌 경우 값을 교환할 수 없습니다. Swift는 타입에 안전한 언어이며 예를 들어 `String` 타입의 변수와 `Double` 타입의 변수가 서로 값을 교환하는 것을 허용하지 않습니다. 그렇게 하려고 하면 컴파일 타임 오류가 발생합니다.
