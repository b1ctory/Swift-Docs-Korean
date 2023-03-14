## *Overflow Operators : 오버플로 연산자*

*If you try to insert a number into an integer constant or variable that can’t hold that value, by default Swift reports an error rather than allowing an invalid value to be created. This behavior gives extra safety when you work with numbers that are too large or too small.*

해당 값을 보유할 수 없는 정수 상수 또는 변수에 숫자를 삽입하려고 하면 Swift는 기본적으로 잘못된 값이 생성되도록 허용하지 않고 오류를 보고합니다. 이 동작은 너무 크거나 작은 숫자로 작업할 때 추가 안전성을 제공합니다.

*For example, the `Int16` integer type can hold any signed integer between `-32768` and `32767`. Trying to set an `Int16` constant or variable to a number outside of this range causes an error:*

예를 들어 `Int16` 정수 타입은 `-32768`과 `32767` 사이의 모든 부호 있는 정수를 포함할 수 있습니다. `Int16` 상수 또는 변수를 이 범위 밖의 숫자로 설정하려고 하면 오류가 발생합니다.

```swift
var potentialOverflow = Int16.max
// potentialOverflow equals 32767, which is the maximum value an Int16 can hold
potentialOverflow += 1
// this causes an error
```

*Providing error handling when values get too large or too small gives you much more flexibility when coding for boundary value conditions.*

값이 너무 크거나 작을 때 오류 처리를 제공하면 경계 값 조건을 코딩할 때 훨씬 더 많은 유연성을 얻을 수 있습니다.

*However, when you specifically want an overflow condition to truncate the number of available bits, you can opt in to this behavior rather than triggering an error. Swift provides three arithmetic overflow operators that opt in to the overflow behavior for integer calculations. These operators all begin with an ampersand (`&`):*

그러나 사용 가능한 비트 수를 자르기 위해 특별히 오버플로 조건을 원하는 경우 오류를 트리거하지 않고 이 동작을 선택할 수 있습니다. Swift는 정수 계산을 위한 오버플로 동작을 선택하는 세 가지 산술 오버플로 연산자를 제공합니다. 이러한 연산자는 모두 앰퍼샌드(`&`)로 시작합니다.

- *Overflow addition (`&+`)* : 오버플로 더하기(`&+`)

- *Overflow subtraction (`&-`)* : 오버플로 빼기(`&-`)

- _Overflow multiplication (`&*`)_ : 오버플로 곱셈(`&*`)

### *Value Overflow : 값 오버플로*

*Numbers can overflow in both the positive and negative direction.*

숫자는 양의 방향과 음의 방향 모두에서 오버플로 될 수 있습니다.

*Here’s an example of what happens when an unsigned integer is allowed to overflow in the positive direction, using the overflow addition operator (`&+`):*

다음은 오버플로 더하기 연산자(`&+`)를 사용하여 부호 없는 정수가 양의 방향으로 오버플로될 때 발생하는 일의 예입니다.

```swift
var unsignedOverflow = UInt8.max
// unsignedOverflow equals 255, which is the maximum value a UInt8 can hold
unsignedOverflow = unsignedOverflow &+ 1
// unsignedOverflow is now equal to 0
```

*The variable `unsignedOverflow` is initialized with the maximum value a `UInt8` can hold (`255`, or `11111111` in binary). It’s then incremented by `1` using the overflow addition operator (`&+`). This pushes its binary representation just over the size that a `UInt8` can hold, causing it to overflow beyond its bounds, as shown in the diagram below. The value that remains within the bounds of the `UInt8` after the overflow addition is `00000000`, or zero.*

`unsignedOverflow` 변수는 `UInt8`이 보유할 수 있는 최대값(`255` 또는 이진법으로 `11111111`)으로 초기화됩니다. 그런 다음 오버플로 더하기 연산자(`&+`)를 사용하여 `1`씩 증가합니다. 이는 아래 다이어그램에 표시된 것처럼 `UInt8`이 보유할 수 있는 크기 이상으로 바이너리 표현을 푸시하여 범위를 넘어 오버플로를 일으킵니다. 오버플로 추가 후 `UInt8` 범위 내에 남아 있는 값은 `00000000` 또는 0입니다.

*![](https://docs.swift.org/swift-book/images/overflowAddition@2x.png)*

*Something similar happens when an unsigned integer is allowed to overflow in the negative direction. Here’s an example using the overflow subtraction operator (`&-`):*

부호 없는 정수가 음의 방향으로 넘칠 때 비슷한 일이 발생합니다. 다음은 오버플로 빼기 연산자(`&-`)를 사용하는 예입니다.

```swift
var unsignedOverflow = UInt8.min
// unsignedOverflow equals 0, which is the minimum value a UInt8 can hold
unsignedOverflow = unsignedOverflow &- 1
// unsignedOverflow is now equal to 255
```

*The minimum value that a `UInt8` can hold is zero, or `00000000` in binary. If you subtract `1` from `00000000` using the overflow subtraction operator (`&-`), the number will overflow and wrap around to `11111111`, or `255` in decimal.*

`UInt8`이 보유할 수 있는 최소값은 0 또는 이진법으로 `00000000`입니다. 오버플로우 빼기 연산자(`&-`)를 사용하여 `00000000`에서 `1`을 빼면 숫자가 오버플로되어 `11111111` 또는 십진수로 `255`가 됩니다.

*![](https://docs.swift.org/swift-book/images/overflowUnsignedSubtraction@2x.png)*

*Overflow also occurs for signed integers. All addition and subtraction for signed integers is performed in bitwise fashion, with the sign bit included as part of the numbers being added or subtracted, as described in [Bitwise Left and Right Shift Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/advancedoperators#Bitwise-Left-and-Right-Shift-Operators).*

부호 있는 정수에서도 오버플로가 발생합니다. 부호 있는 정수에 대한 모든 덧셈과 뺄셈은 [링크]에 설명된 대로 더하거나 뺄 수 있는 숫자의 일부로 포함된 부호 비트와 함께 비트 방식으로 수행됩니다.

```swift
var signedOverflow = Int8.min
// signedOverflow equals -128, which is the minimum value an Int8 can hold
signedOverflow = signedOverflow &- 1
// signedOverflow is now equal to 127
```

*The minimum value that an `Int8` can hold is `-128`, or `10000000` in binary. Subtracting `1` from this binary number with the overflow operator gives a binary value of `01111111`, which toggles the sign bit and gives positive `127`, the maximum positive value that an `Int8` can hold.*

`Int8`이 보유할 수 있는 최소값은 `-128` 또는 이진수로 `10000000`입니다. 오버플로 연산자를 사용하여 이 이진수에서 `1`을 빼면 이진수 값 `01111111`이 됩니다. 이 값은 부호 비트를 전환하고 `Int8`이 가질 수 있는 최대 양수 값인 양수 `127`을 제공합니다.

*![](https://docs.swift.org/swift-book/images/overflowSignedSubtraction@2x.png)*

*For both signed and unsigned integers, overflow in the positive direction wraps around from the maximum valid integer value back to the minimum, and overflow in the negative direction wraps around from the minimum value to the maximum.*

부호 있는 정수와 부호 없는 정수 모두 양의 방향 오버플로는 최대 유효한 정수 값에서 다시 최소값으로 순환하고 음의 방향 오버플로는 최소값에서 최대 값으로 순환합니다.
