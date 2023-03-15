## *Operator Methods : 연산자 메서드*

*Classes and structures can provide their own implementations of existing operators. This is known as overloading the existing operators.*

클래스 및 구조체는 기존 연산자의 자체 구현을 제공할 수 있습니다. 이를 기존 연산자 오버로딩 이라고 합니다.

*The example below shows how to implement the arithmetic addition operator (`+`) for a custom structure. The arithmetic addition operator is a binary operator because it operates on two targets and it’s an infix operator because it appears between those two targets.*

아래 예제는 사용자 정의 구조에 대한 산술 덧셈 연산자(`+`)를 구현하는 방법을 보여줍니다. 산술 덧셈 연산자는 두 개의 대상에서 작동하기 때문에 이진 연산자이고 두 대상 사이에 나타나므로 infix 연산자입니다.

*The example defines a `Vector2D` structure for a two-dimensional position vector `(x, y)`, followed by a definition of an operator method to add together instances of the `Vector2D` structure:*

이 예는 2차원 위치 벡터 `(x, y)`에 대한 `Vector2D` 구조를 정의한 다음 `Vector2D` 구조의 인스턴스를 함께 추가하는 연산자 메서드의 정의가 뒤따릅니다.

```swift
struct Vector2D {
    var x = 0.0, y = 0.0
}

extension Vector2D {
    static func + (left: Vector2D, right: Vector2D) -> Vector2D {
       return Vector2D(x: left.x + right.x, y: left.y + right.y)
    }
}
```

 *`Vector2D` instances that are added together.*

함께 추가되는 `Vector2D` 인스턴스.

*The type method can be used as an infix operator between existing `Vector2D` instances:*

타입 메서드는 기존 `Vector2D` 인스턴스 사이에서 중위 연산자로 사용할 수 있습니다.

```swift
let vector = Vector2D(x: 3.0, y: 1.0)
let anotherVector = Vector2D(x: 2.0, y: 4.0)
let combinedVector = vector + anotherVector
// combinedVector is a Vector2D instance with values of (5.0, 5.0)
```

*This example adds together the vectors `(3.0, 1.0)` and `(2.0, 4.0)` to make the vector `(5.0, 5.0)`, as illustrated below.*

이 예는 벡터 `(3.0, 1.0)`과 `(2.0, 4.0)`을 함께 추가하여 아래 그림과 같이 벡터 `(5.0, 5.0)`을 만듭니다.

*![](https://docs.swift.org/swift-book/images/vectorAddition@2x.png)*

### *Prefix and Postfix Operators : 접두사 및 접미사 연산자*

*The example shown above demonstrates a custom implementation of a binary infix operator. Classes and structures can also provide implementations of the standard unary operators. Unary operators operate on a single target. They’re prefix if they precede their target (such as `-a`) and postfix operators if they follow their target (such as `b!`).*

위에 표시된 예는 이진 중위 연산자의 사용자 정의 구현을 보여줍니다. 클래스 및 구조는 표준 단항 연산자의 구현도 제공할 수 있습니다. 단항 연산자는 단일 대상에서 작동합니다. 대상 앞에 있는 경우 접두사(예: `-a`)이고 대상 뒤에 있는 경우 접미사 연산자입니다(예: `b!`)

*You implement a prefix or postfix unary operator by writing the `prefix` or `postfix` modifier before the `func` keyword when declaring the operator method:*

연산자 메소드를 선언할 때 `func` 키워드 앞에 `prefix` 또는 `postfix` 한정자를 작성하여 접두사 또는 접미사 단항 연산자를 구현합니다.

```swift
extension Vector2D {
    static prefix func - (vector: Vector2D) -> Vector2D {
        return Vector2D(x: -vector.x, y: -vector.y)
    }
}
```

*The example above implements the unary minus operator (`-a`) for `Vector2D` instances. The unary minus operator is a prefix operator, and so this method has to be qualified with the `prefix` modifier.*

위의 예는 `Vector2D` 인스턴스에 대한 단항 빼기 연산자(`-a`)를 구현합니다. 단항 빼기 연산자는 접두사 연산자이므로 이 메서드는 `prefix` 수정자로 한정되어야 합니다.

*For simple numeric values, the unary minus operator converts positive numbers into their negative equivalent and vice versa. The corresponding implementation for `Vector2D` instances performs this operation on both the `x` and `y` properties:*

단순 숫자 값의 경우 단항 빼기 연산자는 양수를 음수로 변환하거나 그 반대로 변환합니다. `Vector2D` 인스턴스에 대한 해당 구현은 `x` 및 `y` 프로퍼티 모두에서 이 작업을 수행합니다.

```swift
let positive = Vector2D(x: 3.0, y: 4.0)
let negative = -positive
// negative is a Vector2D instance with values of (-3.0, -4.0)
let alsoPositive = -negative
// alsoPositive is a Vector2D instance with values of (3.0, 4.0)
```

### *Compound Assignment Operators : 복합 할당 연산자*

*Compound assignment operators combine assignment (`=`) with another operation. For example, the addition assignment operator (`+=`) combines addition and assignment into a single operation. You mark a compound assignment operator’s left input parameter type as `inout`, because the parameter’s value will be modified directly from within the operator method.*

복합 할당 연산자는 대입(`=`)을 다른 연산과 결합합니다. 예를 들어 더하기 할당 연산자(`+=`)는 더하기와 할당을 단일 연산으로 결합합니다. 복합 대입 연산자의 왼쪽 입력 매개변수 유형을 `inout`으로 표시합니다. 매개변수의 값이 연산자 메소드 내에서 직접 수정되기 때문입니다.

*The example below implements an addition assignment operator method for `Vector2D` instances:*

아래 예시는 `Vector2D` 인스턴스에 대한 추가 할당 연산자 메서드를 구현합니다.

```swift
extension Vector2D {
    static func += (left: inout Vector2D, right: Vector2D) {
        left = left + right
    }
}
```

*Because an addition operator was defined earlier, you don’t need to reimplement the addition process here. Instead, the addition assignment operator method takes advantage of the existing addition operator method, and uses it to set the left value to be the left value plus the right value:*

더하기 연산자는 이전에 정의했기 때문에 여기에서 덧셈 프로세스를 다시 구현할 필요가 없습니다. 대신 덧셈 할당 연산자 방식은 기존 덧셈 연산자 방식을 활용하여 왼쪽 값을 왼쪽 값 더하기 오른쪽 값으로 설정하는 데 사용합니다.

```swift
var original = Vector2D(x: 1.0, y: 2.0)
let vectorToAdd = Vector2D(x: 3.0, y: 4.0)
original += vectorToAdd
// original now has values of (4.0, 6.0)
```

> *Note*
> 
> *It isn’t possible to overload the default assignment operator (`=`). Only the compound assignment operators can be overloaded. Similarly, the ternary conditional operator (`a ? b : c`) can’t be overloaded.*
> 
> 기본 할당 연산자(`=`)는 오버로딩할 수 없습니다. 복합 대입 연산자만 오버로드할 수 있습니다. 마찬가지로 삼항 조건 연산자(`a ? b : c`)는 오버로드할 수 없습니다.

### *Equivalence Operators : 등가 연산자*

*By default, custom classes and structures don’t have an implementation of the equivalence operators, known as the equal to operator (`==`) and not equal to operator (`!=`). You usually implement the `==` operator, and use the standard library’s default implementation of the `!=` operator that negates the result of the `==` operator. There are two ways to implement the `==` operator: You can implement it yourself, or for many types, you can ask Swift to synthesize an implementation for you. In both cases, you add conformance to the standard library’s `Equatable` protocol.*

*You provide an implementation of the `==` operator in the same way as you implement other infix operators:*

기본적으로 커스텀 클래스 및 구조체에는 같음 연산자(`==`) 및 같지 않음 연산자(`!=`)로 알려진 등가 연산자 구현이 없습니다. 일반적으로 `==` 연산자를 구현하고 `==` 연산자의 결과를 부정하는 표준 라이브러리의 기본 구현인 `!=` 연산자를 사용합니다. `==` 연산자를 구현하는 방법에는 두 가지가 있습니다. 직접 구현하거나 여러 타입의 경우 Swift에 구현 합성을 요청할 수 있습니다. 두 경우 모두 표준 라이브러리의 `Equatable` 프로토콜에 적합성을 추가합니다.

```swift
extension Vector2Dextension Vector2D: Equatable {
    static func == (left: Vector2D, right: Vector2D) -> Bool {
       return (left.x == right.x) && (left.y == right.y)
    }
}: Equatable {    static func == (left: Vector2D, right: Vector2D) -> Bool {       return (left.x == right.x) && (left.y == right.y)    }}
```

*The example above implements an `==` operator to check whether two `Vector2D` instances have equivalent values. In the context of `Vector2D`, it makes sense to consider “equal” as meaning “both instances have the same `x` values and `y` values”, and so this is the logic used by the operator implementation.*

위의 예는 두 개의 `Vector2D` 인스턴스가 동일한 값을 가지고 있는지 확인하기 위해 `==` 연산자를 구현합니다. `Vector2D`의 맥락에서 "같음"은 "두 인스턴스가 동일한 `x` 값과 `y` 값을 가짐"을 의미하는 것으로 간주하는 것이 합리적이며 이것이 연산자 구현에서 사용되는 논리입니다.

*You can now use this operator to check whether two `Vector2D` instances are equivalent:*

이제 이 연산자를 사용하여 두 개의 `Vector2D` 인스턴스가 동일한지 확인할 수 있습니다.

```swift
let twoThree = Vector2D(x: 2.0, y: 3.0)
let anotherTwoThree = Vector2D(x: 2.0, y: 3.0)
if twoThree == anotherTwoThree {
    print("These two vectors are equivalent.")
}
// Prints "These two vectors are equivalent."
```

*In many simple cases, you can ask Swift to provide synthesized implementations of the equivalence operators for you, as described in [Adopting a Protocol Using a Synthesized Implementation](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/protocols#Adopting-a-Protocol-Using-a-Synthesized-Implementation).*

많은 간단한 경우에 [링크]에 설명된 대로 Swift에 등가 연산자의 합성된 구현을 제공하도록 요청할 수 있습니다.
