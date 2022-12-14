## *Comparing Strings : 문자열 비교*

*Swift provides three ways to compare textual values: string and character equality, prefix equality, and suffix equality.*

Swift는 문자열 및 문자 동일성, 접두사 동일성 그리고 접미사 동일성의 세가지 텍스트 값 비교 방법을 제공합니다.

### *String and Character Equality : 문자열 및 문자 동일성*

*String and character equality is checked with the “equal to” operator (`==`) and the “not equal to” operator (`!=`), as described in [Comparison Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html#ID70):*

문자열 및 문자 동일성은 [링크] 에 설명된 대로 "같음"  연산자 (`==`)  및 "같지 않음" 연산자 (!=)를 사용해서 확인합니다.

```swift
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

*Two `String` values (or two `Character` values) are considered equal if their extended grapheme clusters are canonically equivalent. Extended grapheme clusters are canonically equivalent if they have the same linguistic meaning and appearance, even if they’re composed from different Unicode scalars behind the scenes.*

두 `String` 값 (혹은 두 `Character` 값)은 확장된 grapheme clusters가 표준적으로 동일할 경우 동일한 것으로 간주됩니다. 확장된 grapheme clusters는 비록 뒤에서 서로 다른 유니코드 스칼라 값으로 구성되어 있더라도 동일한 언어적 의미와 모양을 가진 경우 표준적으로 동일합니다. 

*For example, `LATIN SMALL LETTER E WITH ACUTE` (`U+00E9`) is canonically equivalent to `LATIN SMALL LETTER E` (`U+0065`) followed by `COMBINING ACUTE ACCENT` (`U+0301`). Both of these extended grapheme clusters are valid ways to represent the character `é`, and so they’re considered to be canonically equivalent:*

예를 들어,  `LATIN SMALL LETTER E WITH ACUTE` (`U+00E9`) 은 표준적으로  `COMBINING ACUTE ACCENT` (`U+0301`) 에 뒤따라 오는  `LATIN SMALL LETTER E` (`U+0065`) 와  규범적으로(표준적으로) 동일합니다. 이 두 확장된 `grapheme clusters`은 모두 문자 `é`를 표현하는 유효한 방법이며, 따라서 표준적으로 동일한 것으로 간주됩니다. 

```swift
// "Voulez-vous un café?" using LATIN SMALL LETTER E WITH ACUTE
let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"

// "Voulez-vous un café?" using LATIN SMALL LETTER E and COMBINING ACUTE ACCENT
let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"

if eAcuteQuestion == combinedEAcuteQuestion {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

*Conversely, `LATIN CAPITAL LETTER A` (`U+0041`, or `"A"`), as used in English, is not equivalent to `CYRILLIC CAPITAL LETTER A` (`U+0410`, or `"А"`), as used in Russian. The characters are visually similar, but don’t have the same linguistic meaning:*

```swift
let latinCapitalLetterA: Character = "\u{41}"

let cyrillicCapitalLetterA: Character = "\u{0410}"

if latinCapitalLetterA != cyrillicCapitalLetterA {
    print("These two characters aren't equivalent.")
}
// Prints "These two characters aren't equivalent."
```

> *NOTE*
> 
> *String and character comparisons in Swift aren’t locale-sensitive.*
> 
> Swift에서 문자열과 문자 비교는 지역에 민감하지 않습니다.

### *Prefix and Suffix Equality : 접두사와 접미사 동일성*

*To check whether a string has a particular string prefix or suffix, call the string’s `hasPrefix(_:)` and `hasSuffix(_:)` methods, both of which take a single argument of type `String` and return a Boolean value.*

문자열에 특정 문자열 접두사 혹은 접미사가 있는지 확인하려면 둘 다 문자열 형식의 단일 인수를 사용하고 `Boolean` 값을 리턴하는 문자열의 `hasPrefix(*:)`  `hasSuffix(*:)` 메서드를 호출합니다.

*The examples below consider an array of strings representing the scene locations from the first two acts of Shakespeare’s Romeo and Juliet:*

아래의 예시는 셰익스피어의 로미오와 줄리엣의 첫 2막의 장면 위치를 나타내는 문자열의 배열을 고려합니다.

```swift
let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]
```

*You can use the `hasPrefix(_:)` method with the `romeoAndJuliet` array to count the number of scenes in Act 1 of the play:*

`romeoAndJuliet` 배열과 함께 `hasPrefix(_:)` 메소드를 사용하여 연극 1막의 장면 갯수를 셀 수 있습니다. 

```swift
var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        act1SceneCount += 1
    }
}
print("There are \(act1SceneCount) scenes in Act 1")
// Prints "There are 5 scenes in Act 1"
```

*Similarly, use the `hasSuffix(_:)` method to count the number of scenes that take place in or around Capulet’s mansion and Friar Lawrence’s cell:*

비슷하게, `hasSuffix(_:)` 메서드를 사용해서 캐퓰렛의 저택과 로렌스 수사의 감방 안에서 혹은 그 주변에서 일어나는 장면의 수를 세어보세요.(?)

> *NOTE*
> 
> *The `hasPref*ix(_:)` and `hasSuffix(_:)` methods perform a character-by-character canonical equivalence comparison between the extended grapheme clusters in each string, as described in [String and Character Equality](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html#ID299).*
> 
>  `hasPref*ix(_:)` 와 `hasSuffix(_:)` 메서드는 [링크]에 설명된 대로 각 문자열의 확장된 grapheme cluster 간의 문자별 표준 동등성 비교를 수행합니다. 
