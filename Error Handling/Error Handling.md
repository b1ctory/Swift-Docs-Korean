# *Error Handling: 오류처리*

*Error handling is the process of responding to and recovering from error conditions in your program. Swift provides first-class support for throwing, catching, propagating, and manipulating recoverable errors at runtime.*

오류 처리는 프로그램의 오류 상태에 대응하고 복구하는 프로세스입니다. Swift는 런타임에 복구 가능한 오류를 던지고, 잡고, 전파하고, 조작할 수 있는 최고 수준의 지원을 제공합니다.

*Some operations aren’t guaranteed to always complete execution or produce a useful output. Optionals are used to represent the absence of a value, but when an operation fails, it’s often useful to understand what caused the failure, so that your code can respond accordingly.*

일부 작업에서는 항상 실행을 완료하거나 유용한 결과물을 제공하지는 않습니다. 옵셔널은 값이 없음을 나타내는 데 사용되지만 작업이 실패할 경우 코드가 그에 따라 응답할 수 있도록 실패의 원인을 이해하는 것이 유용합니다.

*As an example, consider the task of reading and processing data from a file on disk. There are a number of ways this task can fail, including the file not existing at the specified path, the file not having read permissions, or the file not being encoded in a compatible format. Distinguishing among these different situations allows a program to resolve some errors and to communicate to the user any errors it can’t resolve.*

예를 들어 디스크의 파일에서 데이터를 읽고 처리하는 작업을 생각해 보십시오. 이 작업은 지정된 경로에 존재하지 않는 파일, 읽기 권한이 없는 파일, 호환되는 형식으로 인코딩되지 않은 파일 등 여러 가지 방법으로 실패할 수 있습니다. 이러한 여러 상황을 구분하면 프로그램에서 일부 오류를 해결하고 해결할 수 없는 오류를 사용자에게 전달할 수 있습니다.

> *NOTE*
> 
> *Error handling in Swift interoperates with error handling patterns that use the `NSError` class in Cocoa and Objective-C. For more information about this class, see [Handling Cocoa Errors in Swift](https://developer.apple.com/documentation/swift/cocoa_design_patterns/handling_cocoa_errors_in_swift).*
> 
> Swift의 오류 처리는 Cocoa 및 Objective-C의 `NSError` 클래스를 사용하는 오류 처리 패턴과 상호 운용됩니다. 이 클래스에 대한 자세한 내용은 [링크]를 참조하십시오.
