## *Bitwise Operators*

*Bitwise operators enable you to manipulate the individual raw data bits within a data structure. They’re often used in low-level programming, such as graphics programming and device driver creation. Bitwise operators can also be useful when you work with raw data from external sources, such as encoding and decoding data for communication over a custom protocol.*

*Swift supports all of the bitwise operators found in C, as described below.*

### *Bitwise NOT Operator*

*The bitwise NOT operator (`~`) inverts all bits in a number:*

*![](https://docs.swift.org/swift-book/images/bitwiseNOT@2x.png)*

*The bitwise NOT operator is a prefix operator, and appears immediately before the value it operates on, without any white space:*

```swift
let initialBits: UInt8 = 0b00001111
let invertedBits = ~initialBits  // equals 11110000
```

*`UInt8` integers have eight bits and can store any value between `0` and `255`. This example initializes a `UInt8` integer with the binary value `00001111`, which has its first four bits set to `0`, and its second four bits set to `1`. This is equivalent to a decimal value of `15`.*

*The bitwise NOT operator is then used to create a new constant called `invertedBits`, which is equal to `initialBits`, but with all of the bits inverted. Zeros become ones, and ones become zeros. The value of `invertedBits` is `11110000`, which is equal to an unsigned decimal value of `240`.*

### *Bitwise AND Operator*

*The bitwise AND operator (`&`) combines the bits of two numbers. It returns a new number whose bits are set to `1` only if the bits were equal to `1` in both input numbers:*

*![](https://docs.swift.org/swift-book/images/bitwiseAND@2x.png)*

*In the example below, the values of `firstSixBits` and `lastSixBits` both have four middle bits equal to `1`. The bitwise AND operator combines them to make the number `00111100`, which is equal to an unsigned decimal value of `60`:*

```swift
let firstSixBits: UInt8 = 0b11111100
let lastSixBits: UInt8  = 0b00111111
let middleFourBits = firstSixBits & lastSixBits  // equals 00111100
```

### *Bitwise OR Operator*

*The bitwise OR operator (`|`) compares the bits of two numbers. The operator returns a new number whose bits are set to `1` if the bits are equal to `1` in either input number:*

*![](https://docs.swift.org/swift-book/images/bitwiseOR@2x.png)*

*In the example below, the values of `someBits` and `moreBits` have different bits set to `1`. The bitwise OR operator combines them to make the number `11111110`, which equals an unsigned decimal of `254`:*

```swift
let someBits: UInt8 = 0b10110010
let moreBits: UInt8 = 0b01011110
let combinedbits = someBits | moreBits  // equals 11111110
```

### *Bitwise XOR Operator*

*The bitwise XOR operator, or “exclusive OR operator” (`^`), compares the bits of two numbers. The operator returns a new number whose bits are set to `1` where the input bits are different and are set to `0` where the input bits are the same:*

*![](https://docs.swift.org/swift-book/images/bitwiseXOR@2x.png)*

*In the example below, the values of `firstBits` and `otherBits` each have a bit set to `1` in a location that the other does not. The bitwise XOR operator sets both of these bits to `1` in its output value. All of the other bits in `firstBits` and `otherBits` match and are set to `0` in the output value:*

```swift
let firstBits: UInt8 = 0b00010100
let otherBits: UInt8 = 0b00000101
let outputBits = firstBits ^ otherBits  // equals 00010001
```

### *Bitwise Left and Right Shift Operators*

*The bitwise left shift operator (`<<`) and bitwise right shift operator (`>>`) move all bits in a number to the left or the right by a certain number of places, according to the rules defined below.*

*Bitwise left and right shifts have the effect of multiplying or dividing an integer by a factor of two. Shifting an integer’s bits to the left by one position doubles its value, whereas shifting it to the right by one position halves its value.*

#### *Shifting Behavior for Unsigned Integers*

*The bit-shifting behavior for unsigned integers is as follows:*

1. *Existing bits are moved to the left or right by the requested number of places.*

2. *Any bits that are moved beyond the bounds of the integer’s storage are discarded.*

3. *Zeros are inserted in the spaces left behind after the original bits are moved to the left or right.*

*This approach is known as a logical shift.*

*The illustration below shows the results of `11111111 << 1` (which is `11111111` shifted to the left by `1` place), and `11111111 >> 1` (which is `11111111` shifted to the right by `1` place). Blue numbers are shifted, gray numbers are discarded, and orange zeros are inserted:*

*![](https://docs.swift.org/swift-book/images/bitshiftUnsigned@2x.png)*

*Here’s how bit shifting looks in Swift code:*

```swift
let shiftBits: UInt8 = 4   // 00000100 in binary
shiftBits << 1             // 00001000
shiftBits << 2             // 00010000
shiftBits << 5             // 10000000
shiftBits << 6             // 00000000
shiftBits >> 2             // 00000001
```

*You can use bit shifting to encode and decode values within other data types:*

```swift
let pink: UInt32 = 0xCC6699
let redComponent = (pink & 0xFF0000) >> 16    // redComponent is 0xCC, or 204
let greenComponent = (pink & 0x00FF00) >> 8   // greenComponent is 0x66, or 102
let blueComponent = pink & 0x0000FF           // blueComponent is 0x99, or 153
```

*This example uses a `UInt32` constant called `pink` to store a Cascading Style Sheets color value for the color pink. The CSS color value `#CC6699` is written as `0xCC6699` in Swift’s hexadecimal number representation. This color is then decomposed into its red (`CC`), green (`66`), and blue (`99`) components by the bitwise AND operator (`&`) and the bitwise right shift operator (`>>`).*

*The red component is obtained by performing a bitwise AND between the numbers `0xCC6699` and `0xFF0000`. The zeros in `0xFF0000` effectively “mask” the second and third bytes of `0xCC6699`, causing the `6699` to be ignored and leaving `0xCC0000` as the result.*

*This number is then shifted 16 places to the right (`>> 16`). Each pair of characters in a hexadecimal number uses 8 bits, so a move 16 places to the right will convert `0xCC0000` into `0x0000CC`. This is the same as `0xCC`, which has a decimal value of `204`.*

*Similarly, the green component is obtained by performing a bitwise AND between the numbers `0xCC6699` and `0x00FF00`, which gives an output value of `0x006600`. This output value is then shifted eight places to the right, giving a value of `0x66`, which has a decimal value of `102`.*

*Finally, the blue component is obtained by performing a bitwise AND between the numbers `0xCC6699` and `0x0000FF`, which gives an output value of `0x000099`. Because `0x000099` already equals `0x99`, which has a decimal value of `153`, this value is used without shifting it to the right,*

#### *Shifting Behavior for Signed Integer*

*The shifting behavior is more complex for signed integers than for unsigned integers, because of the way signed integers are represented in binary. (The examples below are based on 8-bit signed integers for simplicity, but the same principles apply for signed integers of any size.)*

*Signed integers use their first bit (known as the sign bit) to indicate whether the integer is positive or negative. A sign bit of `0` means positive, and a sign bit of `1` means negative.*

*The remaining bits (known as the value bits) store the actual value. Positive numbers are stored in exactly the same way as for unsigned integers, counting upwards from `0`. Here’s how the bits inside an `Int8` look for the number `4`:*

*![](https://docs.swift.org/swift-book/images/bitshiftSignedFour@2x.png)*

*The sign bit is `0` (meaning “positive”), and the seven value bits are just the number `4`, written in binary notation.*

*Negative numbers, however, are stored differently. They’re stored by subtracting their absolute value from `2` to the power of `n`, where `n` is the number of value bits. An eight-bit number has seven value bits, so this means `2` to the power of `7`, or `128`.*

*Here’s how the bits inside an `Int8` look for the number `-4`:*

*![](https://docs.swift.org/swift-book/images/bitshiftSignedMinusFour@2x.png)*

*This time, the sign bit is `1` (meaning “negative”), and the seven value bits have a binary value of `124` (which is `128 - 4`):*

*![](https://docs.swift.org/swift-book/images/bitshiftSignedMinusFourValue@2x.png)*

*This encoding for negative numbers is known as a two’s complement representation. It may seem an unusual way to represent negative numbers, but it has several advantages.*

*First, you can add `-1` to `-4`, simply by performing a standard binary addition of all eight bits (including the sign bit), and discarding anything that doesn’t fit in the eight bits once you’re done:*

*![](https://docs.swift.org/swift-book/images/bitshiftSignedAddition@2x.png)*

*Second, the two’s complement representation also lets you shift the bits of negative numbers to the left and right like positive numbers, and still end up doubling them for every shift you make to the left, or halving them for every shift you make to the right. To achieve this, an extra rule is used when signed integers are shifted to the right: When you shift signed integers to the right, apply the same rules as for unsigned integers, but fill any empty bits on the left with the sign bit, rather than with a zero.*

*![](https://docs.swift.org/swift-book/images/bitshiftSigned@2x.png)*

*This action ensures that signed integers have the same sign after they’re shifted to the right, and is known as an arithmetic shift.*

*Because of the special way that positive and negative numbers are stored, shifting either of them to the right moves them closer to zero. Keeping the sign bit the same during this shift means that negative integers remain negative as their value moves closer to zero.*


