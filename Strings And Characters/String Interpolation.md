## *String Interpolation : 문자열 보간법*

*String interpolation is a way to construct a new `String` value from a mix of constants, variables, literals, and expressions by including their values inside a string literal. You can use string interpolation in both single-line and multiline string literals. Each item that you insert into the string literal is wrapped in a pair of parentheses, prefixed by a backslash (`\`):*

문자열 보간법은 상수, 변수, 리터럴, 표현식의 조합에서 문자열 값을 문자열 리터럴 안에 포함시켜 새로운 문자열 값을 구성하는 방법이다. 문자열 보간은 한 줄 및 여러 줄 문자열 리터럴 모두에서 사용할 수 있습니다. 문자열 리터럴에 삽입하는 각 항목은 한 쌍의 괄호로 묶이고 뒤에 백슬래쉬(`\`)를 붙입니다.

```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5"
```

*In the example above, the value of `multiplier` is inserted into a string literal as `\(multiplier)`. This placeholder is replaced with the actual value of `multiplier` when the string interpolation is evaluated to create an actual string.*

위의 예에서 `multiplier`의 값은 문자열 리터럴에 `'\(multiplier)'`로 삽입됩니다. 문자열 보간을 평가하여 실제 문자열을 생성할 때 이 자리표시자는 실제 값인 `multiplier`로 대체됩니다.

*The value of `multiplier` is also part of a larger expression later in the string. This expression calculates the value of `Double(multiplier) * 2.5` and inserts the result (`7.5`) into the string. In this case, the expression is written as `\(Double(multiplier) * 2.5)` when it’s included inside the string literal.*

`multiplier`의 값도 문자열 뒷부분에 있는 더 큰 표현식의 일부입니다. 이 표현식은 `Double(multiplier) * 2.5` 의 값을 계산하고 결과 (`7.5`)를 문자열에 삽입합니다. 이 경우 문자열 리터럴 안에 포함되면 `\(Double(multiplier) * 2.5)`로 표현됩니다.

*You can use extended string delimiters to create strings containing characters that would otherwise be treated as a string interpolation. For example:*

확장 문자열 구분 기호를 사용해서 문자열 보간으로 처리되는 문자가 포함된 문자열을 만들 수 있습니다. 예를 들어 :

```swift
print(#"Write an interpolated string in Swift using \(multiplier)."#)
// Prints "Write an interpolated string in Swift using \(multiplier)."
```

*To use string interpolation inside a string that uses extended delimiters, match the number of number signs after the backslash to the number of number signs at the beginning and end of the string. For example:*

확장 구분 기호를 사용하는 문자열 내에서 문자열 보간을 사용하려면 백슬래쉬 이후의 숫자 기호 수를 문자열의 시작과 끝에 있는 숫자 기호 수와 일치시킵니다. 예를 들어 :

```swift
print(#"6 times 7 is \#(6 * 7)."#)
// Prints "6 times 7 is 42."
```

> *NOTE*
> 
> *The expressions you write inside parentheses within an interpolated string can’t contain an unescaped backslash (`\`), a carriage return, or a line feed. However, they can contain other string literals.*
> 
> 보간 문자열 내 괄호 안에 쓰는 식은 탈출되지않은 백슬래쉬 (`\`), 캐리지 리턴 혹은 라인 피드를 포함할 수 없습니다. 그러나 다른 문자열 리터럴을 포함할 수 있습니다.
