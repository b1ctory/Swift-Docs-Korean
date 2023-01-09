## *Type Methods : 타입 메서드*

*Instance methods, as described above, are methods that you call on an instance of a particular type. You can also define methods that are called on the type itself. These kinds of methods are called type methods. You indicate type methods by writing the `static` keyword before the method’s `func` keyword. Classes can use the `class` keyword instead, to allow subclasses to override the superclass’s implementation of that method.*

인스턴스 메서드는 위에서 설명한 대로 특정 타입의 인스턴스에서 호출하는 메서드입니다. 타입 자체에서 호출되는 메서드를 정의할 수도 있습니다. 이러한 종류의 메서드를 타입 메서드라고 합니다. 메서드의 `func` 키워드 앞에 `static` 키워드를 작성하여 타입 메서드를 나타냅니다. 클래스는 대신 `class` 키워드를 사용하여 하위 클래스가 해당 메서드의 슈퍼 클래스 구현을 재정의할 수 있습니다.

> *NOTE*
> 
> *In Objective-C, you can define type-level methods only for Objective-C classes. In Swift, you can define type-level methods for all classes, structures, and enumerations. Each type method is explicitly scoped to the type it supports.*
> 
> Objective-C에서 Objective-C 클래스에 대해서만 타입레벨 메서드를 정의할 수 있습니다. Swift에서 모든 클래스, 구조체 및 열거형에 대한 타입 레벨 메서드를 정의할 수 있습니다. 각 타입 메서드는 지원되는 타입 따라 명시적으로 범위가 지정됩니다.

*Type methods are called with dot syntax, like instance methods. However, you call type methods on the type, not on an instance of that type. Here’s how you call a type method on a class called `SomeClass`:*

타입 메서드는 인스턴스 메서드와 마찬가지로 점 구문으로 호출됩니다. 그러나 타입 메서드는 해당 타입의 인스턴스가 아닌 타입에 대해 호출합니다. 다음은 `SomeClass`라는 클래스에서 타입 메서드를 호출하는 방법입니다:

```swift
class SomeClass {
    class func someTypeMethod() {
        // type method implementation goes here
    }
}
SomeClass.someTypeMethod()
```

*Within the body of a type method, the implicit `self` property refers to the type itself, rather than an instance of that type. This means that you can use `self` to disambiguate between type properties and type method parameters, just as you do for instance properties and instance method parameters.*

타입 메서드의 본문 내에서 암시적인 `self` 프로퍼티는 해당 타입의 인스턴스가 아니라 타입 자체를 나타냅니다. 즉, 인스턴스 프로퍼티 및 인스턴스 메서드 매개 변수와 마찬가지로 `self`를 사용하여 타입 프로퍼티와 타입 메서드 매개 변수를 명확하게 구분할 수 있습니다.

*More generally, any unqualified method and property names that you use within the body of a type method will refer to other type-level methods and properties. A type method can call another type method with the other method’s name, without needing to prefix it with the type name. Similarly, type methods on structures and enumerations can access type properties by using the type property’s name without a type name prefix.*

일반적으로 타입 메서드의 본문 내에서 사용하는 타입 메서드 및 프로퍼티 이름은 다른 타입레벨 메서드 및 프로퍼티를 참조합니다. 타입 메서드는 타입 이름 앞에 접두사를 붙이지 않고 다른 타입 메서드의 이름을 사용하여 다른 타입 메서드를 호출할 수 있습니다. 마찬가지로 구조체 및 열거형의 타입 메서드는 타입 이름 접두사 없이 타입 프로퍼티의 이름을 사용하여 타입 프로퍼티에 액세스할 수 있습니다.

*The example below defines a structure called `LevelTracker`, which tracks a player’s progress through the different levels or stages of a game. It’s a single-player game, but can store information for multiple players on a single device.*

아래 예시는 `LevelTracker`라는 구조체를 정의하고 있는데, 이 구조체는 게임의 다양한 레벨이나 단계를 통해 플레이어의 진행 상황을 추적합니다. 단일 플레이어 게임이지만 여러 플레이어의 정보를 단일 장치에 저장할 수 있습니다.

*All of the game’s levels (apart from level one) are locked when the game is first played. Every time a player finishes a level, that level is unlocked for all players on the device. The `LevelTracker` structure uses type properties and methods to keep track of which levels of the game have been unlocked. It also tracks the current level for an individual player.*

게임이 처음 시작될 때 (레벨 1을 제외한) 모든 레벨이 잠깁니다. 플레이어가 레벨을 마칠 때마다 장치의 모든 플레이어에 대해 해당 레벨의 잠금이 해제됩니다. `LevelTracker` 구조체는 타입 프로퍼티와 메서드를 사용하여 어떤 레벨의 게임이 잠금 해제되었는지 추적합니다. 또한 개별 플레이어의 현재 레벨을 추적합니다.

```swift
struct LevelTracker {
    static var highestUnlockedLevel = 1
    var currentLevel = 1

    static func unlock(_ level: Int) {
        if level > highestUnlockedLevel { highestUnlockedLevel = level }
    }

    static func isUnlocked(_ level: Int) -> Bool {
        return level <= highestUnlockedLevel
    }

    @discardableResult
    mutating func advance(to level: Int) -> Bool {
        if LevelTracker.isUnlocked(level) {
            currentLevel = level
            return true
        } else {
            return false
        }
    }
}
```

*The `LevelTracker` structure keeps track of the highest level that any player has unlocked. This value is stored in a type property called `highestUnlockedLevel`.*

`LevelTracker` 구조체는 플레이어가 잠금을 해제한 최고 레벨을 추적합니다. 이 값은 `highestUnlockedLevel`이라는 타입 프로퍼티에 저장됩니다.

*`LevelTracker` also defines two type functions to work with the `highestUnlockedLevel` property. The first is a type function called `unlock(_:)`, which updates the value of `highestUnlockedLevel` whenever a new level is unlocked. The second is a convenience type function called `isUnlocked(_:)`, which returns `true` if a particular level number is already unlocked. (Note that these type methods can access the `highestUnlockedLevel` type property without your needing to write it as `LevelTracker.highestUnlockedLevel`.)*

`LevelTracker`는 또한 `highestUnlockedLevel` 프로퍼티와 함께 작동하는 두 가지 타입 함수를 정의합니다. 첫 번째는 새로운 레벨이 잠금 해제될 때마다 `highestUnlockedLevel`의 값을 업데이트하는 `unlock(_:)` 타입 함수입니다. 두 번째는 `isUnlocked(_:)`라는 편의형 함수로, 특정 레벨 숫자가 이미 잠금 해제되어 있으면 `true`를 반환합니다. (이러한 타입 메서드는 `highestUnlockedLevel` 타입 프로퍼티를 `LevelTracker.highestUnlockedLevel`로 쓰지 않고도 액세스할 수 있습니다.)

*In addition to its type property and type methods, `LevelTracker` tracks an individual player’s progress through the game. It uses an instance property called `currentLevel` to track the level that a player is currently playing.*

`LevelTracker`는 타입 프로퍼티와 타입 메서드 외에도 게임 진행 상황을 추적합니다. `currentLevel`이라는 인스턴스 프로퍼티 사용하여 플레이어가 현재 플레이하고 있는 레벨을 추적합니다.

*To help manage the `currentLevel` property, `LevelTracker` defines an instance method called `advance(to:)`. Before updating `currentLevel`, this method checks whether the requested new level is already unlocked. The `advance(to:)` method returns a Boolean value to indicate whether or not it was actually able to set `currentLevel`. Because it’s not necessarily a mistake for code that calls the `advance(to:)` method to ignore the return value, this function is marked with the `@discardableResult` attribute. For more information about this attribute, see [Attributes](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html).*

`currentLevel` 프로퍼티를 관리하는 데 도움이 되도록 `LevelTracker`는 `advance(to:)`라는 인스턴스 메서드를 정의합니다. `currentLevel`을 업데이트하기 전에 이 메서드는 요청된 새 레벨이 이미 잠금 해제되어 있는지 확인합니다. `advance(to:)` 메서드는 실제로 `currentLevel`을 설정할 수 있었는지 여부를 나타내는 Bool 값을 반환합니다. `advance(to:)` 메서드를 호출하는 코드가 반환 값을 무시하는 것이 반드시 실수는 아니기 때문에 이 함수는 `@discardableResult` 속성으로 표시됩니다. 이 속성에 대한 자세한 내용은 [링크]를 참조하십시오.

*The `LevelTracker` structure is used with the `Player` class, shown below, to track and update the progress of an individual player:*

`LevelTracker` 구조체는 아래에 나와 있는 `Player` 클래스와 함께 사용하여 개별 플레이어의 진행 상황을 추적하고 업데이트합니다:

```swift
class Player {
    var tracker = LevelTracker()
    let playerName: String
    func complete(level: Int) {
        LevelTracker.unlock(level + 1)
        tracker.advance(to: level + 1)
    }
    init(name: String) {
        playerName = name
    }
}
```

*The `Player` class creates a new instance of `LevelTracker` to track that player’s progress. It also provides a method called `complete(level:)`, which is called whenever a player completes a particular level. This method unlocks the next level for all players and updates the player’s progress to move them to the next level. (The Boolean return value of `advance(to:)` is ignored, because the level is known to have been unlocked by the call to `LevelTracker.unlock(_:)` on the previous line.)*

`Player` 클래스는 `LevelTracker`의 새 인스턴스를 생성하여 해당 플레이어의 진행 상황을 추적합니다. 또한 플레이어가 특정 레벨을 완료할 때마다 호출되는 `complete(level:)`라는 메서드를 제공합니다. 이 메서드는 모든 플레이어의 다음 레벨을 잠금 해제하고 플레이어의 진행률을 업데이트하여 다음 레벨로 이동합니다. (이전 라인의 `LevelTracker.unlock(_:)`에 대한 호출로 레벨이 잠금 해제된 것으로 알려져 있으므로 'advance(to:)'의 Bool 반환 값은 무시됩니다.)

*You can create an instance of the `Player` class for a new player, and see what happens when the player completes level one:*

새 플레이어에 대한 `Player` 클래스의 인스턴스를 만들고 플레이어가 레벨 1을 완료하면 어떻게 되는지 확인할 수 있습니다:

```swift
var player = Player(name: "Argyrios")
player.complete(level: 1)
print("highest unlocked level is now \(LevelTracker.highestUnlockedLevel)")
// Prints "highest unlocked level is now 2"
```

*If you create a second player, whom you try to move to a level that’s not yet unlocked by any player in the game, the attempt to set the player’s current level fails:*

게임의 어느 플레이어도 아직 잠금을 해제하지 않은 레벨로 이동하려는 두 번째 플레이어를 만들면 플레이어의 현재 레벨을 설정하는 시도가 실패합니다:

```swift
player = Player(name: "Beto")
if player.tracker.advance(to: 6) {
    print("player is now on level 6")
} else {
    print("level 6 hasn't yet been unlocked")
}
// Prints "level 6 hasn't yet been unlocked"
```
