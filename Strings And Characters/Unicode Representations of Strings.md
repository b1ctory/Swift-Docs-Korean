## *Unicode Representations of Strings : 문자열의 유니코드 표현*

*When a Unicode string is written to a text file or some other storage, the Unicode scalars in that string are encoded in one of several Unicode-defined encoding forms. Each form encodes the string in small chunks known as code units. These include the UTF-8 encoding form (which encodes a string as 8-bit code units), the UTF-16 encoding form (which encodes a string as 16-bit code units), and the UTF-32 encoding form (which encodes a string as 32-bit code units).*

유니코드의 문자열이 텍스트 파일이나 다른 저장소에 기록되면 해당 문자열의 유니코드 스칼라는 여러 유니코드 정의 인코딩 형식 중의 하나로 인코딩됩니다. 각 형식은 코드 단위로 알려진 작은 청크로 문자열을 인코딩합니다. 여기에는 UTF-8 인코딩 형식 (문자열을 8비트 단위로 인코딩), UTF-16 인코딩 형식 (문자열을 16비트 단위로 인코딩), UTF-32 (문자열을 32비트 코드 단위로 인코딩) 인코딩 형식이 포함됩니다.

*Swift provides several different ways to access Unicode representations of strings. You can iterate over the string with a `for`-`in` statement, to access its individual `Character` values as Unicode extended grapheme clusters. This process is described in [Working with Characters](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html#ID290).*

Swift는 유니코드 문자열 표현에 엑세스 할 수 있는 여러가지 방법을 제공합니다. 문자열 안에 `for-in` 문을 반복해서 개별 `Character` 값을 유니코드 확장 grapheme clusters로 엑세스할 수 있습니다. 이 과정은 [링크]에 설명되어 있습니다.

*Alternatively, access a `String` value in one of three other Unicode-compliant representations:*

대신에, 다른 세가지 유니코드 호환 표현 중 하나로  `String` 값에 엑세스합니다.

- *A collection of UTF-8 code units (accessed with the string’s `utf8` property)*
  
  UTF-8 코드 단위 모음 (문자열의 "utf8" 속성으로 액세스)

- *A collection of UTF-16 code units (accessed with the string’s `utf16` property)*
  
  UTF-16 코드 단위 모음 (문자열의 'utf16' 속성으로 액세스)

- *A collection of 21-bit Unicode scalar values, equivalent to the string’s UTF-32 encoding form (accessed with the string’s `unicodeScalars` property)*
  
  문자열의 UTF-32 인코딩 형식과 동일한 21비트 유니코드 스칼라 값의 모음(문자열의 "unicodeScalars" 속성으로 액세스)

*Each example below shows a different representation of the following string, which is made up of the characters `D`, `o`, `g`, `‼` (`DOUBLE EXCLAMATION MARK`, or Unicode scalar `U+203C`), and the 🐶 character (`DOG FACE`, or Unicode scalar `U+1F436`):*

각각의 예시는  `D`, `o`, `g`, `‼` (`DOUBLE EXCLAMATION MARK` 혹은 유니코드 스칼라 `U+203C`) 및 🐶문자 (`DOG FACE` 혹은 유니코드 스칼라 `U+1F436`)로 구성된 다음 문자열의 서로 다른 표현을 보여줍니다.

```swift
let dogString = "Dog‼🐶"
```

### *UTF-8 Representation : UTF-8 표현*

*You can access a UTF-8 representation of a `String` by iterating over its `utf8` property. This property is of type `String.UTF8View`, which is a collection of unsigned 8-bit (`UInt8`) values, one for each byte in the string’s UTF-8 representation:*

`utf8` 속성을 반복해서 `String`의 UTF-8 표현에 엑세스할 수 있습니다. 이 속성은 String.UTF8View 타입이며, 이는 부호 없는 8비트 값(`UInt8`)의 모음으로, 문자열의 UTF-8 표현의 각 바이트에 대해 하나씩 표시됩니다.

![](https://docs.swift.org/swift-book/_images/UTF8_2x.png)

```swift
for codeUnit in dogString.utf8 {
    print("\(codeUnit) ", terminator: "")
}
print("")
// Prints "68 111 103 226 128 188 240 159 144 182 "
```

*In the example above, the first three decimal `codeUnit` values (`68`, `111`, `103`) represent the characters `D`, `o`, and `g`, whose UTF-8 representation is the same as their ASCII representation. The next three decimal `codeUnit` values (`226`, `128`, `188`) are a three-byte UTF-8 representation of the `DOUBLE EXCLAMATION MARK` character. The last four `codeUnit` values (`240`, `159`, `144`, `182`) are a four-byte UTF-8 representation of the `DOG FACE` character.*

위의 예에서 codeUnit의 처음 세개 십진수 (`68`, `111`, `103`)는 UTF-8 표현이 ASCII 표현과 동일한 문자인 `D`, `o`, `g`를 나타냅니다. 다음 세개의 십진수 `codeUnit` (`226`, `128`, `188`) 은 `DOUBLE EXCLAMATION MARK` 문자를 3바이트 UTF-8로 표현한 것입니다. 마지막 네개의  `codeUnit` 값 (`240`, `159`, `144`, `182`)은 `DOG FACE` 문자를 4바이트 UTF-8로 표현한 것입니다.

### *UTF-16 Representation : UTF-16 표현*

*You can access a UTF-16 representation of a `String` by iterating over its `utf16` property. This property is of type `String.UTF16View`, which is a collection of unsigned 16-bit (`UInt16`) values, one for each 16-bit code unit in the string’s UTF-16 representation:*

UTF-16 속성을 반복해서 String의 UTF-16 표현에 엑세스할 수 있습니다. 이 속성은 String.UTF16View의 유형으로, 부호 없는 16비트 (`UInt16`)값의 모음으로서 문자열의 UTF-16 표현에서 16비트 코드 단위 마다 하나씩 표현됩니다.

![](https://docs.swift.org/swift-book/_images/UTF16_2x.png)

```swift
for codeUnit in dogString.utf16 {
    print("\(codeUnit) ", terminator: "")
}
print("")
// Prints "68 111 103 8252 55357 56374 "
```

*Again, the first three `codeUnit` values (`68`, `111`, `103`) represent the characters `D`, `o`, and `g`, whose UTF-16 code units have the same values as in the string’s UTF-8 representation (because these Unicode scalars represent ASCII characters).*

다시 ㅁ라하지만, 처음 세개의 `codeUnit` 값 (`68`, `111`, `103`)은 UTF-16 코드 단위가 문자열의 UTF-8과 동일한 값을 갖는 문자 `D`, `o`, `g` 를 나타냅니다. (이는 유니코드 스칼라가 ASCII 문자를 나타내기 때문입니다.)

*The fourth `codeUnit` value (`8252`) is a decimal equivalent of the hexadecimal value `203C`, which represents the Unicode scalar `U+203C` for the `DOUBLE EXCLAMATION MARK` character. This character can be represented as a single code unit in UTF-16.*

네 번째 `codeUnit` 값 (`8252`)는 16진수 값 `203C`에 해당하며, 이는  `DOUBLE EXCLAMATION MARK` 문자에 대한 유니코드 스칼라 `U+203C`를 나타냅니다. 이 문자는 UTF-16에서 단일 코드 단위로 표현될 수 있습니다.

*The fifth and sixth `codeUnit` values (`55357` and `56374`) are a UTF-16 surrogate pair representation of the `DOG FACE` character. These values are a high-surrogate value of `U+D83D` (decimal value `55357`) and a low-surrogate value of `U+DC36` (decimal value `56374`).*

다섯번째와 여섯번째 코드 단위 값 (`55357` 과 `56374`)은 `DOG FACE` 문자를 UTF-16 대리 쌍으로 표현한 것입니다. 이 값들은 높은-대리값 `U+D83D` (10진수 값 `55357`)과 낮은 대리값 `U+DC36` (10진수 값 `56374`) 입니다.

### *Unicode Scalar Representation : 유니코드 스칼라 표현*

*You can access a Unicode scalar representation of a `String` value by iterating over its `unicodeScalars` property. This property is of type `UnicodeScalarView`, which is a collection of values of type `UnicodeScalar`.*

`unicodeScalars` 속성을 반복해서 문자열 값의 유니코드 스칼라 표현에 엑세스 할 수 있습니다. 이 속성은 `UnocideScalar`타입의 값 모음인 `UnicodeScalarView` 타입입니다. 

*Each `UnicodeScalar` has a `value` property that returns the scalar’s 21-bit value, represented within a `UInt32` value:*

각각의 `UnicodeScalar` 는 스칼라의 21비트 값을 반환하고 `UInt32` 값으로 대표되는 `value` 속성을 가지고 있습니다. 

![](https://docs.swift.org/swift-book/_images/UnicodeScalar_2x.png)

```swift
for scalar in dogString.unicodeScalars {
    print("\(scalar.value) ", terminator: "")
}
print("")
// Prints "68 111 103 8252 128054 "
```

*The `value` properties for the first three `UnicodeScalar` values (`68`, `111`, `103`) once again represent the characters `D`, `o`, and `g`.*

첫번째 세개 `UnicodeScalar`값 (`68`, `111`, `103`)의 값 속성은 다시 `D`, `o`, `g`를 나타냅니다. 

*The fourth `codeUnit` value (`8252`) is again a decimal equivalent of the hexadecimal value `203C`, which represents the Unicode scalar `U+203C` for the `DOUBLE EXCLAMATION MARK` character.*

네번째 `codeUnit` 값 (`8252`)는 다시 16진수 값 `203C`에 해당하며 이는 `DOUBLE EXCLAMATION MARK` 문자에 대한 유니코드 스칼라 `U+203C`를 나타냅니다. 

*The `value` property of the fifth and final `UnicodeScalar`, `128054`, is a decimal equivalent of the hexadecimal value `1F436`, which represents the Unicode scalar `U+1F436` for the `DOG FACE` character.*

다섯번째이자 마지막 `UnicodeScalar`인 `128054`의 값 속성은 16진수 값 `1F436`에 해당하며, 이는 `DOG FACE `문자에 대한 유니코드 스칼라  `U+1F436` 을 나타냅니다. 

*As an alternative to querying their `value` properties, each `UnicodeScalar` value can also be used to construct a new `String` value, such as with string interpolation:*

값 속성을 쿼리하는 대신, `UnicodeScalar` 값을 사용해서 문자열 보간과 같은 새로운 `String` 값을 구성할 수도 있습니다.

```swift
for scalar in dogString.unicodeScalars {
    print("\(scalar) ")
}
// D
// o
// g
// ‼
// 🐶
```
