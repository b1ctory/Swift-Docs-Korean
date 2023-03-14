## *Precedence and Associativity*

*Operator precedence gives some operators higher priority than others; these operators are applied first.*

*Operator associativity defines how operators of the same precedence are grouped together — either grouped from the left, or grouped from the right. Think of it as meaning “they associate with the expression to their left,” or “they associate with the expression to their right.”*

*It’s important to consider each operator’s precedence and associativity when working out the order in which a compound expression will be calculated. For example, operator precedence explains why the following expression equals `17`.*

```swift
2 + 3 % 4 * 5
// this equals 17
```

*If you read strictly from left to right, you might expect the expression to be calculated as follows:*

- *`2` plus `3` equals `5`*

- *`5` remainder `4` equals `1`*

- *`1` times `5` equals `5`*

*However, the actual answer is `17`, not `5`. Higher-precedence operators are evaluated before lower-precedence ones. In Swift, as in C, the remainder operator (`%`) and the multiplication operator (`*`) have a higher precedence than the addition operator (`+`). As a result, they’re both evaluated before the addition is considered.*

*However, remainder and multiplication have the same precedence as each other. To work out the exact evaluation order to use, you also need to consider their associativity. Remainder and multiplication both associate with the expression to their left. Think of this as adding implicit parentheses around these parts of the expression, starting from their left:*

```swift
2 + ((3 % 4) * 5)
```

*`(3 % 4)` is `3`, so this is equivalent to:*

```swift
2 + (3 * 5)
```

*`(3 * 5)` is `15`, so this is equivalent to:*

```swift
2 + 15
```

*This calculation yields the final answer of `17`.*

*For information about the operators provided by the Swift standard library, including a complete list of the operator precedence groups and associativity settings, see [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations).*

*Swift’s operator precedences and associativity rules are simpler and more predictable than those found in C and Objective-C. However, this means that they aren’t exactly the same as in C-based languages. Be careful to ensure that operator interactions still behave in the way you intend when porting existing code to Swift.*

> *Note*
> 
> *Swift’s operator precedences and associativity rules are simpler and more predictable than those found in C and Objective-C. However, this means that they aren’t exactly the same as in C-based languages. Be careful to ensure that operator interactions still behave in the way you intend when porting existing code to Swift.*


