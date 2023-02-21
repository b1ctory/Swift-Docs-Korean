## *Type Constraints : 타입 제약조건*

*The `swapTwoValues(_:_:)` function and the `Stack` type can work with any type. However, it’s sometimes useful to enforce certain type constraints on the types that can be used with generic functions and generic types. Type constraints specify that a type parameter must inherit from a specific class, or conform to a particular protocol or protocol composition.*

`swapTwoValues(_:)` 함수와 `Stack` 타입은 모든 타입에서 사용할 수 있습니다. 그러나 제네릭 함수 및 제네릭 타입과 함께 사용할 수 있는 타입에 특정 타입 제약 조건을 적용하는 것이 유용할 수 있습니다. 타입 제약 조건은 타입 매개 변수가 특정 클래스에서 상속되거나 특정 프로토콜 또는 프로토콜 구성을 준수해야 함을 지정합니다.

*For example, Swift’s `Dictionary` type places a limitation on the types that can be used as keys for a dictionary. As described in [Dictionaries](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Dictionaries), the type of a dictionary’s keys must be hashable. That is, it must provide a way to make itself uniquely representable. `Dictionary` needs its keys to be hashable so that it can check whether it already contains a value for a particular key. Without this requirement, `Dictionary` couldn’t tell whether it should insert or replace a value for a particular key, nor would it be able to find a value for a given key that’s already in the dictionary.*

예를 들어, Swift의 `Dictionary` 타입은 딕셔너리의 키로 사용할 수 있는 타입에 제한을 둡니다. [링크]에 설명된 바와 같이, 딕셔너리의 키 타입은 해시 가능해야 합니다. 즉, `Dictionary`는 특정 키에 대한 값을 이미 포함하고 있는지 여부를 확인할 수 있도록 해시 가능한 키여야 합니다. 이 요구 사항이 없으면 `Dictionary`은 특정 키에 대한 값을 삽입해야 하는지 대체해야 하는지 알 수 없었고, 딕셔너리에 이미 있는 특정 키에 대한 값을 찾을 수도 없었습니다.

*This requirement is enforced by a type constraint on the key type for `Dictionary`, which specifies that the key type must conform to the `Hashable` protocol, a special protocol defined in the Swift standard library. All of Swift’s basic types (such as `String`, `Int`, `Double`, and `Bool`) are hashable by default. For information about making your own custom types conform to the `Hashable` protocol, see [Conforming to the Hashable Protocol](https://developer.apple.com/documentation/swift/hashable#2849490).*

이 요구 사항은 키 타입이 Swift 표준 라이브러리에 정의된 특수 프로토콜인 `Dictionary` 프로토콜을 준수해야 함을 지정하는 `Dictionary`의 키 타입에 대한 타입 제약 조건에 의해 시행됩니다. Swift의 모든 기본 타입(예: `String`, `Int`, `Double`, `Boolen`)은 기본적으로 해시 가능합니다. 사용자 정의 타입을 `Hashable` 프로토콜과 일치시키는 방법에 대한 자세한 내용은 [링크]를 참고하세요.

*You can define your own type constraints when creating custom generic types, and these constraints provide much of the power of generic programming. Abstract concepts like `Hashable` characterize types in terms of their conceptual characteristics, rather than their concrete type.*

사용자 정의 제네릭 타입을 만들 때 사용자 정의 타입 제약 조건을 정의할 수 있으며 이러한 제약 조건은 제네릭 프로그래밍의 많은 기능을 제공합니다. `Hashable`과 같은 추상적 개념은 구체적인 타입보다는 개념적인 특성으로 타입을 특징짓습니다.

### *Type Constraint Syntax : 타입 제약 조건 구문*

*You write type constraints by placing a single class or protocol constraint after a type parameter’s name, separated by a colon, as part of the type parameter list. The basic syntax for type constraints on a generic function is shown below (although the syntax is the same for generic types):*

타입 제약 조건은 타입 매개 변수 이름 뒤에 단일 클래스 또는 프로토콜 제약 조건을 배치하고 타입 매개 변수 목록의 일부로 콜론으로 구분하여 작성합니다. 일반 함수에 대한 타입 제약 조건의 기본 구문은 아래와 같습니다. (제네릭 타입에 대한 구문은 동일합니다)

```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // function body goes here
}
```

*The hypothetical function above has two type parameters. The first type parameter, `T`, has a type constraint that requires `T` to be a subclass of `SomeClass`. The second type parameter, `U`, has a type constraint that requires `U` to conform to the protocol `SomeProtocol`.*

위의 가상 함수에는 두 가지 타입 매개 변수가 있습니다. 첫 번째 타입 매개 변수인 `T`는 `T`가 `SomeClass`의 하위 클래스여야 하는 타입 제약 조건을 가지고 있습니다. 두 번째 타입 매개 변수 `U`는 프로토콜 `SomeProtocol`을 준수해야 하는 타입 제약 조건을 가지고 있습니다.

### *Type Constraints in Action : 실행 중인 타입 제약조건*

*Here’s a nongeneric function called `findIndex(ofString:in:)`, which is given a `String` value to find and an array of `String` values within which to find it. The `findIndex(ofString:in:)` function returns an optional `Int` value, which will be the index of the first matching string in the array if it’s found, or `nil` if the string can’t be found:*

다음은 `findIndex(ofString:in:)`이라는 비제네릭 함수로, 찾을 `String` 값과 찾을 수 있는 `String` 값의 배열이 제공됩니다. `findIndex(ofString:in:)` 함수는 옵셔널 `Int` 값을 반환합니다. 이 값은 배열에서 일치하는 첫 번째 문자열이 있는 경우 인덱스가 되고 문자열을 찾을 수 없는 경우 `nil`이 됩니다.

```swift
func findIndex(ofString valueToFind: String, in array: [String]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}
```

*The `findIndex(ofString:in:)` function can be used to find a string value in an array of strings:*

`findIndex(ofString:in:)` 함수는 문자열 배열에서 문자열 값을 찾는 데 사용할 수 있습니다.

```swift
let strings = ["cat", "dog", "llama", "parakeet", "terrapin"]
if let foundIndex = findIndex(ofString: "llama", in: strings) {
    print("The index of llama is \(foundIndex)")
}
// Prints "The index of llama is 2"The principle of finding the index of a value in an array isn’t useful only for strings, however. You can write the same functionality as a generic function by replacing any mention of strings with values of some type `T` instead.
```

*Here’s how you might expect a generic version of `findIndex(ofString:in:)`, called `findIndex(of:in:)`, to be written. Note that the return type of this function is still `Int?`, because the function returns an optional index number, not an optional value from the array. Be warned, though — this function doesn’t compile, for reasons explained after the example:*

다음은 `findIndex(of:in:)`라고 하는 `findIndex(ofString:in:)`의 제네릭 버전이 작성되는 방식입니다. 이 함수의 반환 타입은 여전히 ​​`Int?`입니다. 함수가 배열의 옵셔널 값이 아니라 옵셔널 인덱스 번호를 반환하기 때문입니다. 그러나 주의하세요- 이 함수는 예제 뒤에 설명된 이유 때문에 컴파일되지 않습니다.

```swift
func findIndex<T>(of valueToFind: T, in array:[T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}
```

*This function doesn’t compile as written above. The problem lies with the equality check, “`if value == valueToFind`”. Not every type in Swift can be compared with the equal to operator (`==`). If you create your own class or structure to represent a complex data model, for example, then the meaning of “equal to” for that class or structure isn’t something that Swift can guess for you. Because of this, it isn’t possible to guarantee that this code will work for every possible type `T`, and an appropriate error is reported when you try to compile the code.*

이 함수는 위에 쓴 것처럼 컴파일되지 않습니다. 문제는 `"if value == value To Find"`라는 동일성 검사에 있습니다. Swift의 모든 타입을 연산자와 동일한 타입(`==`)과 비교할 수 있는 것은 아닙니다. 예를 들어, 복잡한 데이터 모델을 나타내기 위해 자신만의 클래스나 구조체를 만드는 경우, 해당 클래스나 구조체에 대한 "같음"의 의미는 Swift가 추측할 수 있는 것이 아닙니다. 이 때문에 이 코드가 가능한 모든 타입의 `T`에 대해 작동한다고 보장할 수 없으며 코드를 컴파일하려고 할 때 적절한 오류가 보고됩니다.

*All is not lost, however. The Swift standard library defines a protocol called `Equatable`, which requires any conforming type to implement the equal to operator (`==`) and the not equal to operator (`!=`) to compare any two values of that type. All of Swift’s standard types automatically support the `Equatable` protocol.*

그러나 모든 것이 사라진 것은 아닙니다. Swift 표준 라이브러리는 `Equatable`이라는 프로토콜을 정의합니다. 이 프로토콜은 모든 적합한 타입이 동등한 연산자(`==`)와 그렇지 않은 연산자(`!=`)를 구현하여 해당 타입의 두 값을 비교해야 합니다. Swift의 모든 표준 타입은 자동으로 `Equatable` 프로토콜을 지원합니다.

*Any type that’s `Equatable` can be used safely with the `findIndex(of:in:)` function, because it’s guaranteed to support the equal to operator. To express this fact, you write a type constraint of `Equatable` as part of the type parameter’s definition when you define the function:*

`Equatable`인 모든 타입은 `findIndex(of:in:)` 함수와 함께 안전하게 사용할 수 있습니다. 이 함수는 등호 연산자를 지원하기 때문입니다. 이 사실을 표현하기 위해 함수를 정의할 때 타입 매개 변수 정의의 일부로 `Equatable` 타입 제약 조건을 작성합니다:

```swift
func findIndex<T: Equatable>(of valueToFind: T, in array:[T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}
```

*The single type parameter for `findIndex(of:in:)` is written as `T: Equatable`, which means “any type `T` that conforms to the `Equatable` protocol.”*

`findIndex(of:in:)`의 단일 타입 매개 변수는 `T: Equatable`로 작성되며, 이는 `Equatable` 프로토콜을 준수하는 모든 타입의 `T`를 의미합니다.

*The `findIndex(of:in:)` function now compiles successfully and can be used with any type that’s `Equatable`, such as `Double` or `String`:*

`findIndex(of:in:)`함수는 이제 성공적으로 컴파일되며 `Double` 또는 `String`과 같이 `Equatable`인 모든 타입과 함께 사용할 수 있습니다:

```swift
let doubleIndex = findIndex(of: 9.3, in: [3.14159, 0.1, 0.25])
// doubleIndex is an optional Int with no value, because 9.3 isn't in the array
let stringIndex = findIndex(of: "Andrea", in: ["Mike", "Malcolm", "Andrea"])
// stringIndex is an optional Int containing a value of 2
```
