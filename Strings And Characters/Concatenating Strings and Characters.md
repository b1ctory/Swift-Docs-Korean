## *Concatenating Strings and Characters : 문자열과 문자 결합*

`String` values can be added together (or *concatenated*) with the addition operator (`+`) to create a new `String` value:

String 값을 추가 연산자 (`+`) 와 함께 추가 (혹은 연결)해서 새 String 값을 만들 수 있습니다.  

```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome now equals "hello there"
```

*You can also append a `String` value to an existing `String` variable with the addition assignment operator (`+=`):*

추가 할당 연산자(`+=`)를 사용해서 기존의 String 변수에 String 값을 추가할 수도 있습니다.

```swift
var instruction = "look over"
instruction += string2
// instruction now equals "look over there"
```

*You can append a `Character` value to a `String` variable with the `String` type’s `append()` method:*

문자열 타입의 append() 메서드를 사용해서 문자 값을 String 변수에 추가할 수 있습니다.

```swift
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome now equals "hello there!"
```

> *NOTE*
> 
> *You can’t append a `String` or `Character` to an existing `Character` variable, because a `Character` value must contain a single character only.*
> 
> 문자 값은 단일 문자만 포함해야하므로 기존 문자 변수에 문자열 혹은 문자를 추가할 수 없습니다.

*If you’re using multiline string literals to build up the lines of a longer string, you want every line in the string to end with a line break, including the last line. For example:*

여러줄 문자열 리터럴을 사용해서 더 긴 문자열의 줄을 작성하는 경우 마지막 줄을 포함해서 문자열의 모든 줄이 줄바꿈으로 끝나도록 합니다. 

```swift
let badStart = """
one
two
"""
let end = """
three
"""
print(badStart + end)
// Prints two lines:
// one
// twothree

let goodStart = """
one
two

"""
print(goodStart + end)
// Prints three lines:
// one
// two
// three
```

*In the code above, concatenating `badStart` with `end` produces a two-line string, which isn’t the desired result. Because the last line of `badStart` doesn’t end with a line break, that line gets combined with the first line of `end`. In contrast, both lines of `goodStart` end with a line break, so when it’s combined with `end` the result has three lines, as expected.*

위의 코드에서 `badStart` 를 end와 연결하면 두 줄의 문자열이 생기는데, 이는 원하는 결과가 아닙니다. `badStart`의 마지막은 줄바꿈으로 끝나지 않기 때문에 그 줄은 `end`의 첫 줄과 합쳐집니다. 반면 `goodStart`의 두 줄은 모두 줄바꿈으로 끝나므로 `end`와 결합하면 예상대로 세 줄이 됩니다.


