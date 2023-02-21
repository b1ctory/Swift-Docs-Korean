## *Extending a Generic Type : 제네릭 타입 확장*

*When you extend a generic type, you don’t provide a type parameter list as part of the extension’s definition. Instead, the type parameter list from the original type definition is available within the body of the extension, and the original type parameter names are used to refer to the type parameters from the original definition.*

제네릭 타입을 확장할 때 타입 매개 변수 목록을 확장 정의의 일부로 제공하지 않습니다. 대신 원래 타입 정의의 타입 매개 변수 목록을 확장자 본문 내에서 사용할 수 있으며, 원래 타입 매개 변수 이름은 원래 정의의 타입 매개 변수를 참조하는 데 사용됩니다.

*The following example extends the generic `Stack` type to add a read-only computed property called `topItem`, which returns the top item on the stack without popping it from the stack:*

다음 예제는 일반적인 `Stack` 타입을 확장하여 `topItem`이라는 읽기 전용 연산 프로퍼티를 추가합니다. 이 프로퍼티는 스택에서 상위 항목을 팝 하지 않고 반환합니다:

```swift
extension Stack {
    var topItem: Element? {
        return items.isEmpty ? nil : items[items.count - 1]
    }
}
```

*The `topItem` computed property can now be used with any `Stack` instance to access and query its top item without removing it.*

이제 `topItem` 연산 프로퍼티를 `Stack` 인스턴스와 함께 사용하여 제거하지 않고도 상위 항목에 액세스하고 쿼리할 수 있습니다.

```swift
if let topItem = stackOfStrings.topItem {
    print("The top item on the stack is \(topItem).")
}
// Prints "The top item on the stack is tres."Extensions of a generic type can also include requirements that instances of the extended type must satisfy in order to gain the new functionality, as discussed in [Extensions with a Generic Where Clause](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Extensions-with-a-Generic-Where-Clause) below.
```

*Extensions of a generic type can also include requirements that instances of the extended type must satisfy in order to gain the new functionality, as discussed in [Extensions with a Generic Where Clause](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Extensions-with-a-Generic-Where-Clause) below.*

제네릭 타입의 확장에는 아래의 [링크]에서 설명한 바와 같이 확장 타입의 인스턴스가 새로운 기능을 얻기 위해 충족해야 하는 요구 사항도 포함될 수 있습니다. 
