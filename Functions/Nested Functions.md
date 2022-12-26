## *Nested Functions : 중첩 함수*

*All of the functions you have encountered so far in this chapter have been examples of global functions, which are defined at a global scope. You can also define functions inside the bodies of other functions, known as nested functions.*

이 장에서 지금까지 경험한 모든 함수는 전역 범위에서 정의된 전역 함수의 예입니다. 중첩 함수라고 하는 다른 함수의 본문 내부에 함수를 정의할 수도 있습니다.

*Nested functions are hidden from the outside world by default, but can still be called and used by their enclosing function. An enclosing function can also return one of its nested functions to allow the nested function to be used in another scope.*

중첩 함수는 기본적으로 외부로부터 숨겨지지만, 그 둘러싸는 함수를 통해 호출 및 사용할 수 있습니다. 둘러싸는 함수는 중첩 함수 중 하나를 반환해서 중첩 함수를 다른 범위에서 사용할 수도 있습니다.

*You can rewrite the `chooseStepFunction(backward:)` example above to use and return nested functions:*

위의 `chooseStepFunction(backward:)` 예제를 다시 작성하여 중첩함수를 사용하고 반환할 수도 있습니다.

```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backward ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```
