## Subscript Options

Subscripts can take any number of input parameters, and these input parameters can be of any type. Subscripts can also return a value of any type.

Like functions, subscripts can take a varying number of parameters and provide default values for their parameters, as discussed in [Variadic Parameters](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID171) and [Default Parameter Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID169). However, unlike functions, subscripts can’t use in-out parameters.

A class or structure can provide as many subscript implementations as it needs, and the appropriate subscript to be used will be inferred based on the types of the value or values that are contained within the subscript brackets at the point that the subscript is used. This definition of multiple subscripts is known as *subscript overloading*.

While it’s most common for a subscript to take a single parameter, you can also define a subscript with multiple parameters if it’s appropriate for your type. The following example defines a `Matrix` structure, which represents a two-dimensional matrix of `Double` values. The `Matrix` structure’s subscript takes two integer parameters:

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

`Matrix` provides an initializer that takes two parameters called `rows` and `columns`, and creates an array that’s large enough to store `rows * columns` values of type `Double`. Each position in the matrix is given an initial value of `0.0`. To achieve this, the array’s size, and an initial cell value of `0.0`, are passed to an array initializer that creates and initializes a new array of the correct size. This initializer is described in more detail in [Creating an Array with a Default Value](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html#ID501).

You can construct a new `Matrix` instance by passing an appropriate row and column count to its initializer:

```swift
var matrix = Matrix(rows: 2, columns: 2)
```

The example above creates a new `Matrix` instance with two rows and two columns. The `grid` array for this `Matrix` instance is effectively a flattened version of the matrix, as read from top left to bottom right:

![](https://docs.swift.org/swift-book/_images/subscriptMatrix01_2x.png)

Values in the matrix can be set by passing row and column values into the subscript, separated by a comma:

```swift
matrix[0, 1] = 1.5
matrix[1, 0] = 3.2
```

These two statements call the subscript’s setter to set a value of `1.5` in the top right position of the matrix (where `row` is `0` and `column` is `1`), and `3.2` in the bottom left position (where `row` is `1` and `column` is `0`):

![](https://docs.swift.org/swift-book/_images/subscriptMatrix02_2x.png)

The `Matrix` subscript’s getter and setter both contain an assertion to check that the subscript’s `row` and `column` values are valid. To assist with these assertions, `Matrix` includes a convenience method called `indexIsValid(row:column:)`, which checks whether the requested `row` and `column` are inside the bounds of the matrix:

```swift
func indexIsValid(row: Int, column: Int) -> Bool {
    return row >= 0 && row < rows && column >= 0 && column < columns
}
```

An assertion is triggered if you try to access a subscript that’s outside of the matrix bounds:

```swift
let someValue = matrix[2, 2]
// This triggers an assert, because [2, 2] is outside of the matrix bounds.
```
