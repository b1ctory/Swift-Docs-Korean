## *Numeric Literals : 숫자 리터럴*

*Integer literals can be written as:*

- *A decimal number, with no prefix*

- *A binary number, with a `0b` prefix*

- *An octal number, with a `0o` prefix*

- *A hexadecimal number, with a `0x` prefix*

*All of these integer literals have a decimal value of `17`:*

정수 리터럴은 이렇게 쓰일 수 있습니다 : 

- 접두사가 없는 10진수

- 0b 접두사를 사용하는 2진수

- 0o 접두사를 사용하는 8진수

- 0x 접두사를 사용하는 16진수

이 모든 정수 리터럴은 10진수 값이 17입니다.

```swift
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
```

*Floating-point literals can be decimal (with no prefix), or hexadecimal (with a `0x` prefix). They must always have a number (or hexadecimal number) on both sides of the decimal point. Decimal floats can also have an optional exponent, indicated by an uppercase or lowercase `e`; hexadecimal floats must have an exponent, indicated by an uppercase or lowercase `p`.*

부동소수점 리터럴은 10진수 (접두사 없음) 혹은 16진수 (0x 접두사 있음) 일 수 있습니다.소수점 양 쪽에 항상 숫자 (혹은 16진수)가 있어야 합니다. 10진수 Float은 대문자 혹은 소문자 e로 표시되는 선택적 지수를 가질 수 있으며, 16진수 Float은 대문자 혹은 소문자 p로 표시되는 지수를 가져야합니다.

*For decimal numbers with an exponent of `exp`, the base number is multiplied by 10exp:*

지수가 exp인 10진수인 경우, 기본 숫자에 10exp를 곱합니다.

- *`1.25e2` means 1.25 x 102, or `125.0`.*
  
  - 1.25e2 는 1.25 x 102 혹은 125.0을 의미합니다.

- *`1.25e-2` means 1.25 x 10-2, or `0.0125`.*
  
  - 1.25e-2 는 1.25 x 10-2 혹은 0.0125를 의미합니다.

*For hexadecimal numbers with an exponent of `exp`, the base number is multiplied by 2exp:*

지수가 exp인 16진수의 경우, 기본 숫자에 2exp를 곱하면 다음과 같습니다.

- *`0xFp2` means 15 x 22, or `60.0`.*
  
  - 0xFp2는 15 x 22 혹은 60.0을 의미합니다.

- *`0xFp-2` means 15 x 2-2, or `3.75`.*
  
  - 0xFp-2는 15 x 2-2 혹은 3.75를 의미합니다.

*All of these floating-point literals have a decimal value of `12.1875`:*

이 모든 부동소수점 리터럴은 십진수 값으로 12.1875를 가집니다.

```swift
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

*Numeric literals can contain extra formatting to make them easier to read. Both integers and floats can be padded with extra zeros and can contain underscores to help with readability. Neither type of formatting affects the underlying value of the literal:*

숫자 리터럴은 읽기 쉽도록 추가 형식을 포함할 수 있습니다. 정수와 Float는 모두 추가 0으로 패딩될 수 있으며 가독성을 높이기 위해 밑줄이 포함될 수 있습니다. 두 형식 모두 리터럴의 기본 값에 영향을 주지 않습니다.

```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```
