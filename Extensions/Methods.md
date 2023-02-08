## *Methods*

*Extensions can add new instance methods and type methods to existing types. The following example adds a new instance method called `repetitions` to the `Int` type:*

확장은 새 인스턴스 메서드 및 타입 메서드를 기존 타입에 추가할 수 있습니다. 다음 예제에서는 `repetitions`라는 새 인스턴스 메서드를 `Int` 타입에 추가합니다:

```swift
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}
```

*The `repetitions(task:)` method takes a single argument of type `() -> Void`, which indicates a function that has no parameters and doesn’t return a value.*

`repetitions(task:)` 메서드는 매개 변수가 없고 값을 반환하지 않는 함수를 나타내는 타입 `() -> 보이드`의 단일 인수를 사용합니다.

*After defining this extension, you can call the `repetitions(task:)` method on any integer to perform a task that many number of times:*

이 확장을 정의한 후에는 임의의 정수에서 `repetitions(task:)` 메서드를 호출하여 다음과 같은 횟수만큼 작업을 수행할 수 있습니다:

```swift
3.repetitions {
    print("Hello!")
}
// Hello!
// Hello!
// Hello!
```

### *Mutating Instance Methods : 인스턴스 메서드 변경*

*Instance methods added with an extension can also modify (or mutate) the instance itself. Structure and enumeration methods that modify `self` or its properties must mark the instance method as `mutating`, just like mutating methods from an original implementation.*

확장명과 함께 추가된 인스턴스 메서드는 인스턴스 자체를 수정(또는 *변환*)할 수도 있습니다. `self` 또는 그 프로퍼티를 수정하는 구조체 및 열거형 메서드는 원래 구현의 mutating 메서드와 마찬가지로 인스턴스 메서드를 `mutating`으로 표시해야 합니다.

*The example below adds a new mutating method called `square` to Swift’s `Int` type, which squares the original value:*

아래의 예는 원래 값을 제곱하는 Swift `Int` 타입의 `square`라는 새로운 mutating 메서드를 추가합니다:

```swift
extension Int {
    mutating func square() {
        self = self * self
    }
}
var someInt = 3
someInt.square()
// someInt is now 9
```
