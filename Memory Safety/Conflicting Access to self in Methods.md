## *Conflicting Access to self in Methods*

*A mutating method on a structure has write access to `self` for the duration of the method call. For example, consider a game where each player has a health amount, which decreases when taking damage, and an energy amount, which decreases when using special abilities.*

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

*![](https://docs.swift.org/swift-book/images/memory_share_health_maria@2x.png)*

*However, if you pass `oscar` as the argument to `shareHealth(with:)`, there’s a conflict:*

```swift
oscar.shareHealth(with: &oscar)
// Error: conflicting accesses to oscar
```

*The mutating method needs write access to `self` for the duration of the method, and the in-out parameter needs write access to `teammate` for the same duration. Within the method, both `self` and `teammate` refer to the same location in memory — as shown in the figure below. The two write accesses refer to the same memory and they overlap, producing a conflict.*

*![](https://docs.swift.org/swift-book/images/memory_share_health_oscar@2x.png)*


