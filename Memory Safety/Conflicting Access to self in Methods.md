## *Conflicting Access to self in Methods : 메서드에서 self에 대한 액세스 충돌*

*A mutating method on a structure has write access to `self` for the duration of the method call. For example, consider a game where each player has a health amount, which decreases when taking damage, and an energy amount, which decreases when using special abilities.*

구조체의 mutating 메서드는 메서드 호출 기간 동안 `self`에 대한 쓰기 액세스 권한을 가집니다. 예를 들어, 각 플레이어가 피해를 입었을 때 감소하는 체력량과 특별한 능력을 사용했을 때 감소하는 에너지량을 가진 게임을 생각해보세요.

```swift
struct Player {
    var name: String
    var health: Int
    var energy: Int

    static let maxHealth = 10
    mutating func restoreHealth() {
        health = Player.maxHealth
    }
}
```

*In the `restoreHealth()` method above, a write access to `self` starts at the beginning of the method and lasts until the method returns. In this case, there’s no other code inside `restoreHealth()` that could have an overlapping access to the properties of a `Player` instance. The `shareHealth(with:)` method below takes another `Player` instance as an in-out parameter, creating the possibility of overlapping accesses.*

위의 `restoreHealth()` 메서드에서 `self`에 대한 쓰기 액세스는 메서드의 시작 부분에서 시작하여 메서드가 반환될 때까지 지속됩니다. 이 경우 `Player` 인스턴스의 프로퍼티에 중복 액세스할 수 있는 `restoreHealth()` 내부의 다른 코드는 없습니다. 아래의 `shareHealth(with:)` 메서드는 다른 `Player` 인스턴스를 in-out 매개변수로 사용하여 중복 액세스 가능성을 생성합니다

```swift
extension Player {
    mutating func shareHealth(with teammate: inout Player) {
        balance(&teammate.health, &health)
    }
}

var oscar = Player(name: "Oscar", health: 10, energy: 10)
var maria = Player(name: "Maria", health: 5, energy: 10)
oscar.shareHealth(with: &maria)  // OK
```

*In the example above, calling the `shareHealth(with:)` method for Oscar’s player to share health with Maria’s player doesn’t cause a conflict. There’s a write access to `oscar` during the method call because `oscar` is the value of `self` in a mutating method, and there’s a write access to `maria` for the same duration because `maria` was passed as an in-out parameter. As shown in the figure below, they access different locations in memory. Even though the two write accesses overlap in time, they don’t conflict.*

위의 예에서 Oscar의 플레이어가 Maria의 플레이어와 체력을 공유하도록 `shareHealth(with:)` 메서드를 호출해도 충돌이 발생하지 않습니다. `oscar`는 변형 메서드에서 `self`의 값이기 때문에 메서드 호출 중에 `oscar`에 대한 쓰기 액세스 권한이 있고 `maria`가 in-out 매개변수로 전달되었기 때문에 같은 기간 동안 `maria`에 대한 쓰기 액세스 권한이 있습니다. 아래 그림과 같이 메모리의 다른 위치에 액세스합니다. 두 쓰기 액세스가 시간적으로 겹치더라도 충돌하지 않습니다.

*![](https://docs.swift.org/swift-book/images/memory_share_health_maria@2x.png)*

*However, if you pass `oscar` as the argument to `shareHealth(with:)`, there’s a conflict:*

하지만 `oscar`를 `shareHealth(with:)`의 인수로 전달하면 충돌이 발생합니다.

```swift
oscar.shareHealth(with: &oscar)
// Error: conflicting accesses to oscar
```

*The mutating method needs write access to `self` for the duration of the method, and the in-out parameter needs write access to `teammate` for the same duration. Within the method, both `self` and `teammate` refer to the same location in memory — as shown in the figure below. The two write accesses refer to the same memory and they overlap, producing a conflict.*

변형 메서드는 메서드 기간 동안 `self` 에 대한 쓰기 액세스 권한이 필요하고, in-out 매개변수는 같은 기간 동안 `teammate`에 대한 쓰기 액세스 권한이 필요합니다. 메서드 내에서 `self` 및 `teammate`는 아래 그림과 같이 메모리에서 동일한 위치를 참조합니다. 두 개의 쓰기 액세스는 동일한 메모리를 참조하고 겹치므로 충돌이 발생합니다.

![](https://docs.swift.org/swift-book/images/memory_share_health_oscar@2x.png)
