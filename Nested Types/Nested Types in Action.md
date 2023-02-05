## *Nested Types in Action*

*The example below defines a structure called `BlackjackCard`, which models a playing card as used in the game of Blackjack. The `BlackjackCard` structure contains two nested enumeration types called `Suit` and `Rank`.*

아래 예시는 블랙잭 게임에 사용되는 플레이 카드를 모델로 하는 `BlackjackCard`라는 구조체를 정의하고 있습니다. `BlackjackCard` 구조체에는 `Suit`와 `Rank`라는 두 가지 중첩 열거형이 포함되어 있습니다.

*In Blackjack, the Ace cards have a value of either one or eleven. This feature is represented by a structure called `Values`, which is nested within the `Rank` enumeration:*

블랙잭에서 에이스 카드의 값은 1 또는 11입니다. 이 기능은 `Rank` 열거 내에 중첩된 `Values`라는 구조체로 표시됩니다:

```swift
struct BlackjackCard {

    // nested Suit enumeration
    enum Suit: Character {
        case spades = "♠", hearts = "♡", diamonds = "♢", clubs = "♣"
    }

    // nested Rank enumeration
    enum Rank: Int {
        case two = 2, three, four, five, six, seven, eight, nine, ten
        case jack, queen, king, ace
        struct Values {
            let first: Int, second: Int?
        }
        var values: Values {
            switch self {
            case .ace:
                return Values(first: 1, second: 11)
            case .jack, .queen, .king:
                return Values(first: 10, second: nil)
            default:
                return Values(first: self.rawValue, second: nil)
            }
        }
    }

    // BlackjackCard properties and methods
    let rank: Rank, suit: Suit
    var description: String {
        var output = "suit is \(suit.rawValue),"
        output += " value is \(rank.values.first)"
        if let second = rank.values.second {
            output += " or \(second)"
        }
        return output
    }
}
```

*The `Suit` enumeration describes the four common playing card suits, together with a raw `Character` value to represent their symbol.*

`Suit` 열거는 4개의 일반적인 플레이 카드 수트를 기호를 나타내는 원시 `Character` 값과 함께 설명합니다.

*The `Rank` enumeration describes the thirteen possible playing card ranks, together with a raw `Int` value to represent their face value. (This raw `Int` value isn’t used for the Jack, Queen, King, and Ace cards.)*

`Rank` 열거형은 13개의 가능한 플레이 카드 순위를 액면가를 나타내는 원시 `Int` 값과 함께 설명합니다. (이 원시 `Int` 값은 잭, 퀸, 킹 및 에이스 카드에 사용되지 않습니다.)

*As mentioned above, the `Rank` enumeration defines a further nested structure of its own, called `Values`. This structure encapsulates the fact that most cards have one value, but the Ace card has two values. The `Values` structure defines two properties to represent this:*

위에서 언급한 바와 같이, `Rank` 열거형은 `Values`라고 불리는 자체의 추가 중첩 구조를 정의합니다. 이 구조체는 대부분의 카드에 하나의 값이 있지만 에이스 카드에는 두 개의 값이 있다는 사실을 의미합니다. `Values` 구조체는 이를 나타내는 두 가지 프로퍼티를 정의합니다:

- *`first`, of type `Int`*
  
  `Int` 타입 `first`

- *`second`, of type `Int?`, or “optional `Int`”*
  
  `Int?` 타입 혹은 옵셔널 `Int` 타입 `second`

*`Rank` also defines a computed property, `values`, which returns an instance of the `Values` structure. This computed property considers the rank of the card and initializes a new `Values` instance with appropriate values based on its rank. It uses special values for `jack`, `queen`, `king`, and `ace`. For the numeric cards, it uses the rank’s raw `Int` value.*

`Rank`는 또한 연산 프로퍼티인 `values`를 정의하며, 이 프로퍼티는 `Values` 구조체의 인스턴스를 반환합니다. 이 연산 프로퍼티는 카드의 순위를 고려하고 순위에 따라 적절한 값으로 새 `Values` 인스턴스를 초기화합니다. 잭, 퀸, 킹, 에이스에 특별한 값을 사용합니다. 숫자 카드의 경우 순위의 원시 `Int` 값을 사용합니다.

*The `BlackjackCard` structure itself has two properties—`rank` and `suit`. It also defines a computed property called `description`, which uses the values stored in `rank` and `suit` to build a description of the name and value of the card. The `description` property uses optional binding to check whether there’s a second value to display, and if so, inserts additional description detail for that second value.*

`BlackjackCard` 구조체 자체는 `rank`와 `suit` 라는 두 가지 프로퍼티를 갖고 있습니다. 또한 `description`이라는 연산 프로퍼티를 정의하는데, 이 프로퍼티는 `rank`와 `suit`에 저장된 값을 사용하여 카드의 이름과 값에 대한 설명을 작성합니다. `description` 프로퍼티는 옵셔널 바인딩을 사용하여 표시할 두 번째 값이 있는지 확인하고, 있으면 해당 두 번째 값에 대한 추가 설명 세부 정보를 삽입합니다.

*Because `BlackjackCard` is a structure with no custom initializers, it has an implicit memberwise initializer, as described in [Memberwise Initializers for Structure Types](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID214). You can use this initializer to initialize a new constant called `theAceOfSpades`:*

`BlackjackCard`는 사용자 지정 이니셜라이저가 없는 구조체이므로 [링크]에서 설명한 대로 암묵적인 멤버별 이니셜라이저가 있습니다. 이 이니셜라이저를 사용하여 `theAceOfSpades`라는 새 상수를 초기화할 수 있습니다:

```swift
let theAceOfSpades = BlackjackCard(rank: .ace, suit: .spades)
print("theAceOfSpades: \(theAceOfSpades.description)")
// Prints "theAceOfSpades: suit is ♠, value is 1 or 11"
```

*Even though `Rank` and `Suit` are nested within `BlackjackCard`, their type can be inferred from context, and so the initialization of this instance is able to refer to the enumeration cases by their case names (`.ace` and `.spades`) alone. In the example above, the `description` property correctly reports that the Ace of Spades has a value of `1` or `11`.*

`Rank`와 `Suit`가 `BlackjackCard`내에 내포되어 있더라도 그들의 타입은 문맥으로 유추할 수 있으므로, 이 인스턴스의 초기화는 케이스 이름(`.ace` 와 `.spades`)만으로 열거형 케이스를 참조할 수 있습니다. 위의 예에서 `description` 프로퍼티는 에이스 오브 스페이드의 값이 `1` 또는 `11`임을 올바르게 보고합니다.
