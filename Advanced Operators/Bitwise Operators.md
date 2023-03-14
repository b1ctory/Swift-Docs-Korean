## *Bitwise Operators : 비트연산자*

*Bitwise operators enable you to manipulate the individual raw data bits within a data structure. They’re often used in low-level programming, such as graphics programming and device driver creation. Bitwise operators can also be useful when you work with raw data from external sources, such as encoding and decoding data for communication over a custom protocol.*

비트 연산자를 사용하면 데이터 구조 내에서 개별 원시 데이터 비트를 조작할 수 있습니다. 그래픽 프로그래밍 및 장치 드라이버 만들기와 같은 낮은 수준의 프로그래밍에 자주 사용됩니다. 비트 연산자는 사용자 정의 프로토콜을 통한 통신을 위해 인코딩 및 디코딩 데이터와 같은 외부 소스의 원시 데이터로 작업할 때도 유용할 수 있습니다.

*Swift supports all of the bitwise operators found in C, as described below.*

Swift는 아래 설명과 같이 C에 있는 모든 비트 연산자를 지원합니다.

### *Bitwise NOT Operator : NOT 비트연산자*

*The bitwise NOT operator (`~`) inverts all bits in a number:*

비트 NOT 연산자(`~`)는 숫자의 모든 비트를 반전합니다.

*![](https://docs.swift.org/swift-book/images/bitwiseNOT@2x.png)*

*The bitwise NOT operator is a prefix operator, and appears immediately before the value it operates on, without any white space:*

비트 NOT 연산자는 접두사 연산자이며 공백 없이 작동하는 값 바로 앞에 나타납니다.

```swift
let initialBits: UInt8 = 0b00001111
let invertedBits = ~initialBits  // equals 11110000
```

*`UInt8` integers have eight bits and can store any value between `0` and `255`. This example initializes a `UInt8` integer with the binary value `00001111`, which has its first four bits set to `0`, and its second four bits set to `1`. This is equivalent to a decimal value of `15`.*

`UInt8` 정수에는 8비트가 있으며 `0`에서 `255` 사이의 값을 저장할 수 있습니다. 이 예시는 `UInt8` 정수를 바이너리 값 `00001111`로 초기화합니다. 처음 4비트는 `0`으로 설정되고 두 번째 4비트는 `1`로 설정됩니다. 이는 `15`의 10진수 값에 해당합니다.

*The bitwise NOT operator is then used to create a new constant called `invertedBits`, which is equal to `initialBits`, but with all of the bits inverted. Zeros become ones, and ones become zeros. The value of `invertedBits` is `11110000`, which is equal to an unsigned decimal value of `240`.*

그런 다음 비트 NOT 연산자를 사용하여 `invertedBits`라는 새 상수를 생성합니다. 이 상수는 `initialBits`와 같지만 모든 비트가 반전됩니다. 0은 1이 되고 1은 0이 됩니다. `invertedBits`의 값은 `11110000`이며 부호 없는 십진수 `240`과 같습니다.

### *Bitwise AND Operator : AND 비트연산자*

*The bitwise AND operator (`&`) combines the bits of two numbers. It returns a new number whose bits are set to `1` only if the bits were equal to `1` in both input numbers:*

비트 AND 연산자(`&`)는 두 숫자의 비트를 결합합니다. 비트가 두 입력 숫자 모두에서 `1`과 같은 경우에만 비트가 `1`로 설정된 새 숫자를 반환합니다.

*![](https://docs.swift.org/swift-book/images/bitwiseAND@2x.png)*

*In the example below, the values of `firstSixBits` and `lastSixBits` both have four middle bits equal to `1`. The bitwise AND operator combines them to make the number `00111100`, which is equal to an unsigned decimal value of `60`:*

아래 예에서 `firstSixBits` 및 `lastSixBits` 값은 모두 `1`과 같은 4개의 중간 비트를 가집니다. 비트 AND 연산자는 이들을 결합하여 숫자 `00111100`을 만들고, 이는 부호 없는 십진수 값 `60`과 같습니다.

```swift
let firstSixBits: UInt8 = 0b11111100
let lastSixBits: UInt8  = 0b00111111
let middleFourBits = firstSixBits & lastSixBits  // equals 00111100
```

### *Bitwise OR Operator : OR 비트연산자*

*The bitwise OR operator (`|`) compares the bits of two numbers. The operator returns a new number whose bits are set to `1` if the bits are equal to `1` in either input number:*

비트 OR 연산자(`|`)는 두 숫자의 비트를 비교합니다. 연산자는 입력 숫자에서 비트가 `1`과 같으면 비트가 `1`로 설정된 새 숫자를 반환합니다.

*![](https://docs.swift.org/swift-book/images/bitwiseOR@2x.png)*

*In the example below, the values of `someBits` and `moreBits` have different bits set to `1`. The bitwise OR operator combines them to make the number `11111110`, which equals an unsigned decimal of `254`:*

아래 예에서 `someBits` 및 `moreBits`의 값은 `1`로 설정된 서로 다른 비트를 가집니다. 비트 OR 연산자는 이들을 결합하여 숫자 `11111110`을 만들고, 이는 부호 없는 십진수 `254`와 같습니다.

```swift
let someBits: UInt8 = 0b10110010
let moreBits: UInt8 = 0b01011110
let combinedbits = someBits | moreBits  // equals 11111110
```

### *Bitwise XOR Operator : XOR 비트연산자*

*The bitwise XOR operator, or “exclusive OR operator” (`^`), compares the bits of two numbers. The operator returns a new number whose bits are set to `1` where the input bits are different and are set to `0` where the input bits are the same:*

비트 XOR 연산자 또는 '배타적 OR 연산자'(`^`)는 두 숫자의 비트를 비교합니다. 연산자는 비트가 입력 비트가 다른 `1`로 설정되고 입력 비트가 동일한 `0`으로 설정된 새 숫자를 반환합니다.

*![](https://docs.swift.org/swift-book/images/bitwiseXOR@2x.png)*

*In the example below, the values of `firstBits` and `otherBits` each have a bit set to `1` in a location that the other does not. The bitwise XOR operator sets both of these bits to `1` in its output value. All of the other bits in `firstBits` and `otherBits` match and are set to `0` in the output value:*

아래 예에서 `firstBits` 및 `otherBits` 값은 각각 다른 위치에 `1`로 설정된 비트를 가집니다. 비트별 XOR 연산자는 출력 값에서 이 두 비트를 모두 `1`로 설정합니다. `firstBits` 및 `otherBits`의 다른 모든 비트는 일치하며 출력 값에서 `0`으로 설정됩니다.

```swift
let firstBits: UInt8 = 0b00010100
let otherBits: UInt8 = 0b00000101
let outputBits = firstBits ^ otherBits  // equals 00010001
```

### *Bitwise Left and Right Shift Operators : 비트 왼쪽 및 오른쪽 시프트 연산자*

*The bitwise left shift operator (`<<`) and bitwise right shift operator (`>>`) move all bits in a number to the left or the right by a certain number of places, according to the rules defined below.*

왼쪽 비트 시프트 연산자(`<<`) 및 비트 오른쪽 시프트 연산자(`>>`)는 아래에 정의된 규칙에 따라 숫자의 모든 비트를 왼쪽 또는 오른쪽으로 특정 위치만큼 이동합니다.

*Bitwise left and right shifts have the effect of multiplying or dividing an integer by a factor of two. Shifting an integer’s bits to the left by one position doubles its value, whereas shifting it to the right by one position halves its value.*

비트 왼쪽 및 오른쪽 시프트는 정수를 2의 인수로 곱하거나 나누는 효과가 있습니다. 정수의 비트를 왼쪽으로 한 위치 이동하면 값이 두 배가 되고 오른쪽으로 한 위치 이동하면 값이 절반이 됩니다.

#### *Shifting Behavior for Unsigned Integers : 부호 없는 정수에 대한 이동 동작*

*The bit-shifting behavior for unsigned integers is as follows:*

부호 없는 정수에 대한 비트 이동 동작은 다음과 같습니다.

1. *Existing bits are moved to the left or right by the requested number of places.*
   
   기존의 비트를 요청한 위치만큼 왼쪽 또는 오른쪽으로 이동합니다.

2. *Any bits that are moved beyond the bounds of the integer’s storage are discarded.*
   
   정수 저장소의 경계를 넘어 이동된 모든 비트는 폐기됩니다.

3. *Zeros are inserted in the spaces left behind after the original bits are moved to the left or right.*
   
   원래 비트를 왼쪽이나 오른쪽으로 이동한 후 남은 공간에 0이 삽입됩니다.

*This approach is known as a logical shift.*

이 접근 방식을 논리적 이동이라고 합니다.

*The illustration below shows the results of `11111111 << 1` (which is `11111111` shifted to the left by `1` place), and `11111111 >> 1` (which is `11111111` shifted to the right by `1` place). Blue numbers are shifted, gray numbers are discarded, and orange zeros are inserted:*

아래 그림은 `11111111 << 1`(`11111111`이 왼쪽으로 `1`만큼 이동됨) 및 `11111111 >> 1`(`11111111`이 `1`만큼 오른쪽으로 이동됨)의 결과를 보여줍니다.). 파란색 숫자는 이동되고 회색 숫자는 삭제되며 주황색 0이 삽입됩니다.

*![](https://docs.swift.org/swift-book/images/bitshiftUnsigned@2x.png)*

*Here’s how bit shifting looks in Swift code:*

Swift 코드에서 비트 이동이 어떻게 보이는지 보여줍니다.

```swift
let shiftBits: UInt8 = 4   // 00000100 in binary
shiftBits << 1             // 00001000
shiftBits << 2             // 00010000
shiftBits << 5             // 10000000
shiftBits << 6             // 00000000
shiftBits >> 2             // 00000001
```

*You can use bit shifting to encode and decode values within other data types:*

비트 이동을 사용하여 다른 데이터 타입 내의 값을 인코딩 및 디코딩할 수 있습니다.

```swift
let pink: UInt32 = 0xCC6699
let redComponent = (pink & 0xFF0000) >> 16    // redComponent is 0xCC, or 204
let greenComponent = (pink & 0x00FF00) >> 8   // greenComponent is 0x66, or 102
let blueComponent = pink & 0x0000FF           // blueComponent is 0x99, or 153
```

*This example uses a `UInt32` constant called `pink` to store a Cascading Style Sheets color value for the color pink. The CSS color value `#CC6699` is written as `0xCC6699` in Swift’s hexadecimal number representation. This color is then decomposed into its red (`CC`), green (`66`), and blue (`99`) components by the bitwise AND operator (`&`) and the bitwise right shift operator (`>>`).*

이 예에서는 `pink`라는 `UInt32` 상수를 사용하여 분홍색에 대한 Cascading Style Sheets 색상 값을 저장합니다. CSS 색상 값 `#CC6699`는 Swift의 16진수 표현에서 `0xCC6699`로 작성됩니다. 그런 다음 이 색상은 비트 AND 연산자(`&`)와 비트 오른쪽 시프트 연산자(`>>`)에 의해 빨간색(`CC`), 녹색(`66`) 및 파란색(`99`) 구성요소로 분해됩니다. ).

*The red component is obtained by performing a bitwise AND between the numbers `0xCC6699` and `0xFF0000`. The zeros in `0xFF0000` effectively “mask” the second and third bytes of `0xCC6699`, causing the `6699` to be ignored and leaving `0xCC0000` as the result.*

빨간색 구성요소는 숫자 `0xCC6699`와 `0xFF0000` 사이에 비트 AND를 수행하여 얻습니다. `0xFF0000`의 0은 `0xCC6699`의 두 번째 및 세 번째 바이트를 효과적으로 '마스킹'하여 `6699`를 무시하고 결과적으로 `0xCC0000`을 남깁니다.

*This number is then shifted 16 places to the right (`>> 16`). Each pair of characters in a hexadecimal number uses 8 bits, so a move 16 places to the right will convert `0xCC0000` into `0x0000CC`. This is the same as `0xCC`, which has a decimal value of `204`.*

이 숫자는 오른쪽으로 16칸 이동합니다(`>> 16`). 16진수의 각 문자 쌍은 8비트를 사용하므로 오른쪽으로 16자리 이동하면 `0xCC0000`이 `0x0000CC`로 변환됩니다. 이는 10진수 값이 `204`인 `0xCC`와 동일합니다.

*Similarly, the green component is obtained by performing a bitwise AND between the numbers `0xCC6699` and `0x00FF00`, which gives an output value of `0x006600`. This output value is then shifted eight places to the right, giving a value of `0x66`, which has a decimal value of `102`.*

마찬가지로, 녹색 구성요소는 숫자 `0xCC6699`와 `0x00FF00` 사이에 비트 AND를 수행하여 얻어지며, 출력 값은 `0x006600`입니다. 그런 다음 이 출력 값은 오른쪽으로 8자리 이동하여 값이 `0x66`이고 십진수 값이 `102`입니다.

*Finally, the blue component is obtained by performing a bitwise AND between the numbers `0xCC6699` and `0x0000FF`, which gives an output value of `0x000099`. Because `0x000099` already equals `0x99`, which has a decimal value of `153`, this value is used without shifting it to the right,*

마지막으로 파란색 구성요소는 숫자 `0xCC6699`와 `0x0000FF` 사이에 비트 AND를 수행하여 얻어지며, 출력 값은 `0x000099`입니다. '0x000099'는 이미 '0x99'와 같기 때문에 십진수 값이 `153`이므로 이 값은 오른쪽으로 이동하지 않고 사용됩니다.

#### *Shifting Behavior for Signed Integer : Signed Integer의 이동 동작*

*The shifting behavior is more complex for signed integers than for unsigned integers, because of the way signed integers are represented in binary. (The examples below are based on 8-bit signed integers for simplicity, but the same principles apply for signed integers of any size.)*

이동 동작은 부호 있는 정수가 이진법으로 표현되는 방식 때문에 부호 없는 정수보다 부호 있는 정수에서 더 복잡합니다. (아래 예제는 단순화를 위해 8비트 부호 있는 정수를 기반으로 하지만 동일한 원칙이 모든 크기의 부호 있는 정수에 적용됩니다.)

*Signed integers use their first bit (known as the sign bit) to indicate whether the integer is positive or negative. A sign bit of `0` means positive, and a sign bit of `1` means negative.*

부호 있는 정수는 첫 번째 비트(부호 비트라고 함)를 사용하여 정수가 양수인지 음수인지 나타냅니다. 부호 비트 `0`은 양수를 의미하고 부호 비트 `1`은 음수를 의미합니다.

*The remaining bits (known as the value bits) store the actual value. Positive numbers are stored in exactly the same way as for unsigned integers, counting upwards from `0`. Here’s how the bits inside an `Int8` look for the number `4`:*

나머지 비트(값 비트라고 함)는 실제 값을 저장합니다. 양수는 `0`부터 위쪽으로 세는 부호가 없는 정수와 정확히 같은 방식으로 저장됩니다. 다음은 `Int8` 내부의 비트가 숫자 `4`를 찾는 방법입니다.

*![](https://docs.swift.org/swift-book/images/bitshiftSignedFour@2x.png)*

*The sign bit is `0` (meaning “positive”), and the seven value bits are just the number `4`, written in binary notation.*

부호 비트는 `0`('양수'를 의미)이고 7개의 값 비트는 이진 표기법으로 작성된 숫자 `4`입니다.

*Negative numbers, however, are stored differently. They’re stored by subtracting their absolute value from `2` to the power of `n`, where `n` is the number of value bits. An eight-bit number has seven value bits, so this means `2` to the power of `7`, or `128`.*

그러나 음수는 다르게 저장됩니다. `2`에서 절대값을 빼서 `n`의 거듭제곱으로 저장합니다. 여기서 `n`은 값 비트의 수입니다. 8비트 숫자에는 7개의 값 비트가 있으므로 이는 `2`의 `7`승 또는 `128`을 의미합니다.

*Here’s how the bits inside an `Int8` look for the number `-4`:*

`Int8` 내부의 비트가 숫자 `-4`를 찾는 방법은 다음과 같습니다.

*![](https://docs.swift.org/swift-book/images/bitshiftSignedMinusFour@2x.png)*

*This time, the sign bit is `1` (meaning “negative”), and the seven value bits have a binary value of `124` (which is `128 - 4`):*

이번에 부호 비트는 `1`('음수'를 의미)이고 7개의 값 비트는 이진 값 `124`(`128 - 4`)입니다.

*![](https://docs.swift.org/swift-book/images/bitshiftSignedMinusFourValue@2x.png)*

*This encoding for negative numbers is known as a two’s complement representation. It may seem an unusual way to represent negative numbers, but it has several advantages.*

음수에 대한 이 인코딩을 2의 보수 표현이라고 합니다. 음수를 나타내는 방법이 이상해 보일 수 있지만 몇 가지 장점이 있습니다.

*First, you can add `-1` to `-4`, simply by performing a standard binary addition of all eight bits (including the sign bit), and discarding anything that doesn’t fit in the eight bits once you’re done:*

첫째, 모든 8비트(부호 비트 포함)의 표준 이진 덧셈을 수행 완료하고 8비트에 맞지 않는 항목을 버리는 방식으로 `-1`을 `-4`에 추가할 수 있습니다:

*![](https://docs.swift.org/swift-book/images/bitshiftSignedAddition@2x.png)*

*Second, the two’s complement representation also lets you shift the bits of negative numbers to the left and right like positive numbers, and still end up doubling them for every shift you make to the left, or halving them for every shift you make to the right. To achieve this, an extra rule is used when signed integers are shifted to the right: When you shift signed integers to the right, apply the same rules as for unsigned integers, but fill any empty bits on the left with the sign bit, rather than with a zero.*

두 번째로, 두 개의 보수 표현을 사용하면 음수의 비트를 양수처럼 왼쪽과 오른쪽으로 이동할 수 있지만, 왼쪽으로 이동할 때마다 두 배로 늘리거나 오른쪽으로 이동할 때마다 두 배로 줄이거나, 오른쪽으로 이동할 때마다 두 배로 늘립니다. 이를 위해 부호 있는 정수를 오른쪽으로 이동할 때 추가 규칙이 사용됩니다: 부호 있는 정수를 오른쪽으로 이동할 때는 부호 없는 정수와 동일한 규칙을 적용하되 왼쪽의 빈 비트를 0이 아닌 부호 비트로 채우세요.

*![](https://docs.swift.org/swift-book/images/bitshiftSigned@2x.png)*

*This action ensures that signed integers have the same sign after they’re shifted to the right, and is known as an arithmetic shift.*

이 동작은 부호 있는 정수가 오른쪽으로 이동한 후에도 동일한 부호를 갖도록 하며, 이를 산술 이동이라고 합니다.

*Because of the special way that positive and negative numbers are stored, shifting either of them to the right moves them closer to zero. Keeping the sign bit the same during this shift means that negative integers remain negative as their value moves closer to zero.*

양수와 음수가 저장되는 특별한 방식 때문에 양수와 음수 중 하나를 오른쪽으로 이동하면 양수와 음수가 0에 가까워집니다. 이 이동 중에 부호 비트를 동일하게 유지하면 음수 정수의 값이 0에 가까워져도 음수로 유지됩니다.
