## *Comparison Operators : 비교연산자*

*Swift supports the following comparison operators:*

스위프트는 다음의 비교 연산자를 지원합니다.

- *Equal to (`a == b`)* : 같음

- *Not equal to (`a != b`)* : 같지 않음

- *Greater than (`a > b`)* : 보다 큼

- *Less than (`a < b`)* : 보다 작음

- *Greater than or equal to (`a >= b`)* : 크거나 같음

- *Less than or equal to (`a <= b`)* : 작거나 같음

> *NOTE*
> 
> *Swift also provides two identity operators (`===` and `!==`), which you use to test whether two object references both refer to the same object instance. For more information, see [Identity Operators](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID90).*
> 
> 스위프트는 또한 두 객체 참조가 동일한 객체 인스턴스를 참조하는지 여부를 테스트하는 두 개의 아이덴티티 연산자 (`===`와 `!==`)를 제공합니다. 자세한 내용은 [링크]를 참조하세요.

*Each of the comparison operators returns a `Bool` value to indicate whether or not the statement is true:*

각각의 비교 연산자는 Bool 값을 반환하여 구문이 참인지 여부를 나타냅니다.

```swift
1 == 1   // true because 1 is equal to 1
2 != 1   // true because 2 isn't equal to 1
2 > 1    // true because 2 is greater than 1
1 < 2    // true because 1 is less than 2
1 >= 1   // true because 1 is greater than or equal to 1
2 <= 1   // false because 2 isn't less than or equal to 1
```

*Comparison operators are often used in conditional statements, such as the `if` statement:*

비교 연산자는 if 구문과 같은 조건문에서 자주 사용됩니다.

```swift
let name = "world"
if name == "world" {
    print("hello, world")
} else {
    print("I'm sorry \(name), but I don't recognize you")
}
// Prints "hello, world", because name is indeed equal to "world".
```

*For more about the `if` statement, see [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html).*

if 구문에 대한 자세한 내용은 [링크]를 확인하세요.

*You can compare two tuples if they have the same type and the same number of values. Tuples are compared from left to right, one value at a time, until the comparison finds two values that aren’t equal. Those two values are compared, and the result of that comparison determines the overall result of the tuple comparison. If all the elements are equal, then the tuples themselves are equal. For example:*

두 튜플의 타입과 값의 개수가 동일한 경우 두 튜플을 비교할 수 있습니다. 튜플은 한 번에 하나의 값씩 왼쪽에서 오른쪽으로 비교되며 비교가 동일하지 않은 두 값을 찾을 때까지 사용됩니다. 이 두 값을 비교하고 그 비교의 결과가 튜플 비교의 전체적인 결과를 결정합니다. 모든 요소가 동일하면 튜플 자체가 동일합니다. 예를 들어 :

```swift
(1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" aren't compared
(3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
(4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"
```

*In the example above, you can see the left-to-right comparison behavior on the first line. Because `1` is less than `2`, `(1, "zebra")` is considered less than `(2, "apple")`, regardless of any other values in the tuples. It doesn’t matter that `"zebra"` isn’t less than `"apple"`, because the comparison is already determined by the tuples’ first elements. However, when the tuples’ first elements are the same, their second elements are compared—this is what happens on the second and third line.*

위의 예에서는 첫번째 줄에서 왼쪽에서 오른쪽으로 비교하는 것을 확인할 수 있습니다. `1`은 `2`보다 작기 때문에 `(1, "zebra")` 는 튜플의 다른 값에 관계없이 `(2, "apple")`보다 작은 것으로 간주됩니다. 비교는 이미 튜플의 첫번째 요소에서 결정되었기 때문에 `zebra` 가 `apple`보다 작지 않아도 상관이 없습니다.

*Tuples can be compared with a given operator only if the operator can be applied to each value in the respective tuples. For example, as demonstrated in the code below, you can compare two tuples of type `(String, Int)` because both `String` and `Int` values can be compared using the `<` operator. In contrast, two tuples of type `(String, Bool)` can’t be compared with the `<` operator because the `<` operator can’t be applied to `Bool` values.*

그러나 튜플의 첫번째 요소가 같을 경우, 두번째 요소가 비교됩니다 - 이것은 두 번째 줄과 세번째 줄에서 발생합니다. 연산자가 각 튜플의 각 값에 적용될 수 있는 경우에만 튜플을 지정된 연산자와 비교할 수 있습니다. 예를 들어, 아래의 코드에서 증명한 것처럼, `String`과 `Int` 값을 모두 `<` 연산자를 사용하여 비교할 수 있기 때문에 `(String, Int)` 타입의 두 튜플을 비교할 수 있습니다. 반면, `(String, Bool)` 타입의 두 튜플은 `<` 연산자를 `Bool` 값에 적용할 수 없기 때문에 `<` 연산자와 비교할 수 없습니다. 

```swift
("blue", -1) < ("purple", 1)        // OK, evaluates to true
("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
```

> *NOTE*
> 
> *The Swift standard library includes tuple comparison operators for tuples with fewer than seven elements. To compare tuples with seven or more elements, you must implement the comparison operators yourself.*
> 
> Swift 표준 라이브러리에는 7개 미만의 요소를 가진 튜플에 대한 튜플 비교 연산자가 포함되어 있습니다. 튜플을 7개 이상의 요소와 비교하려면 비교 연산자를 직접 구현해야 합니다.
