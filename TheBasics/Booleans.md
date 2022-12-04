## *Booleans*

*Swift has a basic Boolean type, called `Bool`. Boolean values are referred to as logical, because they can only ever be true or false. Swift provides two Boolean constant values, `true` and `false`:*

스위프트는 Bool이라고 불리는 Boolean기본타입을 가집니다. Boolean 값은참이거나 거짓일 수 있기 때문에 논리적 값이라고 합니다. 스위프트는 true와 false라는 두가지 Boolean 상수 값을 제공합니다.

```swift
let orangesAreOrange = true
let turnipsAreDelicious = false
```

*The types of `orangesAreOrange` and `turnipsAreDelicious` have been inferred as `Bool` from the fact that they were initialized with Boolean literal values. As with `Int` and `Double` above, you don’t need to declare constants or variables as `Bool` if you set them to `true` or `false` as soon as you create them. Type inference helps make Swift code more concise and readable when it initializes constants or variables with other values whose type is already known.*

orangesAreOrange와 tunipsAreDelicious 의 타입은 Bool 리터럴 값으로 초기화 되었다는 사실에서 Bool로 추론되었습니다. 위의 Int나 Double 처럼 상수나 변수를 생성하는 즉시 true나 false로 설정하면 Bool로 선언할 필요가 없습니다. 타입 추론은 타입이 이미 알려진 다른 값으로 상수나 변수를 초기화 할 때 스위프트 코드를 더 간결하고 읽기 쉽게 만드는데 도움이 됩니다.



*Boolean values are particularly useful when you work with conditional statements such as the `if` statement:*

Boolean 값은 if 문과 같은 조건문으로 작업할 때 특히 유용합니다.

```swift
if turnipsAreDelicious {
    print("Mmm, tasty turnips!")
} else {
    print("Eww, turnips are horrible.")
}
// Prints "Eww, turnips are horrible."
```

*Conditional statements such as the `if` statement are covered in more detail in [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html).*

if 문과 같은 조건문에 대해서는 [링크] 문서에서 자세히 설명합니다.

*Swift’s type safety prevents non-Boolean values from being substituted for `Bool`. The following example reports a compile-time error:*

Swift의 타입 안전성은 Bool값이 아닌 값이 Bool로 대체되는 것을 방지합니다. 다음 예제에서는 컴파일 타임에서의 오류를 보고합니다.

```swift
let i = 1

if i {
    // this example will not compile, and will report an error
}
```

*However, the alternative example below is valid:*

그러나 아래의 대안 예제는 유효합니다.

```swift
let i = 1

if i == 1 {
    // this example will compile successfully
}
```

*The result of the `i == 1` comparison is of type `Bool`, and so this second example passes the type-check. Comparisons like `i == 1` are discussed in [Basic Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html).*

i == 1의 비교 결과는 Bool 타입이므로 이 두번째 예는 타입 검사를 통과합니다. i == 1은 [링크] 에서 논의됩니다.



*As with other examples of type safety in Swift, this approach avoids accidental errors and ensures that the intention of a particular section of code is always clear.*

스위프트의 다른 타입 안전성 사례와 마찬가지로 이 접근 방식은 우발적인 오류를 방지하고 코드의 특정 섹션의 의도가 항상 명확함을 보장합니다.
