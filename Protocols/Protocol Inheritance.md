## *Protocol Inheritance : 프로토콜 상속*

*A protocol can inherit one or more other protocols and can add further requirements on top of the requirements it inherits. The syntax for protocol inheritance is similar to the syntax for class inheritance, but with the option to list multiple inherited protocols, separated by commas:*

프로토콜은 하나 이상의 다른 프로토콜을 상속할 수 있으며 상속되는 요구사항 외에 추가 요구사항을 추가할 수 있습니다. 프로토콜 상속 구문은 클래스 상속 구문과 유사하지만 여러 개의 상속된 프로토콜을 쉼표로 구분하여 나열하는 옵션이 있습니다:

```swift
protocol InheritingProtocol: SomeProtocol, AnotherProtocol {
    // protocol definition goes here
}
```

*Here’s an example of a protocol that inherits the `TextRepresentable` protocol from above:*

다음은 위에서 `TextRepresentable` 프로토콜을 상속하는 프로토콜의 예입니다:

```swift
protocol PrettyTextRepresentable: TextRepresentable {
    var prettyTextualDescription: String { get }
}
```

*This example defines a new protocol, `PrettyTextRepresentable`, which inherits from `TextRepresentable`. Anything that adopts `PrettyTextRepresentable` must satisfy all of the requirements enforced by `TextRepresentable`, plus the additional requirements enforced by `PrettyTextRepresentable`. In this example, `PrettyTextRepresentable` adds a single requirement to provide a gettable property called `prettyTextualDescription` that returns a `String`.*

이 예에서는 `TextPresentable`에서 상속되는 새 프로토콜인 `PrettyTextPresentable`을 정의합니다. `PrettyTextRepresentable`을 채택하는 모든 항목은 `TextRepresentable`이 시행하는 모든 요구 사항과 `PrettyTextRepresentable`이 시행하는 추가 요구 사항을 충족해야 합니다. 이 예에서 `PrettyTextRepresentable`은 `String`을 반환하는 `prettyTextualDescription`라는 gettable 프로퍼티를 제공하기 위한 단일 요구 사항을 추가합니다.

*The `SnakesAndLadders` class can be extended to adopt and conform to `PrettyTextRepresentable`:*

`SnakesAndLadders` 클래스는 `PrettyTextRepresentable`을 채택하고 준수하도록 확장할 수 있습니다:

```swift
extension SnakesAndLadders: PrettyTextRepresentable {
    var prettyTextualDescription: String {
        var output = textualDescription + ":\n"
        for index in 1...finalSquare {
            switch board[index] {
            case let ladder where ladder > 0:
                output += "▲ "
            case let snake where snake < 0:
                output += "▼ "
            default:
                output += "○ "
            }
        }
        return output
    }
}
```

*This extension states that it adopts the `PrettyTextRepresentable` protocol and provides an implementation of the `prettyTextualDescription` property for the `SnakesAndLadders` type. Anything that’s `PrettyTextRepresentable` must also be `TextRepresentable`, and so the implementation of `prettyTextualDescription` starts by accessing the `textualDescription` property from the `TextRepresentable` protocol to begin an output string. It appends a colon and a line break, and uses this as the start of its pretty text representation. It then iterates through the array of board squares, and appends a geometric shape to represent the contents of each square:*

이 확장은 `PrettyTextRepresentable` 프로토콜을 채택하고 `SnakesAndLadders` 타입의 `prettyTextualDescription`프로퍼티의 구현을 제공한다고 명시합니다. `PrettyTextRepresentable`인 모든 항목은 또한 `TextRepresentable`이어야 하므로 `prettyTextualDescription`의 구현은 `TextRepresentable` 프로토콜에서 `textualDescription` 속성에 액세스하여 출력 문자열을 시작하는 것으로 시작됩니다. 콜론과 줄 바꿈을 추가하고 이를 pretty 텍스트 표현의 시작으로 사용합니다. 그런 다음 보드 사각형 배열을 반복하고 기하학적 모양을 추가하여 각 사각형의 내용을 나타냅니다.

- *If the square’s value is greater than `0`, it’s the base of a ladder, and is represented by `▲`.*
  
  사각형의 값이 `0`보다 큰 경우 사다리의 밑면이며 `▲`로 표시됩니다.

- *If the square’s value is less than `0`, it’s the head of a snake, and is represented by `▼`.*
  
  네모의 값이 `0` 미만이면 뱀의 머리이며 `▼`로 표시됩니다.

- *Otherwise, the square’s value is `0`, and it’s a “free” square, represented by `○`.*
  
  그렇지 않으면 사각형의 값은 `0`이고 `○`로 표시되는 'free' 사각형입니다.

*The `prettyTextualDescription` property can now be used to print a pretty text description of any `SnakesAndLadders` instance:*

`prettyTextualDescription` 프로퍼티를 사용하여 모든 `SnakesAndLadders` 인스턴스에 대한 pretty 텍스트 설명을 출력할 수 있습니다.

```swift
print(game.prettyTextualDescription)
// A game of Snakes and Ladders with 25 squares:
// ○ ○ ▲ ○ ○ ▲ ○ ○ ▲ ▲ ○ ○ ○ ▼ ○ ○ ○ ○ ▼ ○ ○ ▼ ○ ▼ ○
```
