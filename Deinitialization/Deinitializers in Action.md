## *Deinitializers in Action*

*Here’s an example of a deinitializer in action. This example defines two new types, `Bank` and `Player`, for a simple game. The `Bank` class manages a made-up currency, which can never have more than 10,000 coins in circulation. There can only ever be one `Bank` in the game, and so the `Bank` is implemented as a class with type properties and methods to store and manage its current state:*

여기에 deinitializer가 작동하는 예가 있습니다. 이 예에서는 간단한 게임을 위해 두 가지 새로운 타입인 `Bank`와 `Player`를 정의합니다. `Bank` 클래스는 10,000개 이상의 코인이 유통될 수 없는 구성 통화를 관리합니다. 게임에는 하나의 `Bank`만 있을 수 있으므로 `Bank`는 현재 상태를 저장하고 관리하기 위한 타입 프로퍼티 및 메소드가 있는 클래스로 구현됩니다

```swift
class Bank {
    static var coinsInBank = 10_000
    static func distribute(coins numberOfCoinsRequested: Int) -> Int {
        let numberOfCoinsToVend = min(numberOfCoinsRequested, coinsInBank)
        coinsInBank -= numberOfCoinsToVend
        return numberOfCoinsToVend
    }
    static func receive(coins: Int) {
        coinsInBank += coins
    }
}
```

*`Bank` keeps track of the current number of coins it holds with its `coinsInBank` property. It also offers two methods—`distribute(coins:)` and `receive(coins:)`—to handle the distribution and collection of coins.*

`Bank`는 `coinsInBank` 프로퍼티로 보유하고 있는 현재 코인 수를 추적합니다. 또한 `distribute(coins:)` 및 `receive(coins:)`라는 두 가지 메서드를 제공하여 코인의 배포 및 수집을 처리합니다.

*The `distribute(coins:)` method checks that there are enough coins in the bank before distributing them. If there aren’t enough coins, `Bank` returns a smaller number than the number that was requested (and returns zero if no coins are left in the bank). It returns an integer value to indicate the actual number of coins that were provided.*

`distribute(coins:)` 메서드는 분배하기 전에 은행에 코인이 충분한지 확인합니다. 코인이 충분하지 않은 경우 `Bank`는 요청된 숫자보다 작은 숫자를 반환합니다 (은행에 코인이 남아 있지 않으면 0을 반환합니다). 제공된 실제 코인 수를 나타내는 정수 값을 반환합니다.

*The `receive(coins:)` method simply adds the received number of coins back into the bank’s coin store.*

`receive(coins:)` 메서드는 받은 코인 수를 은행의 코인 저장소에 다시 추가합니다.

*The `Player` class describes a player in the game. Each player has a certain number of coins stored in their purse at any time. This is represented by the player’s `coinsInPurse` property:*

`Player` 클래스는 게임의 플레이어를 설명합니다. 각 플레이어는 언제든지 지갑에 일정 수의 코인을 보관하고 있습니다. 이는 플레이어의 `coinsInPurse` 프로퍼티로 표시됩니다.

```swift
class Player {
    var coinsInPurse: Int
    init(coins: Int) {
        coinsInPurse = Bank.distribute(coins: coins)
    }
    func win(coins: Int) {
        coinsInPurse += Bank.distribute(coins: coins)
    }
    deinit {
        Bank.receive(coins: coinsInPurse)
    }
}
```

*Each `Player` instance is initialized with a starting allowance of a specified number of coins from the bank during initialization, although a `Player` instance may receive fewer than that number if not enough coins are available.*

각 `Player` 인스턴스는 초기화 중에 은행에서 지정된 수의 코인의 시작 수당으로 초기화되지만, `Player` 인스턴스는 사용 가능한 코인이 충분하지 않은 경우 해당 수보다 적게 받을 수 있습니다.

*The `Player` class defines a `win(coins:)` method, which retrieves a certain number of coins from the bank and adds them to the player’s purse. The `Player` class also implements a deinitializer, which is called just before a `Player` instance is deallocated. Here, the deinitializer simply returns all of the player’s coins to the bank:*

`Player` 클래스는 은행에서 일정 수의 코인을 검색하여 플레이어의 지갑에 추가하는 `win(coins:)` 메소드를 정의합니다. `Player` 클래스는 또한 `Player` 인스턴스가 할당 해제되기 직전에 호출되는 deinitilizer를 구현합니다. 여기서 deinitializer는 단순히 플레이어의 모든 코인을 은행에 반환합니다.

```swift
var playerOne: Player? = Player(coins: 100)
print("A new player has joined the game with \(playerOne!.coinsInPurse) coins")
// Prints "A new player has joined the game with 100 coins"
print("There are now \(Bank.coinsInBank) coins left in the bank")
// Prints "There are now 9900 coins left in the bank"
```

*A new `Player` instance is created, with a request for 100 coins if they’re available. This `Player` instance is stored in an optional `Player` variable called `playerOne`. An optional variable is used here, because players can leave the game at any point. The optional lets you track whether there’s currently a player in the game.*

사용 가능한 경우 100개의 코인을 요청하는 새로운 `Player` 인스턴스가 생성됩니다. 이 `Player` 인스턴스는 `playerOne`이라는 옵셔널 `Player` 변수에 저장됩니다. 플레이어는 언제든지 게임을 떠날 수 있으므로 여기서는 옵셔널 변수를 사용합니다. 옵셔널을 사용하면 현재 게임에 플레이어가 있는지 여부를 추적할 수 있습니다.

*Because `playerOne` is an optional, it’s qualified with an exclamation point (`!`) when its `coinsInPurse` property is accessed to print its default number of coins, and whenever its `win(coins:)` method is called:*

`playerOne`은 옵셔널이므로,  `coinsInPurse` 프로퍼티에 액세스하여 기본 동전 수를 인쇄하고 `win(coins:)` 메서드가 호출될 때마다 느낌표(`!`)로 한정됩니다.

```swift
playerOne!.win(coins: 2_000)
print("PlayerOne won 2000 coins & now has \(playerOne!.coinsInPurse) coins")
// Prints "PlayerOne won 2000 coins & now has 2100 coins"
print("The bank now only has \(Bank.coinsInBank) coins left")
// Prints "The bank now only has 7900 coins left"
```

*Here, the player has won 2,000 coins. The player’s purse now contains 2,100 coins, and the bank has only 7,900 coins left.*

여기서 플레이어는 2,000 코인을 얻었습니다. 플레이어의 지갑에는 이제 2,100개의 코인이 있고 은행에는 7,900개의 코인만 남아 있습니다.

```swift
playerOne = nil
print("PlayerOne has left the game")
// Prints "PlayerOne has left the game"
print("The bank now has \(Bank.coinsInBank) coins")
// Prints "The bank now has 10000 coins"
```

*The player has now left the game. This is indicated by setting the optional `playerOne` variable to `nil`, meaning “no `Player` instance.” At the point that this happens, the `playerOne` variable’s reference to the `Player` instance is broken. No other properties or variables are still referring to the `Player` instance, and so it’s deallocated in order to free up its memory. Just before this happens, its deinitializer is called automatically, and its coins are returned to the bank.*

플레이어는 이제 게임을 떠났습니다. 이것은 옵셔널 `playerOne` 변수를 `nil`로 설정하여 표시됩니다. 이는 '`Player` 인스턴스 없음'을 의미합니다. 이 시점에서 `Player` 인스턴스에 대한 `playerOne` 변수의 참조가 손상됩니다. 다른 프로퍼티나 변수는 아직 `Player` 인스턴스를 참조하지 않으므로 메모리를 확보하기 위해 할당이 취소됩니다. 이 일이 발생하기 직전에 deinitializer가 자동으로 호출되고 코인이 은행으로 반환됩니다.


