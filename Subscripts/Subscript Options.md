## *Subscript Options: 서브스크립트 옵션*

*Subscripts can take any number of input parameters, and these input parameters can be of any type. Subscripts can also return a value of any type.*

서브스크립트는 원하는 개수의 입력 매개 변수를 사용할 수 있으며 이러한 입력 매개 변수는 모든 타입일 수 있습니다. 서브스크립트는  모든 타입의 값을 반환할 수도 있습니다.

*Like functions, subscripts can take a varying number of parameters and provide default values for their parameters, as discussed in [Variadic Parameters](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID171) and [Default Parameter Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID169). However, unlike functions, subscripts can’t use in-out parameters.*

함수와 마찬가지로 서브스크립트는 [링크]와 [링크]에 설명된 대로 다양한 수의 매개 변수를 사용하고 매개변수에 기본값을 제공할 수 있습니다. 단, 함수와 달리  서브스크립트는 인아웃 파라메터를 사용할 수 없습니다.

*A class or structure can provide as many subscript implementations as it needs, and the appropriate subscript to be used will be inferred based on the types of the value or values that are contained within the subscript brackets at the point that the subscript is used. This definition of multiple subscripts is known as subscript overloading.*

클래스 또는 구조체는 필요한 만큼 많은 서브스크립트 구현을 제공할 수 있으며, 사용할 적절한 서브스크립트는 서브스크립트가 사용되는 지점의 서브스크립트 괄호 안에 포함된 값의 타입을 기반으로 유추됩니다. 여러 서브스크립트 대한 이러한 정의를 *서브스크립트 오버로딩* 이라고 합니다.

*While it’s most common for a subscript to take a single parameter, you can also define a subscript with multiple parameters if it’s appropriate for your type. The following example defines a `Matrix` structure, which represents a two-dimensional matrix of `Double` values. The `Matrix` structure’s subscript takes two integer parameters:*

서브스크립트가 단일 매개 변수를 사용하는 것이 가장 일반적이지만 타입에 적합한 경우 여러 매개 변수를 사용하여 서브스크립트를 정의할 수도 있습니다. 다음 예제는 `Double` 값의 2차원 행렬을 나타내는 `Matrix` 구조체를 정의합니다. `Matrix` 구조체의 서브스크립트는 두 개의 정수 매개 변수를 사용합니다:

```swift
struct Matrix {
    let rows: Int, columns: Int
    var grid: [Double]
    init(rows: Int, columns: Int) {
        self.rows = rows
        self.columns = columns
        grid = Array(repeating: 0.0, count: rows * columns)
    }
    func indexIsValid(row: Int, column: Int) -> Bool {
        return row >= 0 && row < rows && column >= 0 && column < columns
    }
    subscript(row: Int, column: Int) -> Double {
        get {
            assert(indexIsValid(row: row, column: column), "Index out of range")
            return grid[(row * columns) + column]
        }
        set {
            assert(indexIsValid(row: row, column: column), "Index out of range")
            grid[(row * columns) + column] = newValue
        }
    }
}
```

*`Matrix` provides an initializer that takes two parameters called `rows` and `columns`, and creates an array that’s large enough to store `rows * columns` values of type `Double`. Each position in the matrix is given an initial value of `0.0`. To achieve this, the array’s size, and an initial cell value of `0.0`, are passed to an array initializer that creates and initializes a new array of the correct size. This initializer is described in more detail in [Creating an Array with a Default Value](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html#ID501).*

`Matrix`는 `rows`와 `columns` 라는 두 가지 매개 변수를 사용하고 `Double` 타입의 `rows*column` 값을 저장하기에 충분한 크기의 배열을 생성하는 이니셜라이저를 제공합니다. 행렬의 각 위치에는 초기 값 `0.0`이 지정됩니다. 이를 위해 배열 크기와 초기 셀 값 `0.0`이 올바른 크기의 새 배열을 만들고 초기화하는 배열 이니셜라이저에 전달됩니다. 이 이니셜라이저에 대한 자세한 내용은 [링크]를 참조하십시오.

*You can construct a new `Matrix` instance by passing an appropriate row and column count to its initializer:*

적절한 행과 열 수를 이니셜라이저에 전달하여 새 `Matrix` 인스턴스를 구성할 수 있습니다:

```swift
var matrix = Matrix(rows: 2, columns: 2)
```

*The example above creates a new `Matrix` instance with two rows and two columns. The `grid` array for this `Matrix` instance is effectively a flattened version of the matrix, as read from top left to bottom right:*

위의 예제는 두 개의 행과 두 개의 열을 가진 새 `Matrix` 인스턴스를 만듭니다. 이 `Matrix` 인스턴스의 `grid` 배열은 왼쪽 위에서 오른쪽 아래로 읽혀지는 것처럼 사실상 매트릭스의 평평한 버전입니다:

*![](https://docs.swift.org/swift-book/_images/subscriptMatrix01_2x.png)*

*Values in the matrix can be set by passing row and column values into the subscript, separated by a comma:*

행 및 열 값을 쉼표로 구분하여 서브스크립트에 전달하여 행렬의 값을 설정할 수 있습니다:

```swift
matrix[0, 1] = 1.5
matrix[1, 0] = 3.2
```

*These two statements call the subscript’s setter to set a value of `1.5` in the top right position of the matrix (where `row` is `0` and `column` is `1`), and `3.2` in the bottom left position (where `row` is `1` and `column` is `0`):*

이 두 구문은 서브스크립트의 세터를 호출하여 행렬의 오른쪽 상단 위치(여기서 `row`은 `0`, `column`은 `1`)에 `1.5`의 값을 설정합니다. 왼쪽 아래 위치에 2가 있습니다(여기서 `row`은 `1`, `col`은 `0`):

*![](https://docs.swift.org/swift-book/_images/subscriptMatrix02_2x.png)*

*The `Matrix` subscript’s getter and setter both contain an assertion to check that the subscript’s `row` and `column` values are valid. To assist with these assertions, `Matrix` includes a convenience method called `indexIsValid(row:column:)`, which checks whether the requested `row` and `column` are inside the bounds of the matrix:*

`Matrix` 서브스크립트의 getter 및 setter에는 서브스크립트의 `row` 및 `column` 값이 유효한지 확인하기 위한 assertion이 모두 포함되어 있습니다. 이러한 주장을 지원하기 위해 `Matrix`는 요청된 `row`와 `column`이 매트릭스의 경계 안에 있는지 확인하는 `indexIsValid(행:column:)`라는 편리한 메서드를 포함합니다:

```swift
func indexIsValid(row: Int, column: Int) -> Bool {
    return row >= 0 && row < rows && column >= 0 && column < columns
}
```

*An assertion is triggered if you try to access a subscript that’s outside of the matrix bounds:*

행렬 경계를 벗어난 서브스크립트에 액세스하려고 하면 어설션이 트리거됩니다:

```swift
let someValue = matrix[2, 2]
// This triggers an assert, because [2, 2] is outside of the matrix bounds.
```
