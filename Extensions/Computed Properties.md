## *Computed Properties : 연산 프로퍼티*

*Extensions can add computed instance properties and computed type properties to existing types. This example adds five computed instance properties to Swift’s built-in `Double` type, to provide basic support for working with distance units:*

확장 기능은 기존 유형에 계산된 인스턴스(instance) 프로퍼티와 연산 타입 프로퍼티를 추가할 수 있습니다. 이 예에서는 거리 단위 작업에 대한 기본적인 지원을 제공하기 위해 Swift의 내장 `Double` 타입에 5개의 연산 인스턴스 프로퍼티를 추가합니다:

```swift
extension Double {
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
    var mm: Double { return self / 1_000.0 }
    var ft: Double { return self / 3.28084 }
}
let oneInch = 25.4.mm
print("One inch is \(oneInch) meters")
// Prints "One inch is 0.0254 meters"
let threeFeet = 3.ft
print("Three feet is \(threeFeet) meters")
// Prints "Three feet is 0.914399970739201 meters"
```

*These computed properties express that a `Double` value should be considered as a certain unit of length. Although they’re implemented as computed properties, the names of these properties can be appended to a floating-point literal value with dot syntax, as a way to use that literal value to perform distance conversions.*

이러한 연산 프로퍼티는 `Double` 값을 특정 길이 단위로 간주해야 함을 나타냅니다. 연산 프로퍼티로 구현되지만 이러한 프로퍼티의 이름은 거리 변환을 수행하는 데 리터럴 값을 사용하는 방법으로 점 구문을 사용하여 부동 소수점 리터럴 값에 추가할 수 있습니다.

*In this example, a `Double` value of `1.0` is considered to represent “one meter”. This is why the `m` computed property returns `self`—the expression `1.m` is considered to calculate a `Double` value of `1.0`.*

이 예에서는 `Double` 값이 `1.0`이면 "1m"를 나타내는 것으로 간주됩니다. 이것이 `m` 연산 프로퍼티가 `self`를 반환하는 이유입니다. 표현 `1.m`은 `Double` 값 `1.0`을 계산하는 것으로 간주됩니다.

*Other units require some conversion to be expressed as a value measured in meters. One kilometer is the same as 1,000 meters, so the `km` computed property multiplies the value by `1_000.00` to convert into a number expressed in meters. Similarly, there are 3.28084 feet in a meter, and so the `ft` computed property divides the underlying `Double` value by `3.28084`, to convert it from feet to meters.*

다른 단위는 미터로 측정된 값으로 표현하기 위해 약간의 변환이 필요합니다. 1km는 1,000m와 동일하기 때문에 연산 프로퍼티 `km` 는 값에 `1_000.00`을 곱하여 미터로 표시된 숫자로 변환합니다. 마찬가지로 1미터에는 3.28084피트가 있으므로 연산 프로퍼티 `ft`는 피트에서 미터로 변환하기 위해 `Double` 값을 `3.28084`으로 나눕니다.

*These properties are read-only computed properties, and so they’re expressed without the `get` keyword, for brevity. Their return value is of type `Double`, and can be used within mathematical calculations wherever a `Double` is accepted:*

이러한 프로퍼티는 읽기 전용 연산 프로퍼티이므로 간결성을 위해 `get` 키워드 없이 표현됩니다. 이들의 반환 값은 `Double` 타입이며, `Double`이 허용되는 곳이라면 어디서나 수학적 계산에 사용할 수 있습니다:

```swift
let aMarathon = 42.km + 195.m
print("A marathon is \(aMarathon) meters long")
// Prints "A marathon is 42195.0 meters long"
```

> *NOTE*
> 
> *Extensions can add new computed properties, but they can’t add stored properties, or add property observers to existing properties.*
> 
> 확장은 새 연산 프로퍼티를 추가할 수 있지만 저장 프로퍼티를 추가하거나 기존 프로퍼티에 프로퍼티 옵저버를 추가할 수 없습니다.


