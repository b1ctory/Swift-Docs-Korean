## *String Literals*

*You can include predefined `String` values within your code as string literals. A string literal is a sequence of characters surrounded by double quotation marks (`"`).*

코드 내에 미리 정의된 `String` 값을 문자열 리터럴로 포함할 수 있습니다. 문자열 리터럴은 큰 따옴표 (`"`)로 둘러쌓인 일련의 문자입니다.

*Use a string literal as an initial value for a constant or variable:*

상수 또는 변수의 초기값으로 문자열 리터럴을 사용 :

```swift
let someString = "Some string literal value"
```

*Note that Swift infers a type of `String` for the `someString` constant because it’s initialized with a string literal value.*

Swift는 문자열 리터럴 값으로 초기화되기 때문에 `someString` 상수에 대해 문자열 유형을 유추합니다. 

### *Multiline String Literals*

*If you need a string that spans several lines, use a multiline string literal—a sequence of characters surrounded by three double quotation marks:*

여러줄에 걸쳐있는 문자열이 필요한 경우 다중행 문자열 리터럴 - 세 개의 큰 따옴표로 둘러싸인 문자 시퀀스 - 를 사용합니다.

```swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

*A multiline string literal includes all of the lines between its opening and closing quotation marks. The string begins on the first line after the opening quotation marks (`"""`) and ends on the line before the closing quotation marks, which means that neither of the strings below start or end with a line break:*

다중행 문자열 리터럴에는 여는 따옴표와 닫는 따옴표 사이의 모든 줄이 포함됩니다. 문자열은 따옴표(`"""`) 뒤의 첫번째 줄에서 시작하여 따옴표 앞의 줄에서 끝납니다. 이는 아래 문자열 중 어느 것도 줄바꿈으로 시작하거나 끝나지 않음을 의미합니다. 

```swift
let singleLineString = "These are the same."
let multilineString = """
These are the same.
"""
```

*When your source code includes a line break inside of a multiline string literal, that line break also appears in the string’s value. If you want to use line breaks to make your source code easier to read, but you don’t want the line breaks to be part of the string’s value, write a backslash (`\`) at the end of those lines:*

소스코드가 다중행 문자열 리터럴 내부에 줄 바꿈을 포함하는 경우 해당 줄 바꿈도 문자열 값에 나타납니다. 줄 바꿈을 사용해서 소스코드를 읽기 쉽게 만들지만 줄 바꿈이 문자열 값의 일부가 되지 않으려면 줄 바꿈의 끝에 백슬래시 (`\`)를 사용하세요.

```swift
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

*To make a multiline string literal that begins or ends with a line feed, write a blank line as the first or last line. For example:*

라인 피드로 시작하거나 끝나는 다중행 리터럴을 만들려면 빈 줄을 첫번째 줄 혹은 마지막 줄로 작성합니다. 예를 들어 : 

```swift
let lineBreaks = """

This string starts with a line break.
It also ends with a line break.

"""
```

*A multiline string can be indented to match the surrounding code. The whitespace before the closing quotation marks (`"""`) tells Swift what whitespace to ignore before all of the other lines. However, if you write whitespace at the beginning of a line in addition to what’s before the closing quotation marks, that whitespace is included.*

다중행 문자열은 주변 코드와 일치하도록 들여쓸 수 있습니다. 닫는 따옴표(`"""`) 앞의 공백은 Swift에게 다른 모든 줄 앞의 공백을 알려줍니다. 그러나, 닫는 따옴표 앞에 추가로 줄의 시작 부분에 공백을 쓰면 해당 공백이 포함됩니다.



![](https://docs.swift.org/swift-book/_images/multilineStringWhitespace_2x.png)

*In the example above, even though the entire multiline string literal is indented, the first and last lines in the string don’t begin with any whitespace. The middle line has more indentation than the closing quotation marks, so it starts with that extra four-space indentation.*

위의 예제에서, 전체 다중 행 문자열 리터럴이 들여쓰기 되더라도, 문자열의 첫번째와 마지막 행은 공백으로 시작하지 않습니다. 가운데 선은 닫는 따옴표보다 들여쓰기가 더 많기 때문에 추가적인 4개의 공백을 들여쓰기로 시작합니다. 

### *Special Characters in String Literals : 문자열 리터럴의 특수문자*

*String literals can include the following special characters:*

문자열에는 다음과 같은 특수 문자가 포함될 수 있습니다. 

- *The escaped special characters `\0` (null character), `\\` (backslash), `\t` (horizontal tab), `\n` (line feed), `\r` (carriage return), `\"` (double quotation mark) and `\'` (single quotation mark)*
  
  탈출된 특수 문자 `\0` (null 문자), `\\` (백슬래시), `\t` (수평 탭), `\n` (라인 피드), `\r` (캐리지 리턴), `\"` (큰 따옴표) and `\'` (작은 따옴표)

- *An arbitrary Unicode scalar value, written as `\u{`n`}`, where n is a 1–8 digit hexadecimal number (Unicode is discussed in [Unicode](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html#ID293) below)*
  
  `\u{`n`}` (n은 1 ~8 자리 16진수) 로 작성된 임의의 유니코드 스칼라 값입니다. (유니코드는 아래 [링크] 에서 설명합니다.)

*The code below shows four examples of these special characters. The `wiseWords` constant contains two escaped double quotation marks. The `dollarSign`, `blackHeart`, and `sparklingHeart` constants demonstrate the Unicode scalar format:*

아래의 코드는 이러한 특수 문자의 네가지 예시를 보여줍니다. wiseWords 상수에는 두개의 탈출된 (?) 큰따옴표가 포함되어 있습니다.  `dollarSign`, `blackHeart`, 그리고 `sparklingHeart` 유니코드 스칼라 형식을 보여줍니다.

```swift
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
```

*Because multiline string literals use three double quotation marks instead of just one, you can include a double quotation mark (`"`) inside of a multiline string literal without escaping it. To include the text `"""` in a multiline string, escape at least one of the quotation marks. For example:*

다중행 문자열 리터럴은 하나가 아니라 세 개의 큰 따옴표를 사용하기 때문에 다중행 문자열 리터럴 내부에 큰따옴표(`"`)를 포함할 수 있습니다. 텍스트 `"""`를 여러 줄 문자열에 포함하려면 따옴표 중 하나 이상을 탈출하세요. 예를 들면 :

```swift
let threeDoubleQuotationMarks = """
Escaping the first quotation mark \"""
Escaping all three quotation marks \"\"\"
"""
```

### *Extended String Delimiters : 확장 문자열 구분 기호*

*You can place a string literal within extended delimiters to include special characters in a string without invoking their effect. You place your string within quotation marks (`"`) and surround that with number signs (`#`). For example, printing the string literal `#"Line 1\nLine 2"#` prints the line feed escape sequence (`\n`) rather than printing the string across two lines.*

효과를 호출하지 않고 문자열에 특수 문자를 포함하도록 확장된 구분 기호 내에 문자열 리터럴을 배치할 수 있습니다. 따옴표(`"`) 안에 문자열을 넣고 숫자 기호(`#`)으로 둘러쌉니다. 예를 들어 문자열 리터럴 `#"Line 1\nLine 2"#`을 인쇄하면 두 줄에 걸쳐서 문자열을 인쇄하는 대신 라인 피드 이스케이프 시퀀스 (`\n`) 가 인쇄됩니다. 

*If you need the special effects of a character in a string literal, match the number of number signs within the string following the escape character (`\`). For example, if your string is `#"Line 1\nLine 2"#` and you want to break the line, you can use `#"Line 1\nLine 2"#`instead. Similarly, `###"Line1\###nLine2"###` also breaks the line.*

문자열 리터럴에서 문자의 특수 효과가 필요한 경우 이스케이프 문자(`\n`) 뒤에 오는 문자열 내 숫자 기호의 수를 일치시키세요. 예를 들어  `#"Line 1\nLine 2"#`인 경우 줄을 끊으려면  `#"Line 1\nLine 2"#`를 대신 사용할 수 있습니다. 마찬가지로  `###"Line1\###nLine2"###` 또한 줄을 그어버립니다. 

*String literals created using extended delimiters can also be multiline string literals. You can use extended delimiters to include the text `"""` in a multiline string, overriding the default behavior that ends the literal. For example:*

확장 구분 기호를 사용해서 만든 문자열 리터럴은 아래 줄의 여러 줄 문자열 리터럴일 수도 있습니다. 확장 구분 기호를 사용해서 텍스트 `"""` 를 다중 행 문자열에 포함해서 리터럴을 끝내는 기본 동작을 재정의할 수 있습니다. 예를 들어 : 

```swift
let threeMoreDoubleQuotationMarks = #"""
Here are three more double quotes: """
"""#
```
