## *Nil-Coalescing Operator*

*The nil-coalescing operator (`a ?? b`) unwraps an optional `a` if it contains a value, or returns a default value `b` if `a` is `nil`. The expression `a` is always of an optional type. The expression `b` must match the type that’s stored inside `a`.*

`nil-coalescing`연산자 (`a ?? b`) 는 값이 있으면 옵셔널 `a` 를 풀거나, `a`가 `nil`인 경우 기본값 `b`를 반환한다.  `a`라는 표현은 항상 옵셔널 타입입니다. 표현식 `b`는 `a`안에 저장된 유형과 일치해야 합니다.

*The nil-coalescing operator is shorthand for the code below:*

`nil-coalescing` 연산자느느 아래 코드의 줄임말입니다. 

```swift
a != nil ? a! : b
```

*The code above uses the ternary conditional operator and forced unwrapping (`a!`) to access the value wrapped inside `a` when `a` isn’t `nil`, and to return `b` otherwise. The nil-coalescing operator provides a more elegant way to encapsulate this conditional checking and unwrapping in a concise and readable form.*

위의 코드는 삼항 조건 연산자와 강재 언래핑 (`a!`)을 사용하여 `a`가 `nil`이 아닐 때 `a`안에 담긴 값에 엑세스하고, 그렇지 않으면 `b`를 반환합니다. 

> *NOTE*
> 
> *If the value of `a` is non-`nil`, the value of `b` isn’t evaluated. This is known as short-circuit evaluation.*
> 
> `a`의 값이 `nil` 이 아니면, `b`의 값은 평가되지 않습니다. 이것은 단락 평가라고 합니다.

*The example below uses the nil-coalescing operator to choose between a default color name and an optional user-defined color name:*

아래 예제에서는 `nil-coalescing` 연산자를 사용해서 기본 색상명과 옵셔널 사용자 정의 색상명의 중 하나를 선택합니다. 

```swift
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is nil, so colorNameToUse is set to the default of "red"
```

*The `userDefinedColorName` variable is defined as an optional `String`, with a default value of `nil`. Because `userDefinedColorName` is of an optional type, you can use the nil-coalescing operator to consider its value. In the example above, the operator is used to determine an initial value for a `String` variable called `colorNameToUse`. Because `userDefinedColorName` is `nil`, the expression `userDefinedColorName ?? defaultColorName` returns the value of `defaultColorName`, or `"red"`.*

 `userDefinedColorName` 변수는 디폴트 값을 nil로 가지는 옵셔널 String으로 정의되어있습니다.  `userDefinedColorName`은 옵셔널 타입이기 때문에 `nil-coalescing` 연산자를 사용하여 값을 고려할 수 있습니다. 위의 예시에서 연산자는 `colorNameToUse` 라는 `String` 변수의 초기 값을 결정하는데 사용됩니다.  `userDefinedColorName`이 nil이기 때문에  `userDefinedColorName ?? defaultColorName`  표현은 `defaultColorName` 혹은 `red` 라는 값을 반환합니다. 

*If you assign a non-`nil` value to `userDefinedColorName` and perform the nil-coalescing operator check again, the value wrapped inside `userDefinedColorName` is used instead of the default:*

만약 `userDefinedColorName`에 nil이 아닌 값을 할당하고 nil-coalescing 연산자를 다세 확인하면, `userDefinedColorName` 안에 있는 값이 기본값 대신 사용됩니다.

```swift
userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName isn't nil, so colorNameToUse is set to "green"
```
