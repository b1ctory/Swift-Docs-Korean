## *Recursive Enumerations : 재귀 열거*

*A recursive enumeration is an enumeration that has another instance of the enumeration as the associated value for one or more of the enumeration cases. You indicate that an enumeration case is recursive by writing `indirect` before it, which tells the compiler to insert the necessary layer of indirection.*

재귀 열거는 하나 이상의 열거형 케이스에 대해 다른 열거형 인스턴스를 관련된 값으로 가지는 열거형입니다. 당신은 컴파일러에게 필요한 간접 레이어를 삽입하도록 지시하는 `indirect`를 앞에 써서 열거형 케이스가 재귀적임을 나타냅니다.

*For example, here is an enumeration that stores simple arithmetic expressions:*

예를 들어, 다음은 단순 산술 식을 저장하는 열거형입니다.

```swift
enum ArithmeticExpression {
    case number(Int)
    indirect case addition(ArithmeticExpression, ArithmeticExpression)
    indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```

*You can also write `indirect` before the beginning of the enumeration to enable indirection for all of the enumeration’s cases that have an associated value:*

또한 열거 시작 전에 `indirect`를 작성하여 연관된 값을 가진 열거의 모든 케이스에 대해 간접을 사용할 수 있습니다.

```swift
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```

*This enumeration can store three kinds of arithmetic expressions: a plain number, the addition of two expressions, and the multiplication of two expressions. The `addition` and `multiplication` cases have associated values that are also arithmetic expressions—these associated values make it possible to nest expressions. For example, the expression `(5 + 4) * 2` has a number on the right-hand side of the multiplication and another expression on the left-hand side of the multiplication. Because the data is nested, the enumeration used to store the data also needs to support nesting—this means the enumeration needs to be recursive. The code below shows the `ArithmeticExpression` recursive enumeration being created for `(5 + 4) * 2`:*

이 열거형은 세가지 종류의 산술 식을 저장할 수 있습니다: 즉, 일반 숫자, 두 표현식의 덧셈, 두 표현식의 곱셈입니다. `addition`과 `multiplication`은 산술적 표현식이기도 한 연관된 값을 가지고 있습니다. 이러한 연관된 값은 표현식을 중첩할 수 있게 합니다. 예를 들어, `(5 + 4) * 2`라는 표현식은 곱셈의 오른쪽에 숫자가 있고 곱셈의 왼쪽에 다른 표현식이 있습니다. 데이터가 중첩되기 때문에 데이터를 저장하는데 사용되는 열거형도 중첩을 지원해야 합니다. 즉, 열거형은 반복적이어야 합니다. 아래의 코드는 `(5 + 4) * 2`에 대해 생성되는 `ArithmeticExpression` 재귀 열거형을 보여줍니다.

```swift
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
let product = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(2))
```

*A recursive function is a straightforward way to work with data that has a recursive structure. For example, here’s a function that evaluates an arithmetic expression:*

재귀함수는 재귀 구조를 가진 데이터를 쉽게 처리할 수 있는 방법입니다. 예를 들어, 산술식을 평가하는 함수는 다음과 같습니다.

```swift
func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}

print(evaluate(product))
// Prints "18"
```

*This function evaluates a plain number by simply returning the associated value. It evaluates an addition or multiplication by evaluating the expression on the left-hand side, evaluating the expression on the right-hand side, and then adding them or multiplying them.*

이 함수는 연결된 값을 반환하는 것만으로 평수를 평가합니다. 그것은 왼쪽에 있는 표현식을 평가하고, 오른쪽에 있는 표현식을 평가한 다음, 그것들을 더하거나 곱하는 방법으로 덧셈이나 곱셈을 평가합니다.


