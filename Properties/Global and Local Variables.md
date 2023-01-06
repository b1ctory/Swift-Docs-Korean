## *Global and Local Variables : 전역 및 지역 변수*

*The capabilities described above for computing and observing properties are also available to global variables and local variables. Global variables are variables that are defined outside of any function, method, closure, or type context. Local variables are variables that are defined within a function, method, or closure context.*

위에서 설명한 프로퍼티 연산 및 관찰 기능은 전역 변수 및 지역 변수에서도 사용할 수 있습니다. 전역 변수는 함수, 메서드, 클로저 또는 타입 컨텍스트 외부에서 정의된 변수입니다. 지역 변수는 함수, 메서드 또는 클로저 컨텍스트 내에서 정의된 변수입니다.

*The global and local variables you have encountered in previous chapters have all been stored variables. Stored variables, like stored properties, provide storage for a value of a certain type and allow that value to be set and retrieved.*

이전 장에서 접한 전역 변수와 로컬 변수는 모두 저장된 변수입니다. 저장된 변수는 저장 프로퍼티와 마찬가지로 특정 타입의 값에 대한 저장을 제공하고 해당 값을 설정하고 검색할 수 있습니다.

*However, you can also define computed variables and define observers for stored variables, in either a global or local scope. Computed variables calculate their value, rather than storing it, and they’re written in the same way as computed properties.*

그러나 전역 또는 지역 범위에서 연산 변수를 정의하고 저장된 변수에 대한 옵저버를 정의할 수도 있습니다. 연산된 변수는 값을 저장하지 않고 계산되며 연산 프로퍼티와 동일한 방식으로 작성됩니다.

> *NOTE*
> 
> *Global constants and variables are always computed lazily, in a similar manner to [Lazy Stored Properties](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID257). Unlike lazy stored properties, global constants and variables don’t need to be marked with the `lazy` modifier.*
> 
> 글로벌 상수 및 변수는 [Lazy Stored Properties](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#)와 유사한 방식으로 항상 느리게 계산됩니다. 저장 프로퍼티와 달리 전역 상수와 변수는 lazy 수식어로 표시할 필요가 없습니다.
> 
> *Local constants and variables are never computed lazily.*
> 
> 지역 상수와 변수는 결코 느리게 계산되지 않습니다.

*You can apply a property wrapper to a local stored variable, but not to a global variable or a computed variable. For example, in the code below, `myNumber` uses `SmallNumber` as a property wrapper.*

프로퍼티 래퍼를 지역 저장 변수에 적용할 수 있지만 전역 변수 또는 연산 변수에는 적용할 수 없습니다. 예를 들어 아래 코드에서 `MyNumber`는 `SmallNumber`를 프로퍼티 래퍼로 사용합니다.

```swift
func someFunction() {
    @SmallNumber var myNumber: Int = 0

    myNumber = 10
    // now myNumber is 10

    myNumber = 24
    // now myNumber is 12
}
```

*Like when you apply `SmallNumber` to a property, setting the value of `myNumber` to 10 i*s valid. Because the property wrapper doesn’t allow values higher than 12, it sets `myNumber` to 12 instead of 24.

프로퍼티에 `SmallNumber`를 적용할 때처럼 `myNumber`의 값을 10으로 설정하면 유효합니다. 프로퍼티 래퍼는 12보다 큰 값을 허용하지 않기 때문에 `myNumber`를 24가 아닌 12로 설정합니다.
