## *Comments*

*Use comments to include nonexecutable text in your code, as a note or reminder to yourself. Comments are ignored by the Swift compiler when your code is compiled.*

*Comments in Swift are very similar to comments in C. Single-line comments begin with two forward-slashes (`//`):*

```swift
// This is a comment.
```

*Multiline comments start with a forward-slash followed by an asterisk* (`/*`) *and end with an asterisk followed by a forward-slash* (`*/`):

```swift
/* This is also a comment
   but is written over multiple lines. */
```

*Unlike multiline comments in C, multiline comments in Swift can be nested inside other multiline comments. You write nested comments by starting a multiline comment block and then starting a second multiline comment within the first block. The second block is then closed, followed by the first block:*

```swift
/* This is the start of the first multiline comment.
/* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */
```

*Nested multiline comments enable you to comment out large blocks of code quickly and easily, even if the code already contains multiline comments.*


