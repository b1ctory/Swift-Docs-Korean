## *Contextual Where Clauses: 상황별 Where 절*

*You can write a generic `where` clause as part of a declaration that doesn’t have its own generic type constraints, when you’re already working in the context of generic types. For example, you can write a generic `where` clause on a subscript of a generic type or on a method in an extension to a generic type. The `Container` structure is generic, and the `where` clauses in the example below specify what type constraints have to be satisfied to make these new methods available on a container.*

제네릭 타입의 컨텍스트에서 이미 작업 중인 경우 자체 제네릭 타입 제약이 없는 선언의 일부로 제네릭 `where` 절을 작성할 수 있습니다. 예를 들어 제네릭 타입의 서브스크립트 또는 제네릭 타입에 대한 확장 메서드에 제네릭 `where` 절을 작성할 수 있습니다. `Container` 구조체는 제네릭이며 아래 예의 `where` 절은 컨테이너에서 이러한 새 메서드를 사용할 수 있도록 충족해야 하는 타입 제약 조건을 지정합니다.

```swift
extension Container {
    func average() -> Double where Item == Int {
        var sum = 0.0
        for index in 0..<count {
            sum += Double(self[index])
        }
        return sum / Double(count)
    }
    func endsWith(_ item: Item) -> Bool where Item: Equatable {
        return count >= 1 && self[count-1] == item
    }
}
let numbers = [1260, 1200, 98, 37]
print(numbers.average())
// Prints "648.75"
print(numbers.endsWith(37))
// Prints "true"
```

*This example adds an `average()` method to `Container` when the items are integers, and it adds an `endsWith(_:)` method when the items are equatable. Both functions include a generic `where` clause that adds type constraints to the generic `Item` type parameter from the original declaration of `Container`.*

이 예는 항목이 정수일 때 `Container`에 `average()` 메서드를 추가하고 항목이 동일할 때 `endsWith(_:)` 메서드를 추가합니다. 두 함수 모두 `Container`의 원래 선언에서 일반 `Item` 유형 매개변수에 타입 제약을 추가하는 일반 `where` 절을 포함합니다.

*If you want to write this code without using contextual `where` clauses, you write two extensions, one for each generic `where` clause. The example above and the example below have the same behavior.*

문맥상 `where` 절을 사용하지 않고 이 코드를 작성하려면 각각의 제네릭 `where` 절에 대해 하나씩 두 개의 확장을 작성합니다. 위 예제와 아래 예제는 동작이 동일합니다.

```swift
extension Container where Item == Int {
    func average() -> Double {
        var sum = 0.0
        for index in 0..<count {
            sum += Double(self[index])
        }
        return sum / Double(count)
    }
}
extension Container where Item: Equatable {
    func endsWith(_ item: Item) -> Bool {
        return count >= 1 && self[count-1] == item
    }
}
```

*In the version of this example that uses contextual `where` clauses, the implementation of `average()` and `endsWith(_:)` are both in the same extension because each method’s generic `where` clause states the requirements that need to be satisfied to make that method available. Moving those requirements to the extensions’ generic `where` clauses makes the methods available in the same situations, but requires one extension per requirement.*

문맥상 `where` 절을 사용하는 이 예제의 버전에서 `average()`와 `endWith(_:)`의 구현은 각각의 방법의 일반적인 `where` 절이 해당 방법을 사용하기 위해 충족해야 하는 요구 사항을 명시하기 때문에 모두 동일한 확장에 있습니다. 이러한 요구 사항을 확장의 제네릭 `where` 절로 이동하면 동일한 상황에서 메서드를 사용할 수 있지만 요구 사항당 하나의 확장이 필요합니다.


