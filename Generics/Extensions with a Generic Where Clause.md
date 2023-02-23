## *Extensions with a Generic Where Clause : 제네릭 Where 절이 있는 확장*

*You can also use a generic `where` clause as part of an extension. The example below extends the generic `Stack` structure from the previous examples to add an `isTop(_:)` method.*

확장의 일부로 제네릭 `where` 절을 사용할 수도 있습니다. 아래 예는 이전 예에서 일반 `Stack` 구조를 확장하여 `isTop(_:)` 메서드를 추가합니다.

```swift
extension Stack where Element: Equatable {
    func isTop(_ item: Element) -> Bool {
        guard let topItem = items.last else {
            return false
        }
        return topItem == item
    }
}
```

*This new `isTop(_:)` method first checks that the stack isn’t empty, and then compares the given item against the stack’s topmost item. If you tried to do this without a generic `where` clause, you would have a problem: The implementation of `isTop(_:)` uses the `==` operator, but the definition of `Stack` doesn’t require its items to be equatable, so using the `==` operator results in a compile-time error. Using a generic `where` clause lets you add a new requirement to the extension, so that the extension adds the `isTop(_:)` method only when the items in the stack are equatable.*

이 새로운 `isTop(_:)` 메서드는 먼저 스택이 비어 있지 않은지 확인한 다음 주어진 항목을 스택의 최상위 항목과 비교합니다. 일반적인 `where` 절 없이 이 작업을 시도하면 문제가 발생합니다. `isTop(_:)`의 구현은 `==` 연산자를 사용하지만 `Stack`의 정의에는 항목이 동일하므로 `==` 연산자를 사용하면 컴파일 타임 오류가 발생합니다. 제네릭 `where` 절을 사용하면 확장에 새 요구 사항을 추가할 수 있으므로 스택의 항목이 동등할 때만 확장이 `isTop(_:)` 메서드를 추가합니다.

*Here’s how the `isTop(_:)` method looks in action:*

다음은 `isTop(_:)` 방법이 작동하는 모습입니다.

```swift
if stackOfStrings.isTop("tres") {
    print("Top element is tres.")
} else {
    print("Top element is something else.")
}
// Prints "Top element is tres."
```

*If you try to call the `isTop(_:)` method on a stack whose elements aren’t equatable, you’ll get a compile-time error.*

요소가 동일하지 않은 스택에서 `isTop(_:)` 메서드를 호출하려고 하면 컴파일 타임 오류가 발생합니다.

```swift
struct NotEquatable { }
var notEquatableStack = Stack<NotEquatable>()
let notEquatableValue = NotEquatable()
notEquatableStack.push(notEquatableValue)
notEquatableStack.isTop(notEquatableValue)  // Error
```

*You can use a generic `where` clause with extensions to a protocol. The example below extends the `Container` protocol from the previous examples to add a `startsWith(_:)` method.*

프로토콜 확장과 함께 제네릭 `where` 절을 사용할 수 있습니다. 아래 예시는 이전 예시의 `Container` 프로토콜을 확장하여 `startsWith(_:)` 메서드를 추가합니다.

```swift
extension Container where Item: Equatable {
    func startsWith(_ item: Item) -> Bool {
        return count >= 1 && self[0] == item
    }
}
```

*The `startsWith(_:)` method first makes sure that the container has at least one item, and then it checks whether the first item in the container matches the given item. This new `startsWith(_:)` method can be used with any type that conforms to the `Container` protocol, including the stacks and arrays used above, as long as the container’s items are equatable.*

`startsWith(_:)` 메서드는 먼저 컨테이너에 항목이 하나 이상 있는지 확인한 다음 컨테이너의 첫 번째 항목이 지정된 항목과 일치하는지 확인합니다. 이 새로운 `startsWith(_:)` 메소드는 컨테이너의 항목이 동일하다면 위에서 사용된 스택 및 배열을 포함하여 `Container` 프로토콜을 준수하는 모든 타입과 함께 사용할 수 있습니다.

```swift
if [9, 9, 9].startsWith(42) {
    print("Starts with 42.")
} else {
    print("Starts with something else.")
}
// Prints "Starts with something else."
```

*The generic `where` clause in the example above requires `Item` to conform to a protocol, but you can also write a generic `where` clauses that require `Item` to be a specific type. For example:*

위의 예에서 제네릭 `where` 절은 프로토콜을 준수하기 위해 `Item`이 필요하지만 `Item`이 특정 타입이어야 하는 제네릭 `where` 절을 작성할 수도 있습니다. 예를 들어:

```swift
extension Container where Item == Double {
    func average() -> Double {
        var sum = 0.0
        for index in 0..<count {
            sum += self[index]
        }
        return sum / Double(count)
    }
}
print([1260.0, 1200.0, 98.6, 37.0].average())
// Prints "648.9"
```

*This example adds an `average()` method to containers whose `Item` type is `Double`. It iterates over the items in the container to add them up, and divides by the container’s count to compute the average. It explicitly converts the count from `Int` to `Double` to be able to do floating-point division.*

이 예시는 `Item` 타입이 `Double`인 컨테이너에 `average()` 메서드를 추가합니다. 컨테이너의 항목을 반복하여 더하고 컨테이너의 수로 나누어 평균을 계산합니다. 부동 소수점 나눗셈을 수행할 수 있도록 개수를 명시적으로 `Int`에서 `Double`로 변환합니다.

*You can include multiple requirements in a generic `where` clause that’s part of an extension, just like you can for a generic `where` clause that you write elsewhere. Separate each requirement in the list with a comma.*

다른 곳에 작성하는 일반적인 `where` 절과 마찬가지로 확장의 일부인 제네릭 `where` 절에 여러 요구 사항을 포함할 수 있습니다. 목록의 각 요구 사항을 쉼표로 구분합니다.
