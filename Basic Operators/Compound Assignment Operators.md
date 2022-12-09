## *Compound Assignment Operators : 복합 할당 연산자*

*Like C, Swift provides compound assignment operators that combine assignment (`=`) with another operation. One example is the addition assignment operator (`+=`):*

C와 마찬가지로, Swift는 할당(`=`)을 다른 연산자와 결합하는 복합 할당 연산자를 제공합니다. 한가지 예는 덧셈 할당 연산자 (`+=`) 입니다.

```swift
var a = 1
a += 2
// a is now equal to 3
```

*The expression `a += 2` is shorthand for `a = a + 2`. Effectively, the addition and the assignment are combined into one operator that performs both tasks at the same time.*

표현식 `a += 2` 은 `a = a + 2`의 줄임말입니다. 효과적으로,추가와 할당은 두 작업을 동시에 수행하는 하나의 연산자로 결합됩니다.

> *NOTE*
> 
> *The compound assignment operators don’t return a value. For example, you can’t write `let b = a += 2`.*
> 
> 복합 할당 연산자는 값을 리턴하지 않습니다. 예를 들어, `let b = a += 2` 와 같이 쓸 수 없습니다.

*For information about the operators provided by the Swift standard library, see [Operator Declarations](https://developer.apple.com/documentation/swift/operator_declarations).*

Swift 표준 라이브러리에서 제공하는 연산자에 대한 자세한 내용은 [링크]를 참조하세요.


