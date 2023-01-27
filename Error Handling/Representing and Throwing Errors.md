## *Representing and Throwing Errors : 오류를 표현하고 던지기*

*In Swift, errors are represented by values of types that conform to the `Error` protocol. This empty protocol indicates that a type can be used for error handling.*

Swift에서 오류는 `Error` 프로토콜을 준수하는 타입의 값으로 표시됩니다. 이 빈 프로토콜은 오류 처리에 타입을 사용할 수 있음을 나타냅니다.

*Swift enumerations are particularly well suited to modeling a group of related error conditions, with associated values allowing for additional information about the nature of an error to be communicated. For example, here’s how you might represent the error conditions of operating a vending machine inside a game:*

Swift의 열거형은 관련된 오류 조건 그룹을 모델링하는 데 특히 적합하며, 관련 값을 사용하면 오류의 특성에 대한 추가 정보를 전달할 수 있습니다. 예를 들어 다음은 게임 내에서 자동 판매기를 작동할 때 발생하는 오류 조건을 나타내는 방법입니다:

```swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```

*Throwing an error lets you indicate that something unexpected happened and the normal flow of execution can’t continue. You use a `throw` statement to throw an error. For example, the following code throws an error to indicate that five additional coins are needed by the vending machine:*

오류를 던지면 예기치 않은 일이 발생하여 정상적인 실행 흐름을 계속할 수 없음을 나타낼 수 있습니다. 오류를 발생시키려면 `throw` 문을 사용합니다. 예를 들어, 다음 코드는 자동판매기에 5개의 동전이 추가로 필요함을 나타내는 오류를 발생시킵니다:

```swift
throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```
