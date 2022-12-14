## *Accessing and Modifying a String : 문자열 엑세스 및 수정*

*You access and modify a string through its methods and properties, or by using subscript syntax.*

메소드 및 속성을 사용하거나 첨자 구문을 사용해서 문자열에 엑세스하고 수정할 수 있습니다.

### *String Indices : 문자열 인덱스*

*Each `String` value has an associated index type, `String.Index`, which corresponds to the position of each `Character` in the string.*

각 `String` 값에는 연관된 인덱스 유형으로 문자열에서 각 `Character`의 위치에 해당하는 `String.Index` 가 있습니다. 

*As mentioned above, different characters can require different amounts of memory to store, so in order to determine which `Character` is at a particular position, you must iterate over each Unicode scalar from the start or end of that `String`. For this reason, Swift strings can’t be indexed by integer values.*

위에서 언급한 것처럼, 문자마다 저장할 메모리 양이 다를 수 있으므로 어떤 문자가 특정 위치에 있는지 확인하려면 해당 `String`의 시작이나 끝에서 각 유니코드 스칼라에 대해 반복해야 합니다. 이러한 이유로 Swift 문자열은 정수 값으로 인덱싱할 수 없습니다. 

*Use the `startIndex` property to access the position of the first `Character` of a `String`. The `endIndex` property is the position after the last character in a `String`. As a result, the `endIndex` property isn’t a valid argument to a string’s subscript. If a `String` is empty, `startIndex` and `endIndex` are equal.*

`String`의 첫번째  `Character`에 접근하기 위해 `startIndex`프로퍼티를 사용합니다. `endIndex` 프로퍼티는 `String`의 마지막 `Character` 입니다. 따라서 endIndex 속성은 문자열 첨자에 대한 유효한 인수가 아닙니다. `String`이 비어있으면, `startIndex`나 `endIndex`는 동일합니다.

*You access the indices before and after a given index using the `index(before:)` and `index(after:)` methods of `String`. To access an index farther away from the given index, you can use the `index(_:offsetBy:)` method instead of calling one of these methods multiple times.*

String의 index(before:) 및 index(after:) 메서드를 사용해서 지정된 인덱스 전후의 인덱스에 엑세스합니다. 지정된 인덱스에서 더 멀리 떨어진 인덱스에 엑세스하려면 이러한 메서드 중 하나를 여러번 호출하는 대신,  `index(_:offsetBy:)` 메서드를 사용할 수 있습니다. 

*You can use subscript syntax to access the `Character` at a particular `String` index.*

첨자 구문을 사용해서 특정 `String` 인덱스의 `Character`에 접근할 수 있습니다.

```swift
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a
```

*Attempting to access an index outside of a string’s range or a `Character` at an index outside of a string’s range will trigger a runtime error.*

문자열 범위 밖의 인덱스 혹은 문자열 범위 밖의 인덱스의 `Character`에 엑세스하려고 하면 런타임 오류가 발생합니다.

```swift
greeting[greeting.endIndex] // Error
greeting.index(after: greeting.endIndex) // Error
```

*Use the `indices` property to access all of the indices of individual characters in a string.*

`indices` 속성을 사용해서 문자열 내 개별 문자의 모든 인덱스에 엑세스합니다. 

```swift
for index in greeting.indices {
    print("\(greeting[index]) ", terminator: "")
}
// Prints "G u t e n   T a g ! "
```

> *NOTE*
> 
> *You can use the `startIndex` and `endIndex` properties and the `index(before:)`, `index(after:)`, and `index(_:offsetBy:)` methods on any type that conforms to the `Collection` protocol. This includes `String`, as shown here, as well as collection types such as `Array`, `Dictionary`, and `Set`.*
> 
> `Collection` 프로토콜을 준수하는 모든 유형에서 `startIndex`와 `endIndex` 프로퍼티와 `index(before:)`, `index(after:)`, and`index(_:offsetBy:)` 메서드를 를 사용할 수 있습니다. 여기에는 여기서 보여진 `String`과 `Array`, `Dictionary`, `Set`등의 콜렉션 타입이 포함됩니다.

### *Inserting and Removing : 삽입 및 제거*

*To insert a single character into a string at a specified index, use the `insert(_:at:)` method, and to insert the contents of another string at a specified index, use the `insert(contentsOf:at:)` method.*

저장된 인덱스의 문자열에 단일 문자를 삽입하려면 `insert(_:at:)` 메서드를 사용하고, 지정된 인덱스에 다른 문자열의 내용을 삽입하려면 `insert(contentsOf: at:)`메서드를 사용합니다.

```swift
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"
```

*To remove a single character from a string at a specified index, use the `remove(at:)` method, and to remove a substring at a specified range, use the `removeSubrange(_:)` method:*

지정된 인덱스의 문자열에서 단일 문자를 제거하려면 `remove(at:)` 메서드를 사용하고, 지정된 범위에서 하위 문자열을 제거하려면  `removeSubrange(_:)` 메서드를 사용합니다. 

```swift
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there"

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome now equals "hello"
```

> *NOTE*
> 
> *You can use the `insert(_:at:)`, `insert(contentsOf:at:)`, `remove(at:)`, and `removeSubrange(_:)` methods on any type that conforms to the `RangeReplaceableCollection` protocol. This includes `String`, as s*hown here, as well as collection types such as `Array`, `Dictionary`, and `Set`.
> 
> `RangeReplaceableCollection` 프로토콜을 준수하는 모든 유형에서  `insert(_:at:)`, `insert(contentsOf:at:)`, `remove(at:)`, 그리고 `removeSubrange(_:)` 메서드를 사용할 수 있습니다. 여기에는 여기에 표시된 *과 같은 `String`과 `Array`, `Dictionary`, Set과 같은 컬렉션 유형이 포함됩니다. 
