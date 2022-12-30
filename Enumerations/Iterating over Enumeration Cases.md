## *Iterating over Enumeration Cases : 열거형 케이스 반복*

*For some enumerations, it’s useful to have a collection of all of that enumeration’s cases. You enable this by writing `: CaseIterable` after the enumeration’s name. Swift exposes a collection of all the cases as an `allCases` property of the enumeration type. Here’s an example:*

일부 열거형의 경우 해당 열거형의 모든 케이스를 수집하는 것이 유용합니다. 열거형 이름 뒤에 `:CaseItable`을 입력해서 이 기능을 활성화합니다. Swift는 모든 케이스의 컬렉션을 열거형의 `allCases` 속성으로 표시합니다.다음은 예시입니다:

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}
let numberOfChoices = Beverage.allCases.count
print("\(numberOfChoices) beverages available")
// Prints "3 beverages available"
```

*In the example above, you write `Beverage.allCases` to access a collection that contains all of the cases of the `Beverage` enumeration. You can use `allCases` like any other collection—the collection’s elements are instances of the enumeration type, so in this case they’re `Beverage` values. The example above counts how many cases there are, and the example below uses a `for`-`in` loop to iterate over all the cases.*

위의 예시에서는 `Beverage.allCases` 를 작성해서 `Beverage` 열거형의 모든 케이스를 포함하는 컬렉션에 엑세스합니다. 다른 컬렉션과 마찬가지로 `allCases`를 사용할 수 있습니다 - 컬렉션의 요소는 열거형 타입의 인스턴스이므로 이 경우에는 `Beverage` 값입니다. 위의 예는 케이스의 수를 세고, 아래의 예는 `for`-`in` 루프를 사용해서 모든 케이스에 대해 반복합니다.

```swift
for beverage in Beverage.allCases {
    print(beverage)
}
// coffee
// tea
// juice
```

*The syntax used in the examples above marks the enumeration as conforming to the [`CaseIterable`](https://developer.apple.com/documentation/swift/caseiterable) protocol. For information about protocols, see [Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).*

위의 예제에 사용된 구문은 열거가 [CaseIterable] 을 준수하는것으로 표시합니다. 프로토콜에 대한 자세한 내용은 [링크]를 참조하세요.


