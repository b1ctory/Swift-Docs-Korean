## *Logical Operators : 논리연산자*

*Logical operators modify or combine the Boolean logic values `true` and `false`. Swift supports the three standard logical operators found in C-based languages:*

논리 연산자는 Boolean 논리 값 `true`와 `false`를 수정하거나 결합합니다. 스위프트는 C 기반 언어에서 발견되는 세가지 표준 논리 연산자를 지원합니다. 

- *Logical NOT (`!a`)* 

- *Logical AND (`a && b`)*

- *Logical OR (`a || b`)*

### *Logical NOT Operator : 논리 NOT 연산자*

*The logical NOT operator (`!a`) inverts a Boolean value so that `true` becomes `false`, and `false` becomes `true`.*

논리 NOT 연산자 (`!a`)는 Boolean 값을 반전시켜 `true`는 `false`가 되고, `false`는 `true`가 됩니다. 

*The logical NOT operator is a prefix operator, and appears immediately before the value it operates on, without any white space. It can be read as “not `a`”, as seen in the following example:*

논리 NOT 연산자는 접두사 연산자이며, 이 연산자가 작동하는 값 바로 앞에 공백 없이 나타납니다. 다음 예시에서 볼 수 있듯이 "`a`가 아닌" 으로 읽을 수 있습니다. 

```swift
let allowedEntry = false
if !allowedEntry {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```

*The phrase `if !allowedEntry` can be read as “if not allowed entry.” The subsequent line is only executed if “not allowed entry” is true; that is, if `allowedEntry` is `false`.*

`if !allowedEntry`라는 문구는 "만약 허용되지 않는 경우"로 읽을 수 있습니다. 후속 행은 `not allowed entry`가 참일 때만 실행됩니다; 즉, `allowedEntry` 가 `false`일 경우에만 실행됩니다.

*As in this example, careful choice of Boolean constant and variable names can help to keep code readable and concise, while avoiding double negatives or confusing logic statements.*

예시에서와 같이, Boolean 상수와 변수 이름을 신중하게 선택하면 코드를 읽기 쉽고 간결하게 유지하는 동시에 이중 부정 혹은 논리 문을 혼동하지 않도록 할 수 있습니다. 

### *Logical AND Operator : 논리 AND 연산자*

*The logical AND operator (`a && b`) creates logical expressions where both values must be `true` for the overall expression to also be `true`.*

논리 AND 연산자 (`a && b`)는 전체 표현식이 `true`가 되려면 두 값이 모두 `true`여야하는 논리 표현식을 생성합니다.

*If either value is `false`, the overall expression will also be `false`. In fact, if the first value is `false`, the second value won’t even be evaluated, because it can’t possibly make the overall expression equate to `true`. This is known as short-circuit evaluation.*

두 값이 모두 `false`이면, 전체 표현식도 `false`가 됩니다. 사실, 첫번째 값이 false이면 두번째 값은 전체 표현식을 true와 동일시할 수 없기 때문에 평가되지 않습니다. 이는 단락평가라고 합니다.

*This example considers two `Bool` values and only allows access if both values are `true`:*

이 예에서는 두 개의 `Bool`값을 고려하며 두 값이 모두 `true`인 경우에만 액세스를 허용합니다.

```swift
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```

### *Logical OR Operator : 논리 OR 연산자*

*The logical OR operator (`a || b`) is an infix operator made from two adjacent pipe characters. You use it to create logical expressions in which only one of the two values has to be `true` for the overall expression to be `true`.*

논리 OR 연산자 (`a || b`)는 두 개의 인접한 파이프 문자로 만들어진 접두 연산자입니다. 전체 표현식이 참아 되려면 두 값 중 하나만 참이어야 하는 논리 표현식을 만들 때 사용합니다.  

*Like the Logical AND operator above, the Logical OR operator uses short-circuit evaluation to consider its expressions. If the left side of a Logical OR expression is `true`, the right side isn’t evaluated, because it can’t change the outcome of the overall expression.*

위의 논리적 AND 연산과 마찬가지로 논리적 OR 연산자는 표현식을 고려하기 위해 단락 평가를 사용합니다. 논리 OR 표현식의 왼쪽이 `true`이면 전체 표현식의 결과를 변경할 수 없기 때문에 오른쪽이 평가되지 않습니다. 

*In the example below, the first `Bool` value (`hasDoorKey`) is `false`, but the second value (`knowsOverridePassword`) is `true`. Because one value is `true`, the overall expression also evaluates to `true`, and access is allowed:*

아래 예제에서 첫번째 Bool 값 (`hasDoorKey`)은 false이지만 두번째 값 (`knowsOverridePassword`) 은 `true` 입니다. 하나의 값이 `true`이기 때문에 전체 표현식도  `true`로 평가되며 다음과 같이 엑세스가 허용됩니다. 

```swift
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

### *Combining Logical Operators : 논리 연산자 결합*

*You can combine multiple logical operators to create longer compound expressions:*

여러 논리 연산자를 결합해서 더 길고 복잡한 표현식을 만들 수 있습니다. 

```swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

*This example uses multiple `&&` and `||` operators to create a longer compound expression. However, the `&&` and `||` operators still operate on only two values, so this is actually three smaller expressions chained together. The example can be read as:*

이 예시에서는 다중 `&&` 및 `||` 연산자를 사용하여 더 길고 복잡한 표현식을 만듭니다. 그러나, `&&`과 `||`연산자는 여전히 두개의 값으로만 작동하기 때문에 이는 실제로 세 개의 작은 표현식이 묶여있는 것입니다. 이 예는 이렇게 읽을 수 있습니다.

*If we’ve entered the correct door code and passed the retina scan, or if we have a valid door key, or if we know the emergency override password, then allow access.*

만약 올바른 도어 코드를 입력하고 망막 스캔을 통과했거나 유효한 도어 키가 있거나 비상 재지정 암호를 알고있으면 엑세스를 허용하세요.

*Based on the values of `enteredDoorCode`, `passedRetinaScan`, and `hasDoorKey`, the first two subexpressions are `false`. However, the emergency override password is known, so the overall compound expression still evaluates to `true`.*

`enteredDoorCode`, `passedRetinaScan`, 그리고 `hasDoorKey`값을 기준으로 할 때 처음 두 개의 하위표현은 `false`입니다. 그러나 비상 덮어쓰기 암호는 알려져 있기 때문에 전체 복합 표현식은 여전히 `true`로 평가됩니다.

> *NOTE*
> 
> *The Swift logical operators `&&` and `||` are left-associative, meaning that compound expressions with multiple logical operators evaluate the leftmost subexpression first.*
> 
> 스위프트의 논리 연산자 &&과 ||는 왼쪽-연관성이 있는데, 이는 여러 논리 연산자를 가진 복합 표현식이 가장 왼쪽의 하위 표현식을 먼저 평가한다는 것을 의미합니다. 

### *Explicit Parentheses : 명시적 괄호*

*It’s sometimes useful to include parentheses when they’re not strictly needed, to make the intention of a complex expression easier to read. In the door access example above, it’s useful to add parentheses around the first part of the compound expression to make its intent explicit:*

복잡한 표현의 의도를 읽기 쉽게 하기 위해 괄호가 꼭 필요하지 않을 때에도 괄호를 포함하는 것이 유용할 때가 있습니다. 위의 도어 엑세스 예제에서 복합 표현식의 첫번째 부분 주위에 괄호를 추가하여 의도를 명시하는 것이 유용합니다.

```swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
// Prints "Welcome!"
```

*The parentheses make it clear that the first two values are considered as part of a separate possible state in the overall logic. The output of the compound expression doesn’t change, but the overall intention is clearer to the reader. Readability is always preferred over brevity; use parentheses where they help to make your intentions clear.*

괄호는 처음 두 값이 전체 논리에서 개별로 가능한 상태의 일부로 간주된다는 것을 명확하게 합니다. 복합식의 출력은 변하지 않지만, 전체적인 의도는 읽는 사람에게 더 명확합니다. 
