## *Sets : 집합*

*A set stores distinct values of the same type in a collection with no defined ordering. You can use a set instead of an array when the order of items isn’t important, or when you need to ensure that an item only appears once.*

집합은 정의된 순서가 없는 집합에 동일한 유형의 고유한 값을 저장합니다. 항목 순서가 중요하지 않거나 항목이 한 번만 나타나도록 해야 할 때 배열대신 집합을 사용할 수 있습니다.

> *NOTE*
> 
> *Swift’s `Set` type is bridged to Foundation’s `NSSet` class.*
> 
> Swift의 `Set`타입은 Foundation의 `NSSet` 클래스로 연결됩니다.
> 
> *For more information about using `Set` with Foundation and Cocoa, see [Bridging Between Set and NSSet](https://developer.apple.com/documentation/swift/set#2845530).*
> 
> Foundation 및 Cocoa 와 함께 `Set`를 사용하는 방법에 대한 자세한 내용은 [링크]를 참조하세요.

### *Hash Values for Set Types : 집합 타입의 해시 값*

*A type must be hashable in order to be stored in a set—that is, the type must provide a way to compute a hash value for itself. A hash value is an `Int` value that’s the same for all objects that compare equally, such that if `a == b`, the hash value of `a` is equal to the hash value of `b`.*

집합에 저장하기 위해서는 타입이 해시 가능해야 합니다. - 즉, 타입이 해시 값을 계산하는 방법을 제공해야 합니다. 해시값은 동일하게 비교되는 모든 개체에 대해 동일한 `Int` 값입니다. 즉, `a == b` 이면 `a`의 해시 값은 `b`의 해시 값과 같습니다.

*All of Swift’s basic types (such as `String`, `Int`, `Double`, and `Bool`) are hashable by default, and can be used as set value types or dictionary key types. Enumeration case values without associated values (as described in [Enumerations](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html)) are also hashable by default.*

Swift의 모든 기본 유형 (예를 들어 `String`, `Int`, `Double` 그리고 `Bool`)은 기본적으로 해시 가능하며 집합 값 타입 혹은 딕셔너리 키 타입으로 사용할 수 있습니다. 연관된 값이 없는 열거형 대소문자 값 ([링크]에 설명되어 있습니다.)도 기본적으로 해시 가능합니다.

> *NOTE*
> 
> *You can use your own custom types as set value types or dictionary key types by making them conform to the `Hashable` protocol from the Swift standard library. For information about implementing the required `hash(into:)` method, see [`Hashable`](https://developer.apple.com/documentation/swift/hashable). For information about conforming to protocols, see [Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).*
> 
> Swift 표준 라이브러리의 해시 가능 프로토콜을 준수하도록 설정해서 사용자 정의 타입을 집합 값 타입 혹은 딕셔너리 키 타입으로 사용할 수 있습니다. 필수 메서드인  `hash(into:)`메서드 구현에 대한 자세한 내용은 [Hashable 링크]를 참조하세요. 프로토콜 준수에 대한 자세한 내용은 [링크]를 참조하세요.

### *Set Type Syntax : 집합 타입 구문*

*The type of a Swift set is written as `Set<Element>`, where `Element` is the type that the set is allowed to store. Unlike arrays, sets don’t have an equivalent shorthand form.*

Swift 집합의 타입은 `Set<Element>`로 작성되며, 여기서 `Element`는 집합이 저장할 수 있는 타입입니다. 배열과는 다르게 집합에넌 동일한 속기 형식이 없습니다.

### *Creating and Initializing an Empty Set : 빈 집합 생성 및 초기화*

*You can create an empty set of a certain type using initializer syntax:*

초기화 구문을 사용해서 특정 타입의 빈 집합을 만들 수 있습니다.

```swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// Prints "letters is of type Set<Character> with 0 items."
```

> *NOTE*
> 
> *The type of the `letters` variable is inferred to be `Set<Character>`, from the type of the initializer.*
> 
> `letters` 변수의 타입은 초기화 타입에서 `Set<Character>` 변수로 추론됩니다.

*Alternatively, if the context already provides type information, such as a function argument or an already typed variable or constant, you can create an empty set with an empty array literal:*

대신에, 컨텍스트가 이미 함수의 인수, 이미 입력된 변수 혹은 상수와 같은 타입 정보를 제공하는 경우 빈 배열 리터럴을 사용해서 빈 집합을 만들 수 있습니다.

```swift
letters.insert("a")
// letters now contains 1 value of type Character
letters = []
// letters is now an empty set, but is still of type Set<Character>
```

### *Creating a Set with an Array Literal : 배열 리터럴로 집합 만들기*

*You can also initialize a set with an array literal, as a shorthand way to write one or more values as a set collection.*

하나 이상의 값을 집합 컬렉션으로 쓰는 간단한 방법으로 배열 리터럴을 사용해서 집합을 초기화할 수 도 있습니다.

*The example below creates a set called `favoriteGenres` to store `String` values:*

아래의 예제에서는 `favoriteGenres`라는 집합을 만들어서 `String` 값을 저장합니다.

```swift
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
// favoriteGenres has been initialized with three initial items
```

*The `favoriteGenres` variable is declared as “a set of `String` values”, written as `Set<String>`. Because this particular set has specified a value type of `String`, it’s only allowed to store `String` values. Here, the `favoriteGenres` set is initialized with three `String` values (`"Rock"`, `"Classical"`, and `"Hip hop"`), written within an array literal.*

`favoriteGenres` 변수는 "`String` 값의 집합"으로 선언되며, `Set<String>`으로 작성됩니다. 이 집합은 값 타입 `String`을 지정했기 때문에 `String` 값만 저장할 수 있습니다. 여기서, `favoriteGenres` 집합은 배열 리터럴 내에 쓰여진 세 개의 `String` 값 (`"Rock"`, `"Classical"`, 그리고 `"Hip hop"`) 으로 초기화됩니다.

> *NOTE*
> 
> *The `favoriteGenres` set is declared as a variable (with the `var` introducer) and not a constant (with the `let` introducer) because items are added and removed in the examples below.*
> 
> 아래 예제에서 항목이 추가 및 제거되기 때문에 `favoriteGenres` 집합은 상수 (`let`)가 아닌 변수 (`var`)로 선언됩니다.

*A set type can’t be inferred from an array literal alone, so the type `Set` must be explicitly declared. However, because of Swift’s type inference, you don’t have to write the type of the set’s elements if you’re initializing it with an array literal that contains values of just one type. The initialization of `favoriteGenres` could have been written in a shorter form instead:*

집합 타입은 배열 리터럴에서만 유추할 수 없기 때문에 집합 타입을 명시적으로 선언해야 합니다. 그러나 Swift의 타입 추론 때문에 한 타입의 값만 포함하는 배열 리터럴로 초기화하는 경우에는 집합의 요소 유형을 작성할 필요가 없습니다. `favoriteGenres`의 초기화는 다음과 같이 더 짧은 형식으로 작성될 수 있습니다.

```swift
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
```

*Because all values in the array literal are of the same type, Swift can infer that `Set<String>` is the correct type to use for the `favoriteGenres` variable.*

배열 리터럴의 모든 값이 동일한 타입이기 때문에 Swift는 `Set<String>`이 `favoriteGenres` 변수에 사용할 올바른 타입이라고 추론할 수 있습니다.

### *Accessing and Modifying a Set : 집합 접근 및 수정*

*You access and modify a set through its methods and properties.*

메서드 및 속성을 통해 집합에 접근하고 수정합니다.

*To find out the number of items in a set, check its read-only `count` property:*

집합의 항목 갯수를 알아보려면 읽기 전용 `count` 프로퍼티를 확인하세요.

```swift
print("I have \(favoriteGenres.count) favorite music genres.")
// Prints "I have 3 favorite music genres."
```

*Use the Boolean `isEmpty` property as a shortcut for checking whether the `count` property is equal to `0`:*

`count` 프로퍼티가 `0`과 같은지 확인하기 위한 지름길로 Boolean 타입의 `isEmpty` 프로퍼티를 사용하세요.

```swift
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
// Prints "I have particular music preferences."
```

*You can add a new item into a set by calling the set’s `insert(_:)` method:*

집합의 `insert(_:)` 메서드를 호출해서 집합에 새 항목을 추가할 수 있습니다.

```swift
favoriteGenres.insert("Jazz")
// favoriteGenres now contains 4 items
```

*You can remove an item from a set by calling the set’s `remove(_:)` method, which removes the item if it’s a member of the set, and returns the removed value, or returns `nil` if the set didn’t contain it. Alternatively, all items in a set can be removed with its `removeAll()` method.*

집합의 `remove(_:)` 메서드를 호출해서 집합에서 항목을 제거할 수 있습니다. 이 메서드는 항목이 집합의 구성원이면 제거된 값을 반환하고, 집합에 포함되지 않은 경우에는 `nil`을 반환합니다. 또는 집합의 몯느 항목을 `removeAll()` 메서드를 사용해서 제거할 수 있습니다.

```swift
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}
// Prints "Rock? I'm over it."
```

*To check whether a set contains a particular item, use the `contains(_:)` method.*

집합에 특정 항목이 포함되어 있는지 확인하려면 `contains(_:)` 메서드를 사용합니다.

```swift
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// Prints "It's too funky in here."
```

### *Iterating Over a Set : 집합에 대한 반복*

*You can iterate over the values in a set with a `for`-`in` loop.*

`for`-`in` 루프를 사용해서 집합의 값을 반복할 수 있습니다.

```swift
for genre in favoriteGenres {
    print("\(genre)")
}
// Classical
// Jazz
// Hip hop
```

*For more about the `for`-`in` loop, see [For-In Loops](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID121).*

`for`-`in` 루프에 대한 더 자세한 내용은 [링크]를 참조하세요.

*Swift’s `Set` type doesn’t have a defined ordering. To iterate over the values of a set in a specific order, use the `sorted()` method, which returns the set’s elements as an array sorted using the `<` operator.*

Swift의 `Set`타입에는 정해진 순서가 없습니다. 집합의 값을 특정 순서로 반복하려면 집합의 요소를 `<`연산자를 사용해서 정렬된 배열로 반환하는 `sorted()` 메서드를 사용합니다.

```swift
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
```
