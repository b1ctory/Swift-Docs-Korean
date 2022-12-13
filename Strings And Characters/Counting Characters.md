## *Counting Characters : 문자수 계산*

*To retrieve a count of the `Character` values in a string, use the `count` property of the string:*

문자열의 `Character` 값 개수를 검색하려면 문자열의 `count` 속성을 사용합니다.

```swift
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("unusualMenagerie has \(unusualMenagerie.count) characters")
// Prints "unusualMenagerie has 40 characters"
```

*Note that Swift’s use of extended grapheme clusters for `Character` values means that string concatenation and modification may not always affect a string’s character count.*

스위프트가 `Character` 값을 위해 확장된 `grapheme clusters` 를 사용한다는 것은 문자열 연결 및 수정이 문자열의 문자 수에 항상 영향을 미치는 것은 아니라는 것을 의미합니다.

*For example, if you initialize a new string with the four-character word `cafe`, and then append a `COMBINING ACUTE ACCENT` (`U+0301`) to the end of the string, the resulting string will still have a character count of `4`, with a fourth character of `é`, not `e`:*

예를 들어, 네 글자로 된 단어 `cafe`로 새 문자열을 초기화한 다음  `COMBINING ACUTE ACCENT` (`U+0301`) 를 추가함하면, 결과 문자열의 문자 수는 4로 유지되며, 네번째 문자는 `e`가 아닌 `é` 입니다.

```swift
var word = "cafe"
print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in cafe is 4"

word += "\u{301}"    // COMBINING ACUTE ACCENT, U+0301

print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in café is 4"
```

> *NOTE*
> 
> *Extended grapheme clusters can be composed of multiple Unicode scalars. This means that different characters—and different representations of the same character—can require different amounts of memory to store. Because of this, characters in Swift don’t each take up the same amount of memory within a string’s representation. As a result, the number of characters in a string can’t be calculated without iterating through the string to determine its extended grapheme cluster boundaries. If you are working with particularly long string values, be aware that the `count` property must iterate over the Unicode scalars in the entire string in order to determine the characters for that string.*
> 
> 확장된 grapheme clusters는 여러 유니코드 스칼라로 구성될 수 있습니다. 즉, 다른 문자와 동일한 문자의 다른 표현은 저장할 메모리의 양이 다를 수 있습니다. 이 때문에 Swift의 문자는 문자열 표현 내에서 각각 동일한 양의 메모리를 차지하지 않습니다. 따라서 문자열의 문자 수는 확장된 grapheme clusters 경계를 결정하기 위해 문자열을 반복하지 않고는 계산할 수 없습니다. 특히 긴 문자열 값을 사용하는 경우 해당 문자열의 문자를 결정하려면 전체 문자열의 유니코드 스칼라에 대해 `count` 속성이 반복되어야 한다는 점에 유의하세요.
> 
> *The count of the characters returned by the `count` property isn’t always the same as the `length` property of an `NSString` that contains the same characters. The length of an `NSString` is based on the number of 16-bit code units within the string’s UTF-16 representation and not the number of Unicode extended grapheme clusters within the string.*
> 
> `count` 속성에서 반환되는 문자의 개수가 항상 같은 문자를 포함하는 `NSString`의 `length` 속성과 같지는 않습니다. `NSString`의 길이는 문자열 내의 유니코드 확장 grapheme clusters의 수가 아니라 문자열의 UTF-16 표현 내의 16 비트 코드 단위의 수에 기초합니다.


