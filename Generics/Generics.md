# *Generics : 제네릭*

*Generic code enables you to write flexible, reusable functions and types that can work with any type, subject to requirements that you define. You can write code that avoids duplication and expresses its intent in a clear, abstracted manner.*

제네릭 코드를 사용하면 정의한 요구사항에 따라 모든 타입에서 작동할 수 있는 유연하고 재사용 가능한 함수 및 타입을 작성할 수 있습니다. 중복을 피하고 명확하고 추상적인 방식으로 의도를 표현하는 코드를 작성할 수 있습니다.

*Generics are one of the most powerful features of Swift, and much of the Swift standard library is built with generic code. In fact, you’ve been using generics throughout the Language Guide, even if you didn’t realize it. For example, Swift’s `Array` and `Dictionary` types are both generic collections. You can create an array that holds `Int` values, or an array that holds `String` values, or indeed an array for any other type that can be created in Swift. Similarly, you can create a dictionary to store values of any specified type, and there are no limitations on what that type can* be.

제네릭은 Swift의 가장 강력한 기능 중 하나이며, Swift 표준 라이브러리의 대부분은 제네릭 코드로 빌드됩니다. 사실, 인식하지 못하더라도 언어 가이드 전체에서 제네릭을 사용하고 있습니다. 예를 들어 Swift의 `Array` 및 `Dictionary` 타입은 모두 일반 컬렉션입니다. `Int` 값을 포함하는 배열, `String` 값을 포함하는 배열 또는 실제로 Swift에서 생성할 수 있는 다른 타입의 배열을 만들 수 있습니다. 마찬가지로 지정된 타입의 값을 저장하는 딕셔너리를 만들 수 있으며 해당 타입에 대한 제한이 없습니다.
