## *Custom Operators : 사용자 지정 연산자*

*You can declare and implement your own custom operators in addition to the standard operators provided by Swift. For a list of characters that can be used to define custom operators, see [Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/lexicalstructure#Operators).*

 Swift에서 제공하는 표준 연산자 외에 사용자 지정 연산자를 선언하고 구현할 수 있습니다. 사용자 지정 연산자를 정의하는 데 사용할 수 있는 문자 목록은 [링크]를 참조하십시오.

*New operators are declared at a global level using the `operator` keyword, and are marked with the `prefix`, `infix` or `postfix` modifiers:*

새 연산자는 `operator` 키워드를 사용하여 전역 수준에서 선언되며 `prefix`, `infix` 또는 `postfix` 수식자로 표시됩니다.

```swift
prefix operator +++
```

*The example above defines a new prefix operator called `+++`. This operator doesn’t have an existing meaning in Swift, and so it’s given its own custom meaning below in the specific context of working with `Vector2D` instances. For the purposes of this example, `+++` is treated as a new “prefix doubling” operator. It doubles the `x` and `y` values of a `Vector2D` instance, by adding the vector to itself with the addition assignment operator defined earlier. To implement the `+++` operator, you add a type method called `+++` to `Vector2D` as follows:*

위의 예는 `+++`라는 새로운 접두사 연산자를 정의합니다. 이 연산자는 Swift에서 기존 의미가 없으므로 `Vector2D` 인스턴스로 작업하는 특정 컨텍스트에서 아래에 고유한 맞춤 의미가 부여됩니다. 이 예시에서는 `+++`를 새로운 '접두사 이중화' 연산자로 취급합니다. 앞에서 정의한 더하기 할당 연산자를 사용하여 벡터를 자체에 추가하여 `Vector2D` 인스턴스의 `x` 및 `y` 값을 두 배로 늘립니다. `+++` 연산자를 구현하려면 다음과 같이 `+++`라는 타입 메서드를 `Vector2D`에 추가합니다.

```swift
extension Vector2D {
    static prefix func +++ (vector: inout Vector2D) -> Vector2D {
        vector += vector
        return vector
    }
}

var toBeDoubled = Vector2D(x: 1.0, y: 4.0)
let afterDoubling = +++toBeDoubled
// toBeDoubled now has values of (2.0, 8.0)
// afterDoubling also has values of (2.0, 8.0)
```

### *Precedence for Custom Infix Operators : 사용자 지정 중위 연산자의 우선 순위*

*Custom infix operators each belong to a precedence group. A precedence group specifies an operator’s precedence relative to other infix operators, as well as the operator’s associativity. See [Precedence and Associativity](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/advancedoperators#Precedence-and-Associativity) for an explanation of how these characteristics affect an infix operator’s interaction with other infix operators.*

맞춤 중위 연산자는 각각 우선 순위 그룹에 속합니다. 우선 순위 그룹은 연산자의 연관성뿐만 아니라 다른 중위 연산자에 상대적인 연산자의 우선 순위를 지정합니다. 이러한 특성이 중위 연산자의 다른 중위 연산자와의 상호 작용에 영향을 끼칩니다.

*A custom infix operator that isn’t explicitly placed into a precedence group is given a default precedence group with a precedence immediately higher than the precedence of the ternary conditional operator.*

우선 순위 그룹에 명시적으로 배치되지 않은 사용자 지정 중위 연산자에는 삼항 조건 연산자의 우선 순위보다 바로 높은 우선 순위를 가진 기본 우선 순위 그룹이 제공됩니다.

*The following example defines a new custom infix operator called `+-`, which belongs to the precedence group `AdditionPrecedence`:*

다음 예는 우선 순위 그룹 `AdditionPrecedence`에 속하는 `+-`라는 새로운 커스텀 중위 연산자를 정의합니다.

```swift
infix operator +-: AdditionPrecedence
extension Vector2D {
    static func +- (left: Vector2D, right: Vector2D) -> Vector2D {
        return Vector2D(x: left.x + right.x, y: left.y - right.y)
    }
}
let firstVector = Vector2D(x: 1.0, y: 2.0)
let secondVector = Vector2D(x: 3.0, y: 4.0)
let plusMinusVector = firstVector +- secondVector
// plusMinusVector is a Vector2D instance with values of (4.0, -2.0)
```

*This operator adds together the `x` values of two vectors, and subtracts the `y` value of the second vector from the first. Because it’s in essence an “additive” operator, it has been given the same precedence group as additive infix operators such as `+` and `-`. For information about the operators provided by the Swift standard library, including a complete list of the operator precedence groups and associativity settings, see [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations). For more information about precedence groups and to see the syntax for defining your own operators and precedence groups, see [Operator Declaration](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations#Operator-Declaration).*

이 연산자는 두 벡터의 `x` 값을 더하고 첫 번째 벡터에서 두 번째 벡터의 `y` 값을 뺍니다. 본질적으로 "더하기" 연산자이기 때문에 `+` 및 `-`와 같은 추가 중위 연산자와 동일한 우선 순위 그룹이 지정되었습니다. 연산자 우선 순위 그룹 및 연관성 설정의 전체 목록을 포함하여 Swift 표준 라이브러리에서 제공하는 연산자에 대한 자세한 내용은 [링크]를 참조하세요. 우선 순위 그룹에 대한 자세한 내용과 고유한 연산자 및 우선 순위 그룹을 정의하는 구문을 보려면 [링크]를 참조하세요.

> *Note*
> 
> *You don’t specify a precedence when defining a prefix or postfix operator. However, if you apply both a prefix and a postfix operator to the same operand, the postfix operator is applied first.*
> 
> 접두사 또는 접미사 연산자를 정의할 때 우선 순위를 지정하지 않습니다. 단, 동일한 피연산자에 접두사 연산자와 후미사 연산자를 모두 적용하면 후위 연산자가 먼저 적용됩니다.
