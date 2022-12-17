## *For-In Loops : For-in 루프*

*You use the `for`-`in` loop to iterate over a sequence, such as items in an array, ranges of numbers, or characters in a string.*

배열의 항목, 숫자의 범위 혹은 문자열의 문자와 같은 시퀀스를 반복하려면 `for`-`in` 루프를 사용합니다.

*This example uses a `for`-`in` loop to iterate over the items in an array:*

이 예시에서는 `for`-`in` 루프를 사용해서 배열의 항목을 반복합니다.

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!
```

*You can also iterate over a dictionary to access its key-value pairs. Each item in the dictionary is returned as a `(key, value)` tuple when the dictionary is iterated, and you can decompose the `(key, value)` tuple’s members as explicitly named constants for use within the body of the `for`-`in` loop. In the code example below, the dictionary’s keys are decomposed into a constant called `animalName`, and the dictionary’s values are decomposed into a constant called `legCount`.*

딕셔너리를 반복해서 키-값 쌍에 엑세스할 수도 있습니다. 딕셔너리의 각 항목은 딕셔너리가 반복될 때 `(key, value)` 튜플로 반환되며, `(key, value)` 튜플의 구성원을 `for`-`in` 루프의 본문 내에서 사용하기 위해 명시적으로 명명된 상수로 분해할 수 있습니다. 아래의 코드 예제에서 딕셔너리의 키는 `animalName`이라는 상수로 분해되고, 딕셔너리의 값은 `legCount`라는 상수로 분해됩니다.

```swift
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// cats have 4 legs
// ants have 6 legs
// spiders have 8 legs
```

*The contents of a `Dictionary` are inherently unordered, and iterating over them doesn’t guarantee the order in which they will be retrieved. In particular, the order you insert items into a `Dictionary` doesn’t define the order they’re iterated. For more about arrays and dictionaries, see [Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html).*

`딕셔너리`의 내용은 본질적으로 순서가 정해져있지 않고 반복된다고 해서 검색 순서가 보장되는 것은 아닙니다. 특히 `딕셔너리`에 항목을 삽입하는 순서는 항목이 반복되는 순서를 정의하지 않습니다. 배열 및 딕셔너리에 대한 자세한 내용은 Collection Types 링크를 확인하세요.

*You can also use `for`-`in` loops with numeric ranges. This example prints the first few entries in a five-times table:*

숫자 범위에 for-in 루프를 사용할 수도 있습니다. 다음 예제에서는 five-times 테이블에서 첫번째 몇 엔트리를 인쇄합니다.

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

*The sequence being iterated over is a range of numbers from `1` to `5`, inclusive, as indicated by the use of the closed range operator (`...`). The value of `index` is set to the first number in the range (`1`), and the statements inside the loop are executed. In this case, the loop contains only one statement, which prints an entry from the five-times table for the current value of `index`. After the statement is executed, the value of `index` is updated to contain the second value in the range (`2`), and the `print(_:separator:terminator:)` function is called again. This process continues until the end of the range is reached.*

위에서 반복되는 시퀀스는 닫힌 범위 연산자 (`...`)를 사용해서 표시된 것처럼 `1`부터 `5`까지의 숫자 범위입니다. `index`값은 범위 내의 첫 번째 숫자 (`1`)로 설정되며, 루프 내의 구문이 실행됩니다. 이 경우 루프에는 `index`의 현재 값에 대한 five-times 테이블의 항목을 인쇄하는 구문이 하나만 포함됩니다. 구문이 실행되면 index 값이 두 번째 값(`2`)을 포함하도록 업데이트되고 `print(_: separator: terminator:)` 함수가 다시 호출됩니다. 이 프로세스는 범위의 끝에 도달할 때까지 계속됩니다.

*In the example above, `index` is a constant whose value is automatically set at the start of each iteration of the loop. As such, `index` doesn’t have to be declared before it’s used. It’s implicitly declared simply by its inclusion in the loop declaration, without the need for a `let` declaration keyword.*

위의 예시에서 `index`는 루프의 반복이 시작될 때 값이 자동으로 설정되는 상수입니다. 따라서 `index`는 사용 전에 선언할 필요가 없습니다. 그것은 단순히 루프 선언에 포함됨으로써 암묵적으로 선언되며, `let` 선언 키워드가 필요하지 않습니다.

*If you don’t need each value from a sequence, you can ignore the values by using an underscore in place of a variable name.*

시퀀스의 각 값이 필요하지 않은 경우 변수 이름 대신 밑줄을 사용해서 값을 무시할 수 있습니다.

```swift
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// Prints "3 to the power of 10 is 59049"
```

*The example above calculates the value of one number to the power of another (in this case, `3` to the power of `10`). It multiplies a starting value of `1` (that is, `3` to the power of `0`) by `3`, ten times, using a closed range that starts with `1` and ends with `10`. For this calculation, the individual counter values each time through the loop are unnecessary—the code simply executes the loop the correct number of times. The underscore character (`_`) used in place of a loop variable causes the individual values to be ignored and doesn’t provide access to the current value during each iteration of the loop.*

위의 예시는 하나의 숫자 대 다른 숫자의 거듭제곱 값을 계산합니다. (이 경우 `3`의 `10` 거듭제곱) 이것은 `1`로 시작해서 `10`으로 끝나는 닫힌 범위를 사용해서 `1` (즉, `3`의 `0` 거듭제곱)의 시작값에 `3`을 `10`번 곱합니다. 이 계산을 위해서는 루프를 통과할 때마다 개별 카운터 값이 필요하지 않으며, 코드는 정확한 횟수만큼 루프를 실행할 뿐입니다. 루프 변수 대신 사용되는 밑줄 문자(`_`)는 개별 값을 무시하게하고 루프의 각 반복 동안 현제 값에 대한 엑세스를 제공하지 않습니다.

*In some situations, you might not want to use closed ranges, which include both endpoints. Consider drawing the tick marks for every minute on a watch face. You want to draw `60` tick marks, starting with the `0` minute. Use the half-open range operator (`..<`) to include the lower bound but not the upper bound. For more about ranges, see [Range Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html#ID73).*

경우에 따라 두 끝 점을 포함하는 닫힌 범위를 사용하지 않을 수 있습니다. 시계에 1분마다 눈금을 그리는 것을 생각해보세요. `0`분부터 시작해서 `60`개의 눈금을 그립니다. 하한은 포함하지만 상한은 포함하지 않는 반열림 범위 연산자를 사용하세요. 범위에 대한 자세한 내용은 [링크]를 확인하세요.

```swift
let minutes = 60
for tickMark in 0..<minutes {
    // render the tick mark each minute (60 times)
}
```

*Some users might want fewer tick marks in their UI. They could prefer one mark every `5` minutes instead. Use the `stride(from:to:by:)` function to skip the unwanted marks.*

일부 사용자는 UI에서 더 적은 체크 표시를 원할 수 있습니다. 대신 5분마다 1개씩 표시하는 것이 좋습니다. `stride(from:to:by:)` 를 사용해서 원하지 않는 표시를 건너뛰세요. 

```swift
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}
```

*Closed ranges are also available, by using `stride(from:through:by:)` instead:*

`stride(from:through:by:)` 를 대신 사용해서 닫힌 범위 또한 가능합니다. 

```swift
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)
}
```

*The examples above use a `for`-`in` loop to iterate ranges, arrays, dictionaries, and strings. However, you can use this syntax to iterate any collection, including your own classes and collection types, as long as those types conform to the [`Sequence`](https://developer.apple.com/documentation/swift/sequence) protocol.*

위의 예들은 범위, 배열, 딕셔너리 및 문자열을 반복하기 위해 `for`-`in` 루프를 사용합니다. 그러나 이러한 유형이 Sequence 프로토콜을 준수하는 경우 이 구문을 사용해서 사용자 자신의 클래스 및 컬렉션 타입을 포함한 모든 컬렉션을 반복할 수 있습니다.
