## *Specifying Cleanup Actions : 정리 작업 지정*

*You use a `defer` statement to execute a set of statements just before code execution leaves the current block of code. This statement lets you do any necessary cleanup that should be performed regardless of how execution leaves the current block of code—whether it leaves because an error was thrown or because of a statement such as `return` or `break`. For example, you can use a `defer` statement to ensure that file descriptors are closed and manually allocated memory is freed.*

`defer` 문을 사용하여 코드 실행이 현재 코드 블록을 떠나기 직전에 일련의 구문을 실행합니다. 이 명령문을 사용하면 실행이 현재 코드 블록을 벗어나는 방식(오류 발생으로 인해 떠나든, `return` 또는 `break`과 같은 구문으로 인해 떠나든)에 관계없이 수행해야만 하는 필요 정리 작업을 수행할 수 있습니다. 예를 들어 `defer` 문을 사용하여 파일 설명자가 닫히고 수동으로 할당된 메모리가 해제되도록 할 수 있습니다.

*A `defer` statement defers execution until the current scope is exited. This statement consists of the `defer` keyword and the statements to be executed later. The deferred statements may not contain any code that would transfer control out of the statements, such as a `break` or a `return` statement, or by throwing an error. Deferred actions are executed in the reverse of the order that they’re written in your source code. That is, the code in the first `defer` statement executes last, the code in the second `defer` statement executes second to last, and so on. The last `defer` statement in source code order executes first.*

`defer` 문은 현재 범위가 종료될 때까지 실행을 연기합니다. 이 문은 `defer` 키워드와 나중에 실행할 문으로 구성됩니다. 지연된 구문에는 `break` 또는 `return` 문과 같이 구문 밖으로 제어를 이전하거나 오류를 발생시키는 코드가 포함되지 않을 것입니다. 지연된 작업은 소스 코드에 작성된 순서와 반대로 실행됩니다. 즉, 첫 번째 `defer` 문의 코드가 마지막으로 실행되고 두 번째 `defer` 문의 코드가 마지막에서 두 번째로 실행되는 식입니다. 소스 코드 순서의 마지막 `defer` 문이 먼저 실행됩니다.

```swift
func processFile(filename: String) throws {
    if exists(filename) {
        let file = open(filename)
        defer {
            close(file)
        }
        while let line = try file.readline() {
            // Work with the file.
        }
        // close(file) is called here, at the end of the scope.
    }
}
```

*The above example uses a `defer` statement to ensure that the `open(_:)` function has a corresponding call to `close(_:)`.*

위의 예에서는 `defer` 문을 사용하여 `open(_:)` 함수가 `close(_:)`에 해당하는 호출을 갖는것을 보장합니다.

> *NOTE*
> 
> *You can use a `defer` statement even when no error handling code is involved.*
> 
> 오류 처리 코드가 관련되지 않은 경우에도  `defer`문을 사용할 수 있습니다.


