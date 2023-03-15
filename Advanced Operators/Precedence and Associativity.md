## *Precedence and Associativity : 우선순위 및 연관성*

*Operator precedence gives some operators higher priority than others; these operators are applied first.*

연산자 우선 순위는 일부 연산자에게 다른 연산자보다 높은 우선 순위를 제공합니다; 이러한 연산자가 먼저 적용됩니다.

*Operator associativity defines how operators of the same precedence are grouped together — either grouped from the left, or grouped from the right. Think of it as meaning “they associate with the expression to their left,” or “they associate with the expression to their right.”*

연산자 연관성은 동일한 우선 순위의 연산자를 왼쪽에서 그룹화하거나 오른쪽에서 그룹화하는 방법을 정의합니다. "그들은 그들의 왼쪽에 있는 표현과 관련이 있다" 또는 "그들은 그들의 오른쪽에 있는 표현과 관련이 있다"는 의미라고 생각하세요.

*It’s important to consider each operator’s precedence and associativity when working out the order in which a compound expression will be calculated. For example, operator precedence explains why the following expression equals `17`.*

복합식이 계산되는 순서를 계산할 때 각 연산자의 우선 순위와 연관성을 고려하는 것이 중요합니다. 예를 들어, 연산자 우선 순위는 다음 식이 `17`과 같은 이유를 설명합니다.

```swift
2 + 3 % 4 * 5
// this equals 17
```

*If you read strictly from left to right, you might expect the expression to be calculated as follows:*

엄격하게 왼쪽에서 오른쪽으로 읽으면 표현식이 다음과 같이 계산될 것으로 예상할 수 있습니다.

- *`2` plus `3` equals `5`*
  
  `2` 더하기 `3`은 `5`입니다.

- *`5` remainder `4` equals `1`*
  
  `5` 나머지 `4`는 `1`입니다.

- *`1` times `5` equals `5`*
  
  `1` 곱하기 `5`는 `5`입니다.

_However, the actual answer is `17`, not `5`. Higher-precedence operators are evaluated before lower-precedence ones. In Swift, as in C, the remainder operator (`%`) and the multiplication operator (`*`) have a higher precedence than the addition operator (`+`). As a result, they’re both evaluated before the addition is considered._

하지만 실제 답은 `5`가 아닌 `17`입니다. 우선 순위가 높은 연산자는 우선 순위가 낮은 연산자보다 먼저 평가됩니다. Swift에서는 C와 마찬가지로 나머지 연산자(`%`)와 곱셈 연산자(`*`)가 더하기 연산자(`+`)보다 우선 순위가 높습니다. 결과적으로 덧셈이 고려되기 전에 둘 다 평가됩니다.

*However, remainder and multiplication have the same precedence as each other. To work out the exact evaluation order to use, you also need to consider their associativity. Remainder and multiplication both associate with the expression to their left. Think of this as adding implicit parentheses around these parts of the expression, starting from their left:*

단, 나머지와 곱셈은 서로 같은 우선순위를 갖습니다. 사용할 정확한 평가 순서를 계산하려면 연관성도 고려해야 합니다. 나머지와 곱셈은 모두 왼쪽에 있는 식과 연결됩니다. 왼쪽부터 시작하여 표현식의 이러한 부분 주위에 암시적 괄호를 추가하는 것으로 생각하세요.

```swift
2 + ((3 % 4) * 5)
```

*`(3 % 4)` is `3`, so this is equivalent to:*

`(3 % 4)` 는`3`이고, 이것은 다음과 동등합니다:

```swift
2 + (3 * 5)
```

*`(3 * 5)` is `15`, so this is equivalent to:*

`(3 * 5)` 는 `15`이고, 이것은 다음과 동등합니다:

```swift
2 + 15
```

*This calculation yields the final answer of `17`.*

이 계산을 통해 `17`의 최종 답을 얻을 수 있습니다.

*For information about the operators provided by the Swift standard library, including a complete list of the operator precedence groups and associativity settings, see [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations).*

연산자 우선순위 그룹 및 연관성 설정의 전체 목록을 포함하여 Swift 표준 라이브러리에서 제공하는 연산자에 대한 정보는 [링크]를 참조하세요.

*Swift’s operator precedences and associativity rules are simpler and more predictable than those found in C and Objective-C. However, this means that they aren’t exactly the same as in C-based languages. Be careful to ensure that operator interactions still behave in the way you intend when porting existing code to Swift.*

Swift의 연산자 우선 순위 및 연관성 규칙은 C 및 Objective-C에 있는 것보다 더 단순하고 예측 가능합니다. 하지만, 이것은 그들이 C 기반 언어와 정확히 같지 않다는 것을 의미합니다. 기존 코드를 Swift로 포팅할 때 연산자 상호 작용이 원하는 방식으로 작동하는지 확인하세요.

> *Note*
> 
> *Swift’s operator precedences and associativity rules are simpler and more predictable than those found in C and Objective-C. However, this means that they aren’t exactly the same as in C-based languages. Be careful to ensure that operator interactions still behave in the way you intend when porting existing code to Swift.*
> 
> Swift의 연산자 우선 순위 및 연관성 규칙은 C 및 Objective-C에 있는 것보다 더 단순하고 예측 가능합니다. 하지만, 이것은 그들이 C 기반 언어와 정확히 같지 않다는 것을 의미합니다. 기존 코드를 Swift로 포팅할 때 연산자 상호 작용이 여전히 의도한 방식으로 작동하도록 주의하십시오.


