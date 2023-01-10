## *Subscript Syntax : 서브스크립트 구문*

*Subscripts enable you to query instances of a type by writing one or more values in square brackets after the instance name. Their syntax is similar to both instance method syntax and computed property syntax. You write subscript definitions with the `subscript` keyword, and specify one or more input parameters and a return type, in the same way as instance methods. Unlike instance methods, subscripts can be read-write or read-only. This behavior is communicated by a getter and setter in the same way as for computed properties:*

서브스크립트를 사용하면 인스턴스 이름 뒤에 하나 이상의 값을 대괄호로 작성하여 타입의 인스턴스를 쿼리할 수 있습니다. 이들의 구문은 인스턴스 메서드 구문 및 연산 프로퍼티 구문과 유사합니다. 인스턴스 메서드와 동일한 방법으로 `subscript` 키워드를 사용하여 서브스크립트 정의를 작성하고 하나 이상의 입력 매개 변수 및 반환 타입을 지정합니다. 인스턴스 메서드와 달리 서브스크립트는 읽기-쓰기 또는 읽기 전용일 수 있습니다. 이 동작은 연산 프로퍼티와 동일한 방식으로 게터 및 세터에 의해 전달됩니다 :

```swift
subscript(index: Int) -> Int {
    get {
        // Return an appropriate subscript value here.
    }
    set(newValue) {
        // Perform a suitable setting action here.
    }
}
```

*The type of `newValue` is the same as the return value of the subscript. As with computed properties, you can choose not to specify the setter’s `(newValue)` parameter. A default parameter called `newValue` is provided to your setter if you don’t provide one yourself.*

`newValue`의 타입은 서브스크립트의 반환 값과 동일합니다. 연산 프로퍼티와 마찬가지로 세터의 `'(newValue)'` 매개 변수를 지정하지 않도록 선택할 수 있습니다. 세터를 직접 제공하지 않으면 `newValue`라는 기본 매개 변수가 세터에 제공됩니다.

*As with read-only computed properties, you can simplify the declaration of a read-only subscript by removing the `get` keyword and its braces:*

읽기 전용 연산 프로퍼티와 마찬가지로 `get` 키워드와 해당 괄호를 제거하여 읽기 전용 서브스크립트의 선언을 단순화할 수 있습니다:

```swift
subscript(index: Int) -> Int {
    // Return an appropriate subscript value here.
}
```

*Here’s an example of a read-only subscript implementation, which defines a `TimesTable` structure to represent an n-times-table of integers:*

다음은 n-times-table의 정수를 나타내는 `TimesTable` 구조체를 정의하는 읽기 전용 서브스크립트 구현의 예입니다:

```swift
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
print("six times three is \(threeTimesTable[6])")
// Prints "six times three is 18"
```

*In this example, a new instance of `TimesTable` is created to represent the three-times-table. This is indicated by passing a value of `3` to the structure’s `initializer` as the value to use for the instance’s `multiplier` parameter.*

이 예에서는 three-times-table을 나타내기 위해 `TimesTable`의 새 인스턴스가 생성됩니다. 이는 인스턴스의 `multiplier` 매개 변수에 사용할 값으로 구조의 `initializer`에 `3`의 값을 전달함으로써 표시됩니다.

*You can query the `threeTimesTable` instance by calling its subscript, as shown in the call to `threeTimesTable[6]`. This requests the sixth entry in the three-times-table, which returns a value of `18`, or `3` times `6`.*

`threeTimesTable[6]`에 대한 호출에 표시된 것처럼 해당 서브스크립트를 호출하여 `threeTimesTable` 인스턴스를 쿼리할 수 있습니다. 이것은 `18` 또는 `3` 곱하기 `6`의 값을 반환하는 three-times-table의 여섯 번째 항목을 요청합니다.

> *NOTE*
> 
> *An n-times-table is based on a fixed mathematical rule. It isn’t appropriate to set `threeTimesTable[someIndex]` to a new value, and so the subscript for `TimesTable` is defined as a read-only subscript.*
> 
> n-times-table은 고정된 수학적 규칙을 기반으로 합니다. `threeTimesTable[someIndex]`을 새 값으로 설정하는 것은 적절하지 않으므로 `TimesTable`의 서브스크립트는 읽기 전용 서브스크립트로 정의됩니다.


