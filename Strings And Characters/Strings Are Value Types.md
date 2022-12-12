## *Strings Are Value Types : String은 값 타입이다.*

*Swift’s `String` type is a value type. If you create a new `String` value, that `String` value is copied when it’s passed to a function or method, or when it’s assigned to a constant or variable. In each case, a new copy of the existing `String` value is created, and the new copy is passed or assigned, not the original version. Value types are described in [Structures and Enumerations Are Value Types](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID88).*

Swift 의 문자열 타입은 값 타입입니다. 새 String 값을 생성하면 해당 String 값이 함수 혹은 메서드에 전달되거나 상수 혹은 변수에 할당될 때 복사됩니다. 각각의 경우 기존 String 값의 새 복사본이 생성되고 원본 버전이 아닌 새 복사본이 전달되거나 할당됩니다. 값 타입은 [링크]에 설명되어있습니다.

*Swift’s copy-by-default `String` behavior ensures that when a function or method passes you a `String` value, it’s clear that you own that exact `String` value, regardless of where it came from. You can be confident that the string you are passed won’t be modified unless you modify it yourself.*

Swift의 기본값인 `String` 동작은 함수가 메서드나 `String` 값을 전달할 때 출처에 상관없이 정확한 `String` 값을 소유한다는 것을 보장합니다. 전달된 문자열은 사용자가 직접 수정하지 않는 한 수정되지 않을 것이라고 확신할 수 있습니다.

*Behind the scenes, Swift’s compiler optimizes string usage so that actual copying takes place only when absolutely necessary. This means you always get great performance when working with strings as value types.*

Swift의 컴파일러는 반드시 필요한 경우에만 실제 복사가 이루어지도록 문자열 사용을 최적화합니다. 이는 문자열을 값 유형으로 사용할 때 항상 뛰어난 성능을 얻을 수 있음을 의미합니다.
