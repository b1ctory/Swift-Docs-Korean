## *Ternary Conditional Operator : 삼항 조건 연산자*

*The ternary conditional operator is a special operator with three parts, which takes the form `question ? answer1 : answer2`. It’s a shortcut for evaluating one of two expressions based on whether `question` is true or false. If `question` is true, it evaluates `answer1` and returns its value; otherwise, it evaluates `answer2` and returns its value.*

삼항 조건 연산자는 `질문 ? 대답1 : 대답2` 형식의 세 부분으로 이루어진 특수 문자입니다. 질문이 참인지 거짓인지를 기준으로 참이면 `answer1` 을 평가하여 값을 반환하고, 그렇지 않으면 `answer2`를 평가하여 값을 반환합니다.

*The ternary conditional operator is shorthand for the code below:*

삼항 조건 연산자는 아래 코드의 줄임말입니다.

```swift
if question {
    answer1
} else {
    answer2
}
```

*Here’s an example, which calculates the height for a table row. The row height should be 50 points taller than the content height if the row has a header, and 20 points taller if the row doesn’t have a header:*

다음은 테이블 행의 높이를 계산하는 예시입니다. 행의 높이는 헤더가 있는 경우 내용 높이보다 50포인트 높고, 행에 헤더가 없는 경우에는 20포인트 높아야 합니다.

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// rowHeight is equal to 90
```

*The example above is shorthand for the code below:*

위의 예시는 아래의 코드의 축약입니다.

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight: Int
if hasHeader {
    rowHeight = contentHeight + 50
} else {
    rowHeight = contentHeight + 20
}
// rowHeight is equal to 90
```

*The first example’s use of the ternary conditional operator means that `rowHeight` can be set to the correct value on a single line of code, which is more concise than the code used in the second example.*

첫 번째 예제에서 삼항 연산자를 사용한다는 것은 `rowHeight`을 코드 한 줄에 정확한  값으로 설정할 수 있다는 것을 의미하며, 이는 두번째 예제에서 사용된 코드보다 간결합니다. 

*The ternary conditional operator provides an efficient shorthand for deciding which of two expressions to consider. Use the ternary conditional operator with care, however. Its conciseness can lead to hard-to-read code if overused. Avoid combining multiple instances of the ternary conditional operator into one compound statement.*

삼항 조건 연산자는 두 표현식 중 어떤것을 고려할지 결정하기 위한 효율적인 속기를 제공ㅎ바니다. 그러나 삼항 조건 연산자를 주의해서 사용해야 합니다. 그 간결함이 과하게 사용될 경우 읽기 어려운 코드로 이어질 수 있기 때문입니다. 삼항 조건 연산자의 여러 인스턴스를 하나의 복합문으로 결합하지 않도록 합니다.
