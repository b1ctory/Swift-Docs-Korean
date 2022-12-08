## *Arithmetic Operators : 산술연산자*

*Swift supports the four standard arithmetic operators for all number types:*

Swift는 모든 숫자 유형에 대해 네가지 표준 산술 연산자를 지원합니다.

- *Addition (`+`)* : 더하기

- *Subtraction (`-`)* : 빼기

- *Multiplication* (`*`): 곱하기

- *Division (`/`)* : 나누기

```swift
1 + 2       // equals 3
5 - 3       // equals 2
2 * 3       // equals 6
10.0 / 2.5  // equals 4.0
```

*Unlike the arithmetic operators in C and Objective-C, the Swift arithmetic operators don’t allow values to overflow by default. You can opt in to value overflow behavior by using Swift’s overflow operators (such as `a &+ b`). See [Overflow Operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID37).*

C 및 Objective-C 산술 연산자와 달리 Swift 의 산술 연산자는 기본적으로 값의 오버플로우를 허용하지 않습니다. 스위프트의 오버플로우 연산자 (예 : `a &+ b`) 를 사용하여 오버플로우 동작을 값으로 지정할 수 있습니다. [링크]를 보세요.

*The addition operator is also supported for `String` concatenation:*

더하기 연산자는 또한 String 결합을 지원합니다.

```swift
"hello, " + "world"  // equals "hello, world"
```



### *Remainder Operator : 나머지 연산자*

*The remainder operator (`a % b`) works out how many multiples of `b` will fit inside `a` and returns the value that’s left over (known as the remainder).*

나머지 연산자 (`a % b`) 는 `b`의 배수가 `a` 안에 얼마나 들어가는지 계산하고 남은 값을 (나머지 라고 알려진) 리턴합니다. 

> *NOTE*
> 
> *The remainder operator (`%`) is also known as a modulo operator in other languages. However, its behavior in Swift for negative numbers means that, strictly speaking, it’s a remainder rather than a modulo operation.*
> 
> 나머지 연산자 (`%`) 는 다른 언어에서는 *모듈로 연산자* 로도 알려져있습니다. 그러나 Swift에서 음수에 대한 동작은 엄밀히 말하면 *모듈로 연산*이 아닌 나머지 연산을 의미합니다. 

*Here’s how the remainder operator works. To calculate `9 % 4`, you first work out how many `4`s will fit inside `9`:*

다음은 나머지 연산자의 작동 방식입니다. `9 % 4` 를 계산하기 위해서 먼저 9 안에 4가 얼마나 들어갈지 계산해야 합니다.

![](https://docs.swift.org/swift-book/_images/remainderInteger_2x.png)

*You can fit two `4`s inside `9`, and the remainder is `1` (shown in orange).*

`9` 안에 `4` 두개를 넣을 수 있고 나머지는 `1`입니다. 

*In Swift, this would be written as:*

Swift 에서는 다음과 같이 쓰입니다.

```swift
9 % 4 // equals 1
```

*To determine the answer for `a % b`, the `%` operator calculates the following equation and returns `remainder` as its output:*

`a % b`에 대한 답을 결정하기 위해 `%` 연산자는 다음 방정식을 계산하고 결과물로 `나머지`를 반환합니다.

> `a` = (`b` x `some multiplier`) + `remainder`

*where `some multiplier` is the largest number of multiples of `b` that will fit inside `a`.* *Inserting `9` and `4` into this equation yields:*

여기서 `일부 승수`는 `a` 안에 들어갈 `b`의 최대 배수입니다. 이 방정식에 `9`와 `4`를 넣으면 다음과 같습니다.

> `9` = (`4` x `2`) + `1`

*The same method is applied when calculating the remainder for a negative value of `a`:*

`a`의 음수 값에 대한 나머지를 계산할 때도 동일한 방법이 적용됩니다.

```swift
-9 % 4 // equals -1
```

*Inserting `-9` and `4` into the equation yields:*

`-9`와 `4`를 방정식에 넣으면 다음과 같습니다. 

> `-9` = (`4` x `-2`) + `-1`

*giving a remainder value of `-1`.*

`-1`의 나머지 값을 제공합니다. 



*The sign of `b` is ignored for negative values of `b`. This means that `a % b` and `a % -b` always give the same answer.*

`b`의 음수 값에 대해서는 `b`의 부호가 무시됩니다. 이것은 `a % b`와 `a % -b`가 항상 같은 대답을 한다는 것을 의미합니다. 



> 직접 실행해본 예시코드

```swift
print(-9 % 4)
print(9 % 4)

print(9 % 4)
print(9 % -4)


/*
 출력 결과

-1
1
1
1

*/
```



### *Unary Minus Operator : 단항 빼기 연산자*

*The sign of a numeric value can be toggled using a prefixed `-`, known as the unary minus operator:*

숫자 값의 부호는 단항 빼기 연산자로 알려진 접두사 `-`를 사용해서 전환할 수 있습니다. 

```swift
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three"
```

*The unary minus operator (`-`) is prepended directly before the value it operates on, without any white space.*

단항 빼기 연산자 (`-`)는 공백 없이 연산값 바로 앞에 붙습니다. 



### *Unary Plus Operator : 단항 더하기 연산자*

*The unary plus operator (`+`) simply returns the value it operates on, without any change:*

단항 더하기 연산자 (`+`)는 변경 없이 단순히 연산값을 반환합니다.

```swift
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
```

*Although the unary plus operator doesn’t actually do anything, you can use it to provide symmetry in your code for positive numbers when also using the unary minus operator for negative numbers.*

비록 단항 덧셈 연산자는 실제로 아무것도 하지 않지만, 음수에 대해 단항 빼기 연산자를 사용할 때 양의 숫자에 대한 대칭을 제공하는데 사용할 수 있습니다.


