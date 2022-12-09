## *String Literals*

*You can include predefined `String` values within your code as string literals. A string literal is a sequence of characters surrounded by double quotation marks (`"`).*

*Use a string literal as an initial value for a constant or variable:*

```swift
let someString = "Some string literal value
```

*Note that Swift infers a type of `String` for the `someString` constant because it’s initialized with a string literal value.*

### *Multiline String Literals*

*If you need a string that spans several lines, use a multiline string literal—a sequence of characters surrounded by three double quotation marks:*

```swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

*A multiline string literal includes all of the lines between its opening and closing quotation marks. The string begins on the first line after the opening quotation marks (`"""`) and ends on the line before the closing quotation marks, which means that neither of the strings below start or end with a line break:*

```swift
let singleLineString = "These are the same."
let multilineString = """
These are the same.
"""
```

*When your source code includes a line break inside of a multiline string literal, that line break also appears in the string’s value. If you want to use line breaks to make your source code easier to read, but you don’t want the line breaks to be part of the string’s value, write a backslash (`\`) at the end of those lines:*

```swift
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

*To make a multiline string literal that begins or ends with a line feed, write a blank line as the first or last line. For example:*

```swift
let lineBreaks = """

This string starts with a line break.
It also ends with a line break.

"""
```

*A multiline string can be indented to match the surrounding code. The whitespace before the closing quotation marks (`"""`) tells Swift what whitespace to ignore before all of the other lines. However, if you write whitespace at the beginning of a line in addition to what’s before the closing quotation marks, that whitespace is included.*

![](https://docs.swift.org/swift-book/_images/multilineStringWhitespace_2x.png)

*In the example above, even though the entire multiline string literal is indented, the first and last lines in the string don’t begin with any whitespace. The middle line has more indentation than the closing quotation marks, so it starts with that extra four-space indentation.*

### *Special Characters in String Literals*

*String literals can include the following special characters:*

- *The escaped special characters `\0` (null character), `\\` (backslash), `\t` (horizontal tab), `\n` (line feed), `\r` (carriage return), `\"` (double quotation mark) and `\'` (single quotation mark)*

- *An arbitrary Unicode scalar value, written as `\u{`n`}`, where n is a 1–8 digit hexadecimal number (Unicode is discussed in [Unicode](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html#ID293) below)*

*The code below shows four examples of these special characters. The `wiseWords` constant contains two escaped double quotation marks. The `dollarSign`, `blackHeart`, and `sparklingHeart` constants demonstrate the Unicode scalar format:*

```swift
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
```

*Because multiline string literals use three double quotation marks instead of just one, you can include a double quotation mark (`"`) inside of a multiline string literal without escaping it. To include the text `"""` in a multiline string, escape at least one of the quotation marks. For example:*

```swift
let threeDoubleQuotationMarks = """
Escaping the first quotation mark \"""
Escaping all three quotation marks \"\"\"
"""
```

### *Extended String Delimiters*

*You can place a string literal within extended delimiters to include special characters in a string without invoking their effect. You place your string within quotation marks (`"`) and surround that with number signs (`#`). For example, printing the string literal `#"Line 1\nLine 2"#` prints the line feed escape sequence (`\n`) rather than printing the string across two lines.*

*If you need the special effects of a character in a string literal, match the number of number signs within the string following the escape character (`\`). For example, if your string is `#"Line 1\nLine 2"#` and you want to break the line, you can use `#"Line 1\#nLine 2"#` instead. Similarly, `###"Line1\###nLine2"###` also breaks the line.*

*String literals created using extended delimiters can also be multiline string literals. You can use extended delimiters to include the text `"""` in a multiline string, overriding the default behavior that ends the literal. For example:*

```swift
let threeMoreDoubleQuotationMarks = #"""
Here are three more double quotes: """
"""#
```


