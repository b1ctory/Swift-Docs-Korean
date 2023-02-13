## *Delegation : 위임*

*Delegation is a design pattern that enables a class or structure to hand off (or delegate) some of its responsibilities to an instance of another type. This design pattern is implemented by defining a protocol that encapsulates the delegated responsibilities, such that a conforming type (known as a delegate) is guaranteed to provide the functionality that has been delegated. Delegation can be used to respond to a particular action, or to retrieve data from an external source without needing to know the underlying type of that source.*

위임은 클래스 또는 구조체가 자신의 책임 중 일부를 다른 타입의 인스턴스에 인계(또는 위임)할 수 있도록 하는 설계 패턴입니다. 이 설계 패턴은 위임된 책임을 캡슐화하는 프로토콜을 정의하여 구현됩니다. 따라서 위임된 기능을 제공하는 적합한 타입 (위임자라고 함) 이 보장됩니다. 위임을 사용하여 특정 작업에 응답하거나 해당 원본의 기본 타입을 알 필요 없이 외부 원본에서 데이터를 검색할 수 있습니다.

*The example below defines two protocols for use with dice-based board games:*

아래 예제는 주사위 기반 보드 게임에서 사용하기 위한 두 가지 프로토콜을 정의합니다:

```swift
protocol DiceGame {
    var dice: Dice { get }
    func play()
}
protocol DiceGameDelegate: AnyObject {
    func gameDidStart(_ game: DiceGame)
    func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int)
    func gameDidEnd(_ game: DiceGame)
}
```

*The `DiceGame` protocol is a protocol that can be adopted by any game that involves dice.*

`DiceGame` 프로토콜은 주사위를 사용하는 모든 게임에서 채택할 수 있는 프로토콜입니다.

*The `DiceGameDelegate` protocol can be adopted to track the progress of a `DiceGame`. To prevent strong reference cycles, delegates are declared as weak references. For information about weak references, see [Strong Reference Cycles Between Class Instances](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID51). Marking the protocol as class-only lets the `SnakesAndLadders` class later in this chapter declare that its delegate must use a weak reference. A class-only protocol is marked by its inheritance from `AnyObject`, as discussed in [Class-Only Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html#ID281).*

`DiceGameDelegate` 프로토콜을 사용하여 `DiceGame`의 진행 상황을 추적할 수 있습니다. 강한 참조 주기를 방지하기 위해 델리게이트는 약한 참조로 선언됩니다. 약한 참조에 대한 자세한 내용은 [링크]를 참조하십시오. 프로토콜을 클래스 전용으로 표시하면 이 장의 뒷부분에 있는 `SnakesAndLadders` 클래스가 해당 위임자가 약한 참조를 사용해야 함을 선언할 수 있습니다. [링크]에서 설명한 바와 같이 클래스 전용 프로토콜은 `AnyObject`에서 상속된 것으로 표시됩니다.

*Here’s a version of the Snakes and Ladders game originally introduced in [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html). This version is adapted to use a `Dice` instance for its dice-rolls; to adopt the `DiceGame` protocol; and to notify a `DiceGameDelegate` about its progress:*

[링크]에서 처음 소개된 뱀과 사다리 게임 버전은 다음과 같습니다. 이 버전은 주사위 롤에 `Dice` 인스턴스를 사용하고, `DiceGame` 프로토콜을 채택하고, 진행 상황에 대해 `DiceGameDelegate`에게 알리도록 조정되었습니다:

```swift
class SnakesAndLadders: DiceGame {
    let finalSquare = 25
    let dice = Dice(sides: 6, generator: LinearCongruentialGenerator())
    var square = 0
    var board: [Int]
    init() {
        board = Array(repeating: 0, count: finalSquare + 1)
        board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
        board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
    }
    weak var delegate: DiceGameDelegate?
    func play() {
        square = 0
        delegate?.gameDidStart(self)
        gameLoop: while square != finalSquare {
            let diceRoll = dice.roll()
            delegate?.game(self, didStartNewTurnWithDiceRoll: diceRoll)
            switch square + diceRoll {
            case finalSquare:
                break gameLoop
            case let newSquare where newSquare > finalSquare:
                continue gameLoop
            default:
                square += diceRoll
                square += board[square]
            }
        }
        delegate?.gameDidEnd(self)
    }
}
```

*For a description of the Snakes and Ladders gameplay, see [Break](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID137).*

뱀과 사다리 게임에 대한 설명은 [링크]를 참조하십시오.

*This version of the game is wrapped up as a class called `SnakesAndLadders`, which adopts the `DiceGame` protocol. It provides a gettable `dice` property and a `play()` method in order to conform to the protocol. (The `dice` property is declared as a constant property because it doesn’t need to change after initialization, and the protocol only requires that it must be gettable.)*

이 버전의 게임은 주사위 게임 프로토콜을 채택한 뱀과 사다리라는 클래스로 포장됩니다. 프로토콜을 준수하기 위해 getable `dice` 프로퍼티와 `play()` 메서드를 제공합니다. (`dice` 프로퍼티는 초기화 후에 변경할 필요가 없으며 프로토콜은 반드시 gettable이어야 하기 때문에 상수 프로퍼티로으로 선언됩니다.)

*The Snakes and Ladders game board setup takes place within the class’s `init()` initializer. All game logic is moved into the protocol’s `play` method, which uses the protocol’s required `dice` property to provide its dice roll values.*

뱀과 사다리 게임 보드 설정은 클래스의 `init()` 이니셜라이저 내에서 이루어집니다. 모든 게임 로직은 프로토콜의 `play()` 메서드로 이동되며, 이 메서드는 프로토콜에 필요한 `dice` 프로퍼티를 사용하여 주사위 롤 값을 제공합니다.

*Note that the `delegate` property is defined as an optional `DiceGameDelegate`, because a delegate isn’t required in order to play the game. Because it’s of an optional type, the `delegate` property is automatically set to an initial value of `nil`. Thereafter, the game instantiator has the option to set the property to a suitable delegate. Because the `DiceGameDelegate` protocol is class-only, you can declare the delegate to be `weak` to prevent reference cycles.*

게임을 하기 위해 위임자가 필요하지 않기 때문에 `delegate` 프로퍼티는 옵셔널 `DiceGameDelegate`로 정의됩니다. 옵셔널 타입이므로 `delegate` 프로퍼티는 자동으로 초기 값인 `nil`로 설정됩니다. 그런 다음 게임 인스턴스 작성자는 적절한 위임자로 프로퍼티를 설정할 수 있습니다. `DiceGameDelegate` 프로토콜은 클래스 전용이므로 참조 주기를 방지하기 위해 위임자를 `weak`로 선언할 수 있습니다.

*`DiceGameDelegate` provides three methods for tracking the progress of a game. These three methods have been incorporated into the game logic within the `play()` method above, and are called when a new game starts, a new turn begins, or the game ends.*

`DiceGameDelegate`는 게임 진행 상황을 추적하는 세 가지 방법을 제공합니다. 이 세 가지 메서드는 위의 `play()` 메서드 내에서 게임 로직에 통합되어 새로운 게임이 시작되거나, 새로운 턴이 시작되거나, 게임이 종료될 때 호출됩니다.

*Because the `delegate` property is an optional `DiceGameDelegate`, the `play()` method uses optional chaining each time it calls a method on the delegate. If the `delegate` property is nil, these delegate calls fail gracefully and without error. If the `delegate` property is non-nil, the delegate methods are called, and are passed the `SnakesAndLadders` instance as a parameter.*

`delegate` 프로퍼티는 옵셔널 `DiceGameDelegate`이므로 `play()` 메서드는 위임자에게 메서드를 호출할 때마다 옵셔널 체인을 사용합니다. `delegate` 프로퍼티가 nil이면 이러한 위임 호출은 오류 없이 정상적으로 실패합니다. `delegate` 프로퍼티가 nil이 아닌 경우 대리 메서드가 호출되고 매개 변수로 `SnakesAndLaders` 인스턴스를 전달합니다.

*This next example shows a class called `DiceGameTracker`, which adopts the `DiceGameDelegate` protocol:*

다음 예는 `DiceGameDelegate` 프로토콜을 채택한 `DiceGameTracker`라는 클래스를 보여줍니다:

```swift
class DiceGameTracker: DiceGameDelegate {
    var numberOfTurns = 0
    func gameDidStart(_ game: DiceGame) {
        numberOfTurns = 0
        if game is SnakesAndLadders {
            print("Started a new game of Snakes and Ladders")
        }
        print("The game is using a \(game.dice.sides)-sided dice")
    }
    func game(_ game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int) {
        numberOfTurns += 1
        print("Rolled a \(diceRoll)")
    }
    func gameDidEnd(_ game: DiceGame) {
        print("The game lasted for \(numberOfTurns) turns")
    }
}
```

*`DiceGameTracker` implements all three methods required by `DiceGameDelegate`. It uses these methods to keep track of the number of turns a game has taken. It resets a `numberOfTurns` property to zero when the game starts, increments it each time a new turn begins, and prints out the total number of turns once the game has ended.*

`DiceGameTracker`는 `DiceGameDelegate`가 요구하는 세 가지 메서드를 모두 구현합니다. 이 메서드를 사용하여 게임의 턴 수를 추적합니다. 게임이 시작되면 `numberOfTurns` 프로퍼티를 0으로 재설정하고, 새로운 턴이 시작될 때마다 이 프로퍼티를 증가시키며, 게임이 종료되면 총 턴 수를 출력합니다.

*The implementation of `gameDidStart(_:)` shown above uses the `game` parameter to print some introductory information about the game that’s about to be played. The `game` parameter has a type of `DiceGame`, not `SnakesAndLadders`, and so `gameDidStart(_:)` can access and use only methods and properties that are implemented as part of the `DiceGame` protocol. However, the method is still able to use type casting to query the type of the underlying instance. In this example, it checks whether `game` is actually an instance of `SnakesAndLadders` behind the scenes, and prints an appropriate message if so.*

위의 `gameDidStart(_:)` 구현은 `game` 매개 변수를 사용하여 게임에 대한 소개 정보를 출력합니다. 게임 매개 변수는 `SnakesAndLadders`가 아닌 `DiceGame` 타입을 가지고 있으므로 `gameDidStart(_:)`는 `DiceGame` 프로토콜의 일부로 구현된 메서드 및 프로퍼티에만 액세스하여 사용할 수 있습니다. 그러나 메서드는 여전히 타입 캐스팅을 사용하여 기본 인스턴스의 타입을 쿼리할 수 있습니다. 이 예에서는 게임이 실제로 배후에서 뱀과 사다리의 인스턴스인지 여부를 확인하고, 있으면 적절한 메시지를 출력합니다.

*The `gameDidStart(_:)` method also accesses the `dice` property of the passed `game` parameter. Because `game` is known to conform to the `DiceGame` protocol, it’s guaranteed to have a `dice` property, and so the `gameDidStart(_:)` method is able to access and print the dice’s `sides` property, regardless of what kind of game is being played.*

`gameDidStart(_:)` 메서드는 전달된 `game` 매개 변수의 `dice` 프로퍼티에도 액세스합니다. 게임은 주사위 `game` 프로토콜을 준수하는 것으로 알려져 있기 때문에 주사위 프로퍼티가 보장되므로 `gameDidStart(_:)` 메서드는 어떤 게임을 플레이하든 주사위의 `sides` 프로퍼티에 액세스하여 인쇄할 수 있습니다.

*Here’s how `DiceGameTracker` looks in action:*

다음은 `DiceGameTracker`의 동작 모습입니다:

```swift
let tracker = DiceGameTracker()
let game = SnakesAndLadders()
game.delegate = tracker
game.play()
// Started a new game of Snakes and Ladders
// The game is using a 6-sided dice
// Rolled a 3
// Rolled a 5
// Rolled a 4
// Rolled a 5
// The game lasted for 4 turns
```
