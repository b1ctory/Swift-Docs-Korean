## *Arrays : 배열*

*An array stores values of the same type in an ordered list. The same value can appear in an array multiple times at different positions.*

배열은 동일한 타입의 값을 순서 목록에 저장합니다. 동일한 값이 배열에서 서로 다른 위치에 여러번 나타날 수 있습니다. 

> *NOTE*
> 
> *Swift’s `Array` type is bridged to Foundation’s `NSArray` class.*
> 
> 스위프트의 `Array` 타입은 Foundation의 `NSArray` 클래스에 연결된 것입니다.
> 
> *For more information about using `Array` with Foundation and Cocoa, see [Bridging Between Array and NSArray](https://developer.apple.com/documentation/swift/array#2846730).*
> 
> Foundation 및 Cocoa 에서 `Array`를 사용하는 방법에 대한 자세한 내용은 [링크]를 참조하세요.

### *Array Type Shorthand Syntax : 배열 타입 단축 구문*

*The type of a Swift array is written in full as `Array<Element>`, where `Element` is the type of values the array is allowed to store. You can also write the type of an array in shorthand form as `[Element]`. Although the two forms are functionally identical, the shorthand form is preferred and is used throughout this guide when referring to the type of an array.*

Swift 배열의 유형은 전체를 `Array<Element>` 로 기록하며, 여기서 `Element`는 배열이 저장할 수 있는 값의 유형입니다. 배열의 타입을 속기 형식으로 `[Element]`로 쓸 수도 있습니다. 두 가지 형태가 기능적으로 동일하지만, 배열의 타입을 언급할 때는 간략한 형태가 선호되며, 본 안내서 전반에 걸쳐 사용됩니다.

### *Creating an Empty Array : 빈 배열 만들기*

*You can create an empty array of a certain type using initializer syntax:*

initializer 구문을 사용해서 특정 타입의 빈 배열을 생성할 수 있습니다. 

```swift
var someInts: [Int] = []
print("someInts is of type [Int] with \(someInts.count) items.")
// Prints "someInts is of type [Int] with 0 items."
```

*Note that the type of the `someInts` variable is inferred to be `[Int]` from the type of the initializer.*

`somInts` 변수의 타입은 `initializer` 의 타입으로부터 `[Int]`로 추론된다는 점에 유의하세요.

*Alternatively, if the context already provides type information, such as a function argument or an already typed variable or constant, you can create an empty array with an empty array literal, which is written as `[]` (an empty pair of square brackets):*

또는 컨텍스트가 이미 함수 인수나 이미 입력된 변수 혹은 상수와 같은 타입 정보를 제공하는 경우 빈 배열 리터럴을 사용해서 빈 배열을 만들 수 있습니다. 이 배열 리터럴은 `[]` (빈 대괄호 쌍) 으로 기록됩니다. 

```swift
someInts.append(3)
// someInts now contains 1 value of type Int
someInts = []
// someInts is now an empty array, but is still of type [Int]
```

### *Creating an Array with a Default Value : 기본 값으로 배열 생성*

*Swift’s `Array` type also provides an initializer for creating an array of a certain size with all of its values set to the same default value. You pass this initializer a default value of the appropriate type (called `repeating`): and the number of times that value is repeated in the new array (called `count`):*

Swift의 `Array` 타입은 모든 값이 동일한 기본값으로 설정된 특정 크기의 배열을 생성하기 위한 Initializer를 제공합니다. 이 Initializer를 적절한 타입의 기본값 (`repeating`이라고 함)과 해당 값이 새 배열에서 반복되는 횟수 (`count` 라고 불림)로 전달합니다.

```swift
var threeDoubles = Array(repeating: 0.0, count: 3)
// threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]
```

### *Creating an Array by Adding Two Arrays Together : 두 배열을 더해 배열 생성*

*You can create a new array by adding together two existing arrays with compatible types with the addition operator (`+`). The new array’s type is inferred from the type of the two arrays you add together:*

추가 연산자 (`+`)를 사용해서 호환되는 타입의 기존 배열 두 개를 함께 추가해서 새 배열을 생성할 수 있습니다. 새 배열의 타입은 함께 추가하는 두 배열의 타입에서 유추됩니다. 

```swift
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]

var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

### *Creating an Array with an Array Literal : 배열 리터럴을 사용해서 배열 생성*

*You can also initialize an array with an array literal, which is a shorthand way to write one or more values as an array collection. An array literal is written as a list of values, separated by commas, surrounded by a pair of square brackets:*

배열 리터럴을 사용해서 배열을 초기화할 수도 있습니다. 이는 하나 이상의 값을 배열 컬렉션으로 쓰는 간단한 방법입니다. 배열 리터럴은 쉼표로 구분되고 한 쌍의 대괄호로 둘러싸인 값 목록으로 작성됩니다.

```swift
[value 1, value 2, value 3]
```

*The example below creates an array called `shoppingList` to store `String` values:*

아래 예제에서는 `String`값을 저장하기 위해 `shoppingList`라는 배열을 만듭니다.

```swift
var shoppingList: [String] = ["Eggs", "Milk"]
// shoppingList has been initialized with two initial items
```

*The `shoppingList` variable is declared as “an array of string values”, written as `[String]`. Because this particular array has specified a value type of `String`, it’s allowed to store `String` values only. Here, the `shoppingList` array is initialized with two `String` values (`"Eggs"` and `"Milk"`), written within an array literal.*

`shoppingList` 변수는 `[String]`으로 작성된 "String 값의 배열"로 선언됩니다. 이 배열은 값 타입인 `String`을 지정했기 때문에 `String` 값만 저장할 수 있습니다. 여기서 shoppingList 배열은 배열 리터럴 내에 쓰여진 두 개의 `String` 값 (`Eggs` 와 `Milk`)로 초기화됩니다.

> *NOTE*
> 
> *The `shoppingList` array is declared as a variable (with the `var` introducer) and not a constant (with the `let` introducer) because more items are added to the shopping list in the examples below.*
> 
> 아래 예제에서 `shoppingList` 배열에 더 많은 항목이 추가되므로 `shoppingList` 배열은 상수 (`let`)가 아닌 변수(`var`)로 선언됩니다. 

*In this case, the array literal contains two `String` values and nothing else. This matches the type of the `shoppingList` variable’s declaration (an array that can only contain `String` values), and so the assignment of the array literal is permitted as a way to initialize `shoppingList` with two initial items.*

이 경우, 배열 리터럴에는 두 개의 `String` 값만 포함되며 다른 값은 포함되지 않습니다. 이는 `shoppingList` 변수의 선언 유형 (`String` 값만 포함할 수 있는 배열)과 일치하므로 두 개의 초기 항목으로 `shoppingList`를 초기화하는 방법으로 배열 리터럴 할당이 허용됩니다.

*Thanks to Swift’s type inference, you don’t have to write the type of the array if you’re initializing it with an array literal containing values of the same type. The initialization of `shoppingList` could have been written in a shorter form instead:*

Swift 타입 추론 덕분에 동일한 타입의 값을 포함하는 배열 리터럴로 초기화하는 경우 배열의 타입을 작성할 필요가 없습니다. `shoppingList`의 초기화는 다음과 같이 더 짧은 형식으로 작성될 수 있습니다.

```swift
var shoppingList = ["Eggs", "Milk"]
```

*Because all values in the array literal are of the same type, Swift can infer that `[String]` is the correct type to use for the `shoppingList` variable.*

배열 리터럴의 모든 값이 동일한 타입이기 때문에 Swift는 `[String]`이 `shoppingList` 변수에 사용할 올바른 유형이라고 추론할 수 있습니다.

### *Accessing and Modifying an Array : 배열 접근 및 수정*

*You access and modify an array through its methods and properties, or by using subscript syntax.*

메소드 및 속성을 사용하거나 첨자 구문을 사용해서 배열에 접근하고 수정합니다.

*To find out the number of items in an array, check its read-only `count` property:*

배열의 항목 수를 알아보려면 읽기 전용 프로퍼티인 `count`를 확인하세요. 

```swift
print("The shopping list contains \(shoppingList.count) items.")
// Prints "The shopping list contains 2 items."
```

*Use the Boolean `isEmpty` property as a shortcut for checking whether the `count` property is equal to `0`:*

`count` 프로퍼티가 `0`과 같은지 체크하기 위한 지름길로 `Boolean` 타입의 `isEmpty` 프로퍼티를 사용하세요.

```swift
if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list isn't empty.")
}
// Prints "The shopping list isn't empty."
```

*You can add a new item to the end of an array by calling the array’s `append(_:)` method:*

배열의 `append(_:)` 메서드를 호출해서 배열 끝에 새 항목을 추가할 수 있습니다. 

```swift
shoppingList.append("Flour")
// shoppingList now contains 3 items, and someone is making pancakes
```

*Alternatively, append an array of one or more compatible items with the addition assignment operator (`+=`):*

대신에, 추가 할당 연산자 (`+=`) 와 호환되는 항목의 배열을 추가합니다. 

```swift
shoppingList += ["Baking Powder"]
// shoppingList now contains 4 items
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList now contains 7 items
```

*Retrieve a value from the array by using subscript syntax, passing the index of the value you want to retrieve within square brackets immediately after the name of the array:*

첨자 구문을 사용해서 배열 이름 바로 뒤에 있는 각 괄호 안에 검색할 값의 인덱스를 전달해서 배열에서 값을 검색합니다. 

```swift
var firstItem = shoppingList[0]
// firstItem is equal to "Eggs"
```

> *NOTE*
> 
> *The first item in the array has an index of `0`, not `1`. Arrays in Swift are always zero-indexed.*
> 
> 배열의 첫번째 항목의 인덱스는 `1`이 아니라 `0`입니다. Swift의 배열은 항상 0으로 인덱싱됩니다.

*You can use subscript syntax to change an existing value at a given index:*

첨자 구문을 사용해서 지정된 인덱스의 기존 값을 변경할 수 있습니다. 

```swift
shoppingList[0] = "Six eggs"
// the first item in the list is now equal to "Six eggs" rather than "Eggs"
```

*When you use subscript syntax, the index you specify needs to be valid. For example, writing `shoppingList[shoppingList.count] = "Salt"` to try to append an item to the end of the array results in a runtime error.*

첨자 구문을 사용할 때는 지정한 인덱스가 유효해야 합니다. 예를 들어, 배열 끝에 항목을 추가하려고   `shoppingList[shoppingList.count] = "Salt"`를 쓰면 런타임 오류가 발생합니다.

*You can also use subscript syntax to change a range of values at once, even if the replacement set of values has a different length than the range you are replacing. The following example replaces `"Chocolate Spread"`, `"Cheese"`, and `"Butter"` with `"Bananas"` and `"Apples"`:*

또한 대체할 값 집합의 길이가 대체할 값 범위와 다른 경우에도 첨자 구문을 사용해서 값 범위를 한 번에 변경할 수 있습니다. 다음 예시에서는  `"Chocolate Spread"`, `"Cheese"`,  `"Butter"` 를 `"Bananas"` 와 `"Apples"`로 바꿉니다.

```swift
shoppingList[4...6] = ["Bananas", "Apples"]
// shoppingList now contains 6 items
```

*To insert an item into the array at a specified index, call the array’s `insert(_:at:)` method:*

지정된 인덱스의 배열에 항목을 삽입하려면 배열의 `insert(_:at:)` 메서드를 호출합니다.

```swift
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList now contains 7 items
// "Maple Syrup" is now the first item in the list
```

*This call to the `insert(_:at:)` method inserts a new item with a value of `"Maple Syrup"` at the very beginning of the shopping list, indicated by an index of `0`.*

`insert(_:at:)` 메서드에 대한 호출은 `Maple Syrup` 값을 가진 새 항목을 `0`의 인덱스로 표시된 쇼핑 목록의 맨 앞에 삽입합니다. 

*Similarly, you remove an item from the array with the `remove(at:)` method. This method removes the item at the specified index and returns the removed item (although you can ignore the returned value if you don’t need it):*

마찬가지로 `remove(at:)` 메서드를 사용해서 배열에서 항목을 제거합니다. 이 메서드는 지정된 인덱스에서 항목을 제거하고 제거된 항목을 반환합니다. (필요하지 않은 경우 반환된 값을 무시할 수도 있습니다.)

```swift
let mapleSyrup = shoppingList.remove(at: 0)
// the item that was at index 0 has just been removed
// shoppingList now contains 6 items, and no Maple Syrup
// the mapleSyrup constant is now equal to the removed "Maple Syrup" string
```

> *NOTE*
> 
> *Any gaps in an array are closed when an item is removed, and so the value at index `0` is once again equal to `"Six eggs"`:*
> 
> 항목이 제거되면 배열의 간격이 모두 닫히므로 인덱스 `0`의 값은 다시 `Six eggs`과 같습니다.

```swift
firstItem = shoppingList[0]
// firstItem is now equal to "Six eggs"
```

*If you want to remove the final item from an array, use the `removeLast()` method rather than the `remove(at:)` method to avoid the need to query the array’s `count` property. Like the `remove(at:)` method, `removeLast()` returns the removed item:*

배열에서 마지막 항목을 제거하려면 배열의 count 프로퍼티를 쿼리할 필요가 없도록 `remove(at:)` 메서드 대신 `removeLast()` 메서드를 사용하세요. `remove(at:)` 메서드와 마찬가지로 `removeLast()`는 제거된 항목을 반환합니다.

```swift
let apples = shoppingList.removeLast()
// the last item in the array has just been removed
// shoppingList now contains 5 items, and no apples
// the apples constant is now equal to the removed "Apples" string
```

### *Iterating Over an Array : 배열에서의 반복*

*You can iterate over the entire set of values in an array with the `for`-`in` loop:*

`for`-`in` 루프를 사용해서 배열의 전체 값 집합에 대해 반복할 수 있습니다.

```swift
for item in shoppingList {
    print(item)
}
// Six eggs
// Milk
// Flour
// Baking Powder
// Bananas
```

*If you need the integer index of each item as well as its value, use the `enumerated()` method to iterate over the array instead. For each item in the array, the `enumerated()` method returns a tuple composed of an integer and the item. The integers start at zero and count up by one for each item; if you enumerate over a whole array, these integers match the items’ indices. You can decompose the tuple into temporary constants or variables as part of the iteration:*

각 항목의 정수 인덱스와 해당 값이 필요한 경우 `enumerated()` 메서드를 사용해서 배열을 반복합니다. 배열의 각 항목에 대해 `enumerated()` 메서드는 정수와 아이템으로 구성된 튜플을 반환합니다. 정수는 0에서 시작해서 각 항목에 대해 하나씩 카운트 됩니다. 전체 배열에 걸쳐 열거하면 이러한 정수는 항목의 인덱스와 일치합니다. 반복의 일부로 튜플을 임시 상수 혹은 변수로 분해할 수 있습니다. 

```swift
for (index, value) in shoppingList.enumerated() {
    print("Item \(index + 1): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
```

*For more about the `for`-`in` loop, see [For-In Loops](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID121).*

`for`-`in` 루프에 대한 더 많은 설명은 [링크]를 참조하세요.


