### *Function Types : 함수 타입*

*The access level for a function type is calculated as the most restrictive access level of the function’s parameter types and return type. You must specify the access level explicitly as part of the function’s definition if the function’s calculated access level doesn’t match the contextual default.*

함수 타입에 대한 액세스 레벨은 함수의 매개 변수 타입 및 반환 타입 중 가장 제한적인 액세스 레벨로 계산됩니다. 함수의 계산된 액세스 레벨이 상황별 기본값과 일치하지 않으면 함수 정의의 일부로 액세스 레벨을 명시적으로 지정해야 합니다.

*The example below defines a global function called `someFunction()`, without providing a specific access-level modifier for the function itself. You might expect this function to have the default access level of “internal”, but this isn’t the case. In fact, `someFunction()` won’t compile as written below:*

아래 예는 함수 자체에 대한 특정 액세스 레벨 제어자를 제공하지 않고 `someFunction()`이라는 전역 함수를 정의합니다. 이 기능의 기본 액세스 레벨이 "내부"일 것으로 예상할 수 있지만 그렇지 않습니다. 사실 `someFunction()`은 아래와 같이 컴파일되지 않습니다.

```swift
func someFunction() -> (SomeInternalClass, SomePrivateClass) {
    // function implementation goes here
}
```

*The function’s return type is a tuple type composed from two of the custom classes defined above in [Custom Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol#Custom-Types). One of these classes is defined as internal, and the other is defined as private. Therefore, the overall access level of the compound tuple type is private (the minimum access level of the tuple’s constituent types).*

함수의 반환 타입은 위의 [링크]에서 정의한 두 개의 사용자 지정 클래스로 구성된 튜플 타입입니다. 이러한 클래스 중 하나는 내부로 정의되고 다른 하나는 프라이빗으로 정의됩니다. 따라서 복합 튜플 타입의 전체 엑세스 레벨은 프라이빗(튜플 구성 타입의 최소 접근 레벨)입니다.

*Because the function’s return type is private, you must mark the function’s overall access level with the `private` modifier for the function declaration to be valid:*

함수의 반환 타입이 프라이빗이므로 함수 선언이 유효하려면 함수의 전체 액세스 레벨을 `private` 제어자로 표시해야 합니다.

```swift
private func someFunction() -> (SomeInternalClass, SomePrivateClass) {
    // function implementation goes here
}
```

*It’s not valid to mark the definition of `someFunction()` with the `public` or `internal` modifiers, or to use the default setting of internal, because public or internal users of the function might not have appropriate access to the private class used in the function’s return type.*

`someFunction()`의 정의를 `public` 또는 `internal` 제어자로 표시하거나 함수의 공용 또는 내부 사용자가 함수의 반환 타입에 사용되는 개인 클래스에 대한 적절한 액세스 권한을 갖지 못할 수 있기 때문에 내부의 기본 설정을 사용합니다.
