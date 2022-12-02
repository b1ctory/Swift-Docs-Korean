## *Comments : 주석*

*Use comments to include nonexecutable text in your code, as a note or reminder to yourself. Comments are ignored by the Swift compiler when your code is compiled.*

메모나 주의사항 등의 코드에서 실행되지 않는 코드를 포함하려면 주석을 사용하세요. 컴파일될 때 Swift 컴파일러는 주석을 무시합니다.

*Comments in Swift are very similar to comments in C. Single-line comments begin with two forward-slashes (`//`):*

Swift에서의 주석은 C언어에서의 주석과 비슷합니다. 한 줄 주석은 두개의 슬래쉬 // 로 시작합니다.

```swift
// This is a comment.
```

*Multiline comments start with a forward-slash followed by an asterisk* (`/*`) *and end with an asterisk followed by a forward-slash* (`*/`):

여러줄의 주석은/* 로 시작해서 */ 로 끝납니다.

```swift
/* This is also a comment
   but is written over multiple lines. */
```

*Unlike multiline comments in C, multiline comments in Swift can be nested inside other multiline comments. You write nested comments by starting a multiline comment block and then starting a second multiline comment within the first block. The second block is then closed, followed by the first block:*

C언어에서의 여러 줄 주석과 달리, Swift의 여러 줄 주석은 다른 여러줄 주석 안에 중첩될 수 있습니다. 여러줄 주석을 시작한 다음 첫번째 블록 내에서 두번째 여러줄 주석을 시작해서 중첩 주석을 작성합니다. 그런 다음 두번째 블록이 닫히고 첫번째 블록이 이어집니다.

```swift
/* This is the start of the first multiline comment.
/* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */
```

*Nested multiline comments enable you to comment out large blocks of code quickly and easily, even if the code already contains multiline comments.*

중첩된 여러줄 주석을 사용하면 코드에 이미 여러줄 주석이 포함되어 있더라도 코드의 큰 블록을 빠르고 쉽게 주석처리할 수 있습니다.
