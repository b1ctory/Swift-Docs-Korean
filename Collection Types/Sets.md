## *Sets*

*A set stores distinct values of the same type in a collection with no defined ordering. You can use a set instead of an array when the order of items isn’t important, or when you need to ensure that an item only appears once.*

> *NOTE*
> 
> *Swift’s `Set` type is bridged to Foundation’s `NSSet` class.*
> 
> *For more information about using `Set` with Foundation and Cocoa, see [Bridging Between Set and NSSet](https://developer.apple.com/documentation/swift/set#2845530).*

### *Hash Values for Set Types*

*A type must be hashable in order to be stored in a set—that is, the type must provide a way to compute a hash value for itself. A hash value is an `Int` value that’s the same for all objects that compare equally, such that if `a == b`, the hash value of `a` is equal to the hash value of `b`.*

*All of Swift’s basic types (such as `String`, `Int`, `Double`, and `Bool`) are hashable by default, and can be used as set value types or dictionary key types. Enumeration case values without associated values (as described in [Enumerations](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html)) are also hashable by default.*

> *NOTE*
> 
> *You can use your own custom types as set value types or dictionary key types by making them conform to the `Hashable` protocol from the Swift standard library. For information about implementing the required `hash(into:)` method, see [`Hashable`](https://developer.apple.com/documentation/swift/hashable). For information about conforming to protocols, see [Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).*

### *Set Type Syntax*

*The type of a Swift set is written as `Set<Element>`, where `Element` is the type that the set is allowed to store. Unlike arrays, sets don’t have an equivalent shorthand form.*

### *Creating and Initializing an Empty Set*

*You can create an empty set of a certain type using initializer syntax:*

```swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// Prints "letters is of type Set<Character> with 0 items."
```

> *NOTE*
> 
> *The type of the `letters` variable is inferred to be `Set<Character>`, from the type of the initializer.*

*Alternatively, if the context already provides type information, such as a function argument or an already typed variable or constant, you can create an empty set with an empty array literal:*

```swift
letters.insert("a")
// letters now contains 1 value of type Character
letters = []
// letters is now an empty set, but is still of type Set<Character>
```

### *Creating a Set with an Array Literal*

*You can also initialize a set with an array literal, as a shorthand way to write one or more values as a set collection.*

*The example below creates a set called `favoriteGenres` to store `String` values:*

```swift
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
// favoriteGenres has been initialized with three initial items
```

*The `favoriteGenres` variable is declared as “a set of `String` values”, written as `Set<String>`. Because this particular set has specified a value type of `String`, it’s only allowed to store `String` values. Here, the `favoriteGenres` set is initialized with three `String` values (`"Rock"`, `"Classical"`, and `"Hip hop"`), written within an array literal.*

> *NOTE*
> 
> *The `favoriteGenres` set is declared as a variable (with the `var` introducer) and not a constant (with the `let` introducer) because items are added and removed in the examples below.*

*A set type can’t be inferred from an array literal alone, so the type `Set` must be explicitly declared. However, because of Swift’s type inference, you don’t have to write the type of the set’s elements if you’re initializing it with an array literal that contains values of just one type. The initialization of `favoriteGenres` could have been written in a shorter form instead:*

```swift
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
```

*Because all values in the array literal are of the same type, Swift can infer that `Set<String>` is the correct type to use for the `favoriteGenres` variable.*



### *Accessing and Modifying a Set*

*You access and modify a set through its methods and properties.*

*To find out the number of items in a set, check its read-only `count` property:*

```swift
print("I have \(favoriteGenres.count) favorite music genres.")
// Prints "I have 3 favorite music genres."
```

*Use the Boolean `isEmpty` property as a shortcut for checking whether the `count` property is equal to `0`:*

```swift
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
// Prints "I have particular music preferences."
```

*You can add a new item into a set by calling the set’s `insert(_:)` method:*

```swift
favoriteGenres.insert("Jazz")
// favoriteGenres now contains 4 items
```

*You can remove an item from a set by calling the set’s `remove(_:)` method, which removes the item if it’s a member of the set, and returns the removed value, or returns `nil` if the set didn’t contain it. Alternatively, all items in a set can be removed with its `removeAll()` method.*

```swift
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}
// Prints "Rock? I'm over it."
```

*To check whether a set contains a particular item, use the `contains(_:)` method.*

```swift
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// Prints "It's too funky in here."
```

### *Iterating Over a Set*

*You can iterate over the values in a set with a `for`-`in` loop.*

```swift
for genre in favoriteGenres {
    print("\(genre)")
}
// Classical
// Jazz
// Hip hop
```

*For more about the `for`-`in` loop, see [For-In Loops](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID121).*

*Swift’s `Set` type doesn’t have a defined ordering. To iterate over the values of a set in a specific order, use the `sorted()` method, which returns the set’s elements as an array sorted using the `<` operator.*

```swift
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
```


