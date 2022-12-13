## *Unicode : 유니코드*

*Unicode is an international standard for encoding, representing, and processing text in different writing systems. It enables you to represent almost any character from any language in a standardized form, and to read and write those characters to and from an external source such as a text file or web page. Swift’s `String` and `Character` types are fully Unicode-compliant, as described in this section.*

유니코드는 다양한 쓰기 시스템에서 텍스트를 인코딩, 표현 및 처리하기 위한 국제 표준입니다. 표준화된 형식으로 모든 언어의 거의 모든 문자를 표시하고 텍스트 파일이나 웹 페이지와 같은 외부 소스에서 이러한 문자를 읽고 쓸 수 있습니다. 스위프트의 문자열과 문자 타입은 이 절에서 설명한 바와 같이 유니코드를 완전히 준수합니다. 

### *Unicode Scalar Values : 유니코드 스칼라 값*

*Behind the scenes, Swift’s native `String` type is built from Unicode scalar values. A Unicode scalar value is a unique 21-bit number for a character or modifier, such as `U+0061` for `LATIN SMALL LETTER A` (`"a"`), or `U+1F425` for `FRONT-FACING BABY CHICK` (`"🐥"`).*

그 이면에는, Swift의 네이티브  `String`타입이 유니코드 스칼라 값으로 구축되어 있습니다. 유니코드 스칼라 값은 `LATIN SMALL LETTER A` (`"a"`) 를 위한  `U+0061`, 혹은 `FRONT-FACING BABY CHICK` (`"🐥"`) 을 위한 `U+1F425` 값 등의 유니크한 문자나 수식자의 21비트 숫자입니다.

*Note that not all 21-bit Unicode scalar values are assigned to a character—some scalars are reserved for future assignment or for use in UTF-16 encoding. Scalar values that have been assigned to a character typically also have a name, such as `LATIN SMALL LETTER A` and `FRONT-FACING BABY CHICK` in the examples above.*

모든 21비트 유니코드 스칼라 값이 문자에 할당되는 것은 아닙니다. 일부 스칼라값은 나중에 할당하거나 UTF-16 인코딩에 사용하기 위해 예약되어있습니다. 일반적으로 문자에 할당된 스칼라 값은 위의 예에서  `LATIN SMALL LETTER A` 이나 `FRONT-FACING BABY CHICK` 같은 이름을 가집니다.



### *Extended Grapheme Clusters*

*Every instance of Swift’s `Character` type represents a single extended grapheme cluster. An extended grapheme cluster is a sequence of one or more Unicode scalars that (when combined) produce a single human-readable character.*

Swift에서 `Character`유형의 모든 인스턴스는 확장된 `Grapheme Cluster`를 나타냅니다. 확장된 `Grapheme Cluster`는 하나 이상의 유니코드 스칼라의 시퀀스로 사람이 읽을 수 있는 단일 문자를 생성합니다. 

*Here’s an example. The letter `é` can be represented as the single Unicode scalar `é` (`LATIN SMALL LETTER E WITH ACUTE`, or `U+00E9`). However, the same letter can also be represented as a pair of scalars—a standard letter `e` (`LATIN SMALL LETTER E`, or `U+0065`), followed by the `COMBINING ACUTE ACCENT` scalar (`U+0301`). The `COMBINING ACUTE ACCENT` scalar is graphically applied to the scalar that precedes it, turning an `e` into an `é` when it’s rendered by a Unicode-aware text-rendering system.*

여기 예시가 있습니다. `é` 라는 문자는 유니코드 스칼라 (`LATIN SMALL LETTER E WITH ACUTE`, 혹은 `U+00E9`)로 나타낼 수 있습니다. 그러나, 동일한 문자는  `COMBINING ACUTE ACCENT` 스칼라 (`U+0301`) 뒤에 오는 표준 문자 e (`LATIN TELETE WITH AQUIT` 또는 '`U+00E9`') 스칼라 쌍으로도 표현될 수 있습니다. `COMBINING ACUTE ACCENT` 스칼라는 유니코드 인식 텍스트 렌더링 시스템에 의해 렌더링 될 때  `e` 를 `é`로 변환하면서 그 앞에 있는 스칼라에 그래픽으로 적용됩니다. 

*In both cases, the letter `é` is represented as a single Swift `Character` value that represents an extended grapheme cluster. In the first case, the cluster contains a single scalar; in the second case, it’s a cluster of two scalars:*

두 경우 모두 문자  `é`는 확장된 그래프 클러스터를 나타내는 단일 Swift 문자 값으로 표시됩니다. 첫 번째 경우, 클러스터는 단일 스칼라 값을 포함하고 두번쨰 경우는 두 스칼라로 구성된 클러스터입니다.

```swift
let eAcute: Character = "\u{E9}"                         // é
let combinedEAcute: Character = "\u{65}\u{301}"          // e followed by ́
// eAcute is é, combinedEAcute is é
```

*Extended grapheme clusters are a flexible way to represent many complex script characters as a single `Character` value. For example, Hangul syllables from the Korean alphabet can be represented as either a precomposed or decomposed sequence. Both of these representations qualify as a single `Character` value in Swift:*

확장된 `grapheme clusters`는 많은 복잡한 스크립트 문자를 하나의 `Character` 값으로 표현할 수 있는 유연한 방법입니다. 예를 들어, 한글의 음절은 사전에 합성되거나 분해된 순서로 표현될 수 있습니다. 이 두 표현 모두 Swift에서 단일 `Character` 값으로 적합합니다.

```swift
let precomposed: Character = "\u{D55C}"                  // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"   // ᄒ, ᅡ, ᆫ
// precomposed is 한, decomposed is 한
```

*Extended grapheme clusters enable scalars for enclosing marks (such as `COMBINING ENCLOSING CIRCLE`, or `U+20DD`) to enclose other Unicode scalars as part of a single `Character` value:*

확장된 `grapheme clusters`는 마크 (`COMBINING ENCLOSING CIRCLE`,  `U+20DD` 과 같은)를 둘러싸는 스칼라가 단일 `Character` 값의 일부로 다른 유니코드 스칼라를 둘러싸도록 합니다.

```swift
let enclosedEAcute: Character = "\u{E9}\u{20DD}"
// enclosedEAcute is é⃝
```

*Unicode scalars for regional indicator symbols can be combined in pairs to make a single `Character` value, such as this combination of `REGIONAL INDICATOR SYMBOL LETTER U` (`U+1F1FA`) and `REGIONAL INDICATOR SYMBOL LETTER S` (`U+1F1F8`):*

지역 표시 기호에 대한 유니코드 스칼라를 쌍으로 결합해서  `REGIONAL INDICATOR SYMBOL LETTER U` (`U+1F1FA`) 혹은 `REGIONAL INDICATOR SYMBOL LETTER S` (`U+1F1F8`) 의 결합과 같은 하나의 `Character` 값을 만들 수 있습니다.

```swift
let regionalIndicatorForUS: Character = "\u{1F1FA}\u{1F1F8}"
// regionalIndicatorForUS is 🇺🇸
```
