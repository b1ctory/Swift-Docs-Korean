## *Working with Characters*

*You can access the individual `Character` values for a `String` by iterating over the string with a `for`-`in` loop:*

`for-in` 루프가 있는 문자열 위에서 반복해서 `String`에 대한 개별 `Character` 값에 엑세스할 수 있습니다.

```swift
for character in "Dog!🐶" {
    print(character)
}
// D
// o
// g
// !
// 🐶
```

*The `for`-`in` loop is described in [For-In Loops](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID121).*

for-in 루프는 [링크]에 설명되어있습니다. 

*Alternatively, you can create a stand-alone `Character` constant or variable from a single-character string literal by providing a `Character` type annotation:*

대신에, Character 타입 어노테이션을 제공해서 단일 문자열 리터럴에서 독립 실행형 Character 상수 혹은 변수를 만들 수 있습니다. 

```swift
let exclamationMark: Character = "!"
```

*`String` values can be constructed by passing an array of `Character` values as an argument to its initializer:*

`String` 값은 `Character` 값의 배열을 인수로 이니셜라이저에 전달해서 구성할 수 있습니다. 

```swift
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱"
```
