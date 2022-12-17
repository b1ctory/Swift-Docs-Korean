## *Dictionaries : 딕셔너리*

*A dictionary stores associations between keys of the same type and values of the same type in a collection with no defined ordering. Each value is associated with a unique key, which acts as an identifier for that value within the dictionary. Unlike items in an array, items in a dictionary don’t have a specified order. You use a dictionary when you need to look up values based on their identifier, in much the same way that a real-world dictionary is used to look up the definition for a particular word.*

딕셔너리는 동일한 타입의 키와 값 사이의 연결을 정의한 순서가 없는 집합에 저장합니다. 각각의 값은 딕셔너리 내에서 해당 값의 식별자 역할을 하는 고유 키와 연결됩니다. 배열의 항목과 달리 딕셔너리의 항목은 지정된 순서가 없습니다.실제 사전이 특정 단어의 정의를 검색하는데 사용되는 것과 동일한 방식으로 식별자를 기반으로 값을 검색해야 할 때 딕셔너리를 사용합니다.

> *NOTE*
> 
> *Swift’s `Dictionary` type is bridged to Foundation’s `NSDictionary` class.*
> 
> Swift의 `Dictionary` 타입은 Foundation의 `NSDictionary` 클래스와 연결됩니다.
> 
> *For more information about using `Dictionary` with Foundation and Cocoa, see [Bridging Between Dictionary and NSDictionary](https://developer.apple.com/documentation/swift/dictionary#2846239).*
> 
> `Foundation` 및 `Cocoa`와 함께 `Dictionary`를 사용하는 방법에 대한 자세한 내용은 [링크]를 확인하세요.

### *Dictionary Type Shorthand Syntax : 딕셔너리 타입 단축 구문*

*The type of a Swift dictionary is written in full as `Dictionary<Key, Value>`, where `Key` is the type of value that can be used as a dictionary key, and `Value` is the type of value that the dictionary stores for those keys.*

Swift 딕셔너리의 형식은 풀로 작성하면 `Dictionary<Key, Value>`로 작성되고, 여기서 `Key`는 딕셔너리 키로 사용할 수 있는 값의 타입이고 `Value`는 해당 키에 대해 딕셔너리가 저장하는 값의 타입입니다.

> *NOTE*
> 
> *A dictionary `Key` type must conform to the `Hashable` protocol, like a set’s value type.*
> 
> 딕셔너리 `Key` 타입은 집합의 값 타입과 같이 `Hashable` 프로토콜을 준수해야 합니다.

*You can also write the type of a dictionary in shorthand form as `[Key: Value]`. Although the two forms are functionally identical, the shorthand form is preferred and is used throughout this guide when referring to the type of a dictionary.*

딕셔너리의 종류를 속기 형태로 `[Key: Value]` 으로 쓸 수도 있습니다. 두 가지 형식이 기능적으로는 동일하지만, 딕셔너리의 타입을 언급할 때는 이 안내서 전체에 걸쳐 속기 형식이 선호됩니다.

### *Creating an Empty Dictionary : 빈 딕셔너리 만들기*

*As with arrays, you can create an empty `Dictionary` of a certain type by using initializer syntax:*

배열과 마찬가지로 초기화 구문을 사용해서 특정 타입의 빈 딕셔너리를 만들 수 있습니다.

```swift
var namesOfIntegers: [Int: String] = [:]
// namesOfIntegers is an empty [Int: String] dictionary
```

*This example creates an empty dictionary of type `[Int: String]` to store human-readable names of integer values. Its keys are of type `Int`, and its values are of type `String`.*

이 예에서는 사람이 읽을 수 있는 정수 값 이름을 저장하기 위해 `[Int: String]` 타입의 빈 딕셔너리를 만듭니다. 키는 `Int` 형이고, 값은 `String` 형입니다.

*If the context already provides type information, you can create an empty dictionary with an empty dictionary literal, which is written as `[:]` (a colon inside a pair of square brackets):*

콘텍스트가 이미 타입 정보를 제공하는 경우 빈 딕셔너리 리터럴을 사용해서 빈 딕셔너리를 만들 수 있습니다. 이 딕셔너리 리터럴은 `[:]`로 작성됩니다.

```swift
namesOfIntegers[16] = "sixteen"
// namesOfIntegers now contains 1 key-value pair
namesOfIntegers = [:]
// namesOfIntegers is once again an empty dictionary of type [Int: String]
```

### *Creating a Dictionary with a Dictionary Literal : 딕셔너리 리터럴을 사용해서 딕셔너리 만들기*

*You can also initialize a dictionary with a dictionary literal, which has a similar syntax to the array literal seen earlier. A dictionary literal is a shorthand way to write one or more key-value pairs as a `Dictionary` collection.*

앞서 본 배열 리터럴과 유사한 구문을 가진 딕셔너리 리터럴을 사용해서 딕셔너리를 초기화할 수도 있습니다. 딕셔너리 리터럴은 하나 이상의 키-값 쌍을 딕셔너리 컬렉션으로 작성하는 간단한 방법입니다.

*A key-value pair is a combination of a key and a value. In a dictionary literal, the key and value in each key-value pair are separated by a colon. The key-value pairs are written as a list, separated by commas, surrounded by a pair of square brackets:*

키-값 쌍은 키와 값의 조합입니다. 딕셔너리 리터럴에서 각 키-값 쌍의 키와 값은 콜론으로 구분됩니다. 키-값 쌍은 쉼표로 구분된 목록으로 작성되며 대괄호 한 쌍으로 둘러싸여 있습니다.

```swift
[key 1: value 1, key 2: value 2, key 3: value 3]
```

*The example below creates a dictionary to store the names of international airports. In this dictionary, the keys are three-letter International Air Transport Association codes, and the values are airport names:*

아래 예제는 국제 공항의 이름을 저장하기 위한 딕셔너리를 만듭니다. 이 사전에서 키는 세 글자의 국제 항공 운송 협회 코드이며 값은 공항 이름입니다.

```swift
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```

*The `airports` dictionary is declared as having a type of `[String: String]`, which means “a `Dictionary` whose keys are of type `String`, and whose values are also of type `String`”.*

`airports` 딕셔너리는 키가 문자열이고 값도 문자열인 딕셔너리라는 뜻의 `[String:String]` 형태로 표현됩니다.

> *NOTE*
> 
> *The `airports` dictionary is declared as a variable (with the `var` introducer), and not a constant (with the `let` introducer), because more airports are added to the dictionary in the examples below.*
> 
> `airports` 딕셔너리는 변수로 (`var`) 선언되며, 상수로 (`let`) 선언되지 않습니다. 아래의 예에서 더 많은 공항이 딕셔너리에 추가되기 때문입니다.

*The `airports` dictionary is initialized with a dictionary literal containing two key-value pairs. The first pair has a key of `"YYZ"` and a value of `"Toronto Pearson"`. The second pair has a key of `"DUB"` and a value of `"Dublin"`.*

`airports` 딕셔너리는 두 개의 키-값 쌍을 포함하는 딕셔너리 리터럴로 초기화됩니다. 첫 번째 쌍은 `YYZ`의 키를 가지고 `Toronto Person`의 값을 가지고 있습니다. 두번째 쌍은 `DUB` 키와 `Dublin` 값을 가지고 있습니다.

*This dictionary literal contains two `String: String` pairs. This key-value type matches the type of the `airports` variable declaration (a dictionary with only `String` keys, and only `String` values), and so the assignment of the dictionary literal is permitted as a way to initialize the `airports` dictionary with two initial items.*

이 딕셔너리 리터럴에는 두 개의 `String : String` 쌍이 포함되어 있습니다. 이 키-값 타입은 `airports` 변수 선언 타입 (`String` 키만 있고 `String` 값만 있는 딕셔너리)과 일치하므로 두 개의 초기 항목으로 `airports` 딕셔너리를 초기화하는 방법으로 딕셔너리 리터럴 할당이 허용됩니다.

*As with arrays, you don’t have to write the type of the dictionary if you’re initializing it with a dictionary literal whose keys and values have consistent types. The initialization of `airports` could have been written in a shorter form instead:*

배열과 마찬가지로 키와 값의 타입이 일치하는 딕셔너리 리터럴을 사용해서 딕셔너리를 초기화하는 경우 딕셔너리의 타입을 작성할 필요가 없습니다. `airports`의 초기화는 다음과 같이 더 짧은 형태로 작성될 수 있었습니다.

```swift
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```

*Because all keys in the literal are of the same type as each other, and likewise all values are of the same type as each other, Swift can infer that `[String: String]` is the correct type to use for the `airports` dictionary.*

문자의 모든 키가 동일한 타입이고 모든 값도 동일한 타입이기 때문에 Swift는 `[String: String]`이 `airports` 딕셔너리에 사용할 올바른 타입이라고 추론할 수 있습니다.

### *Accessing and Modifying a Dictionary : 딕셔너리 접근 및 수정*

*You access and modify a dictionary through its methods and properties, or by using subscript syntax.*

메서드 및 속성을 사용하거나 첨자 구문을 사용해서 딕셔너리에 엑세스하고 수정합니다.

*As with an array, you find out the number of items in a `Dictionary` by checking its read-only `count` property:*

배열과 마찬가지로 읽기 전용 `count` 속성을 확인해서 `Dictionary`의 항목 수를 확인합니다.

```swift
print("The airports dictionary contains \(airports.count) items.")
// Prints "The airports dictionary contains 2 items."
```

*Use the Boolean `isEmpty` property as a shortcut for checking whether the `count` property is equal to `0`:*

Boolen `isEmpty` 속성을 사용해서 `count` 속성이 `0`과 동일한지 확인합니다.

```swift
if airports.isEmpty {
    print("The airports dictionary is empty.")
} else {
    print("The airports dictionary isn't empty.")
}
// Prints "The airports dictionary isn't empty."
```

*You can add a new item to a dictionary with subscript syntax. Use a new key of the appropriate type as the subscript index, and assign a new value of the appropriate type:*

첨자 구문을 사용해서 딕셔너리에 새 항목을 추가할 수 있습니다. 적절한 타입의 새 키를 첨자 인덱스로 사용하고 적절한 타입의 새 값을 할당합니다.

```swift
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
```

*You can also use subscript syntax to change the value associated with a particular key:*

첨자 구문을 사용해서 특정 키와 관련된 값을 변경할 수도 있습니다.

```swift
airports["LHR"] = "London Heathrow"
// the value for "LHR" has been changed to "London Heathrow"
```

*As an alternative to subscripting, use a dictionary’s `updateValue(_:forKey:)` method to set or update the value for a particular key. Like the subscript examples above, the `updateValue(_:forKey:)` method sets a value for a key if none exists, or updates the value if that key already exists. Unlike a subscript, however, the `updateValue(_:forKey:)` method returns the old value after performing an update. This enables you to check whether or not an update took place.*

구독 대신 딕셔너리의 `updateValue(_:forKey:)` 메서드를 사용해서 특정 키의 값을 설정하거나 업데이트합니다. 위의 첨자 예시와 마찬가지로 `updateValue(_:forKey:)` 메서드는 키가 없으면 값을 설정하거나 키가 이미 있으면 값을 업데이트합니다. 그러나 첨자와 달리 `updateValue(_:forKey:)` 메서드는 업데이트를 수행한 후 이전 값을 반환합니다. 이렇게 하면 업데이트가 수행되었는지 여부를 확인할 수 있습니다. 

*The `updateValue(_:forKey:)` method returns an optional value of the dictionary’s value type. For a dictionary that stores `String` values, for example, the method returns a value of type `String?`, or “optional `String`”. This optional value contains the old value for that key if one existed before the update, or `nil` if no value existed:*

`updateValue(_:forKey:)` 메서드는 딕셔너리의 값 타입에 대한 optional 값을 반환합니다. 예를 들어 String 값을 저장하는 딕셔너리의 경우, 메서드는 `String?` 타입 혹은 `optional String` 타입의 값을 반환합니다. 이 옵셔널 값은 업데이트 전에 키의 이전 값을 포함하며, 값이 없으면 `nil`을 포함합니다.

```swift
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
// Prints "The old value for DUB was Dublin."
```

*You can also use subscript syntax to retrieve a value from the dictionary for a particular key. Because it’s possible to request a key for which no value exists, a dictionary’s subscript returns an optional value of the dictionary’s value type. If the dictionary contains a value for the requested key, the subscript returns an optional value containing the existing value for that key. Otherwise, the subscript returns `nil`:*

첨자 구문을 사용해서 딕셔너리에서 특정 키에 대한 값을 검색할 수도 있습니다. 값이 없는 키를 요청할 수 있으므로 딕셔너리의 첨자는 딕셔너리의 값 타입에 대한 옵셔널 값을 반환합니다. 딕셔너리에 요청한 키의 값이 표현된 경우, 첨자는 해당 키의 기존 값을 포함하는 옵셔널 값을 반환합니다. 그렇지 않으면 첨자가 `nil`을 반환합니다.

```swift
if let airportName = airports["DUB"] {
    print("The name of the airport is \(airportName).")
} else {
    print("That airport isn't in the airports dictionary.")
}
// Prints "The name of the airport is Dublin Airport."
```

*You can use subscript syntax to remove a key-value pair from a dictionary by assigning a value of `nil` for that key:*

첨자 구문을 사용해서 딕셔너리에서 키 값 쌍을 제거하려면 해당 키에 `nil` 값을 할당합니다.

```swift
airports["APL"] = "Apple International"
// "Apple International" isn't the real airport for APL, so delete it
airports["APL"] = nil
// APL has now been removed from the dictionary
```

*Alternatively, remove a key-value pair from a dictionary with the `removeValue(forKey:)` method. This method removes the key-value pair if it exists and returns the removed value, or returns `nil` if no value existed:*

혹은 `removeValue(forKey:)` 메서드를 사용해서 딕셔너리에서 키-값 쌍을 제거합니다. 이 메서드는 키-값 쌍이 있으면 제거하고 제거한 값을 반환하거나 값이 없으면 `nil`을 반환합니다.

```swift
if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary doesn't contain a value for DUB.")
}
// Prints "The removed airport's name is Dublin Airport."
```

### *Iterating Over a Dictionary : 딕셔너리를 통해 반복*

*You can iterate over the key-value pairs in a dictionary with a `for`-`in` loop. Each item in the dictionary is returned as a `(key, value)` tuple, and you can decompose the tuple’s members into temporary constants or variables as part of the iteration:*

`for`-`in` 루프가 있는 딕셔너리의 키-값 쌍에 대해 반복할 수 있습니다. 딕셔너리의 각 항목은 `(key, value)` 튜플로 반환되며, 반복의 일부로 튜플의 구성원을 임시 상수 혹은 변수로 분해할 수 있습니다.

```swift
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// LHR: London Heathrow
// YYZ: Toronto Pearson
```

*For more about the `for`-`in` loop, see [For-In Loops](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID121).*

`for`-`in` 루프에 대한 더 많은 정보는 [링크]를 확인하세요.

*You can also retrieve an iterable collection of a dictionary’s keys or values by accessing its `keys` and `values` properties:*

또한 다음과 같은 `key` 및 `values` 속성에 엑세스하여 딕셔너리의 키 혹은 값 컬렉션을 검색할 수 있습니다.

```swift
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: LHR
// Airport code: YYZ

for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: London Heathrow
// Airport name: Toronto Pearson
```

*If you need to use a dictionary’s keys or values with an API that takes an `Array` instance, initialize a new array with the `keys` or `values` property:*

`Array` 인스턴스를 사용하는 API에서 딕셔너리의 키 혹은 값을 사용해야 하는 경우 `key` 또는 `values` 속성을 사용해서 새 배열을 초기화합니다.

```swift
let airportCodes = [String](airports.keys)
// airportCodes is ["LHR", "YYZ"]

let airportNames = [String](airports.values)
// airportNames is ["London Heathrow", "Toronto Pearson"]
```

*Swift’s `Dictionary` type doesn’t have a defined ordering. To iterate over the keys or values of a dictionary in a specific order, use the `sorted()` method on its `keys` or `values` property.*

Swift의 딕셔너리형은 순서가 정해져 있지 않습니다. 딕셔너리의 키 혹은 값을 특정 순서로 반복하려면 해당 `key` 혹은 `values` 속성에서 `sorted()` 메서드를 사용합니다.
