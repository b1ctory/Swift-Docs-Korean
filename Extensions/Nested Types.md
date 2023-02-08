## *Nested Types: 중첩 타입*

*Extensions can add new nested types to existing classes, structures, and enumerations:*

확장은 새 중첩 타입을 기존 클래스, 구조체 및 열거형에 추가할 수 있습니다.

```swift
extension Int {
    enum Kind {
        case negative, zero, positive
    }
    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
        }
    }
}
```

*This example adds a new nested enumeration to `Int`. This enumeration, called `Kind`, expresses the kind of number that a particular integer represents. Specifically, it expresses whether the number is negative, zero, or positive.*

이 예에서는 새 중첩 열거를 `Int`에 추가합니다. `Kind`라고 하는 이 열거형은 특정 정수가 나타내는 숫자의 종류를 나타냅니다. 구체적으로, 숫자가 음수인지, 0인지, 양수인지를 나타냅니다.

*This example also adds a new computed instance property to `Int`, called `kind`, which returns the appropriate `Kind` enumeration case for that integer.*

또한 이 예에서는 `kind`라는 새로운 연산 인스턴스 프로퍼티를 `Int`에 추가하여 해당 정수에 대한 적절한 `Kind` 열거형 케이스를 반환합니다.

*The nested enumeration can now be used with any `Int` value:*

이제 중첩된 열거형을 모든 `Int` 값과 함께 사용할 수 있습니다:

```swift
func printIntegerKinds(_ numbers: [Int]) {
    for number in numbers {
        switch number.kind {
        case .negative:
            print("- ", terminator: "")
        case .zero:
            print("0 ", terminator: "")
        case .positive:
            print("+ ", terminator: "")
        }
    }
    print("")
}
printIntegerKinds([3, 19, -27, 0, -6, 0, 7])
// Prints "+ + - 0 - 0 + "
```

*This function, `printIntegerKinds(_:)`, takes an input array of `Int` values and iterates over those values in turn. For each integer in the array, the function considers the `kind` computed property for that integer, and prints an appropriate description.*

이 함수 `printIntegerKinds(_:)`는 Int 값의 배열 입력을 사용하고 해당 값에 대해 차례로 반복합니다. 배열의 각 정수에 대해 함수는 해당 정수에 대한 `kind` 연산 프로퍼티를 고려하고 적절한 설명을 인쇄합니다.

> *NOTE*
> 
> *`number.kind` is already known to be of type `Int.Kind`. Because of this, all of the `Int.Kind` case values can be written in shorthand form inside the `switch` statement, such as `.negative` rather than `Int.Kind.negative`.*
> 
> `number.kind`는 이미 `Int.Kind` 타입으로 알려져 있습니다. 이 때문에 `switch` 구문 내부에 속기로 쓰여진 모든 `Int.Kind`의 케이스가 사용될 수 있습니다, `Int.Kind.negative` 대신 `.negative` 같이


