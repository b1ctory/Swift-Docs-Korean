## *Assertions and Preconditions*

*Assertions and preconditions are checks that happen at runtime. You use them to make sure an essential condition is satisfied before executing any further code. If the Boolean condition in the assertion or precondition evaluates to `true`, code execution continues as usual. If the condition evaluates to `false`, the current state of the program is invalid; code execution ends, and your app is terminated.*

Assertion과 전제조건은 런타임 시에 수행되는 검사입니다. 추가 코드를 실행하기 전에 필수 조건에 충족되는지 확인하기 위해 사용합니다. Assertion에서의 Bool 값이나 전제조건이 true로 파악되면, 코드 실행은 평소와 같이 실행됩니다. 만약 조건이 false로 평가되면 프로그램의 현재 상태가 유효하지 않습니다 : 코드 실행이 종료되고 앱이 종료됩니다.



*You use assertions and preconditions to express the assumptions you make and the expectations you have while coding, so you can include them as part of your code. Assertions help you find mistakes and incorrect assumptions during development, and preconditions help you detect issues in production.*

당신이 코드를 작성하는 동안 당신이 하는 가정과 기대를 표현하기 위해 전제조건을 사용함으로써 코드의 일부에 포함할 수 있습니다. Assertion은 개발 중에 실수와 잘못된 가정을 찾는데 도움이 되며 전제조건은 생산 단계에서의 이슈를 감지하는데 도움이 됩니다. 



*In addition to verifying your expectations at runtime, assertions and preconditions also become a useful form of documentation within the code. Unlike the error conditions discussed in [Error Handling](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID515) above, assertions and preconditions aren’t used for recoverable or expected errors. Because a failed assertion or precondition indicates an invalid program state, there’s no way to catch a failed assertion.*

실행 시 기대사항을 확인하는 것 이외에도 Assertion 및 전제조건은 코드 내에서 유용한 문서 형태가 됩니다. [링크]에서 설명한 오류 조건과 달리 복구 가능하거나 예상되는 오류에는 Assertion 및 전제조건이 사용되지 않습니다. 실패한 Assertion 혹은 전제조건은 잘못된 프로그램을 상태를 나타내기 때문에 실패한 Assertion을 잡아낼 방법이 없습니다. 



*Using assertions and preconditions isn’t a substitute for designing your code in such a way that invalid conditions are unlikely to arise. However, using them to enforce valid data and state causes your app to terminate more predictably if an invalid state occurs, and helps make the problem easier to debug. Stopping execution as soon as an invalid state is detected also helps limit the damage caused by that invalid state.*

Assertion과 전제조건을 사용하는 것은 잘못된 조건이 발생할 가능성이 낮은 방식으로 코드를 설계하는 것을 대체할 수 없습니다. 그러나 유용한 데이터와 상테를 적용하기 위해 이를 사용하면 잘못된 상태가 발생할 경우 앱이 더욱 예측가능하게 종료되고 문제를 더욱 쉽게 디버깅할 수 있습니다. 잘못된 상태가 감지되는 즉시 실행을 중지하는 것도 해당 잘못된 상태로 인한 손해를 제한하는데 도움이 됩니다.



*The difference between assertions and preconditions is in when they’re checked: Assertions are checked only in debug builds, but preconditions are checked in both debug and production builds. In production builds, the condition inside an assertion isn’t evaluated. This means you can use as many assertions as you want during your development process, without impacting performance in production.*

Assersion과 전제조건의 차이점은 다음과 같습니다. : Assertion은 디버그 빌드시에만 검사되지만 사전조건은 디버그와 생산 빌드 모두에서 검사됩니다. 즉, 개발 프로세스 중에 생산 성능에 영향을 미치지 않고 원하는 만큼의 assertions를 사용할 수 있습니다.



### *Debugging with Assertions*

*You write an assertion by calling the [`assert(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1541112-assert) function from the Swift standard library. You pass this function an expression that evaluates to `true` or `false` and a message to display if the result of the condition is `false`. For example:*

Swift 표준 라이브러리에서  [`assert(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1541112-assert) 함수를 호출해서 Assertion을 작성합니다. 이 함수르 true 혹은 false로 평가하는 표현식과 조건의 결과가 false인 경우 표시할 메세지를 전달합니다. 예를 들면 : 

```swift
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// This assertion fails because -3 isn't >= 0.
```

*In this example, code execution continues if `age >= 0` evaluates to `true`, that is, if the value of `age` is nonnegative. If the value of `age` is negative, as in the code above, then `age >= 0` evaluates to `false`, and the assertion fails, terminating the application.*

이 예시에서 age >= 0 이 true로 평가되면, 즉 'age' 값이 음수가 아닌 경우 코드의 실행이 계속됩니다. 만약 위읰 ㅗ드에서와 같이 age 값이 음수이면 age >= 0 은 false로 평가되고 Assertion이 실패하여 으용 프로그램이 종료됩니다.

*You can omit the assertion message—for example, when it would just repeat the condition as prose.*

예를 들어 조건을 산문으로 반복하는 경우와 같이 Assertion 메세지를 생략할 수 있습니다. 

```swift
assert(age >= 0)
```

*If the code already checks the condition, you use the [`assertionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539616-assertionfailure) function to indicate that an assertion has failed. For example:*

만약 코드가 이미 조건을 확인했다면,  `assertionFailure(_:file:line:)` 메소드를 사용해서 Assertion이 실패했음을 나타냅니다. 예를 들면 :  

```swift
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age >= 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}
```

### *Enforcing Preconditions : 사전 조건 시행*

*Use a precondition whenever a condition has the potential to be false, but must definitely be true for your code to continue execution. For example, use a precondition to check that a subscript isn’t out of bounds, or to check that a function has been passed a valid value.*

조건이 거짓일 수도 있지만 코드가 계속 실행되려면 반드시 참이어야 합니다. 에를 들어, 사전 조건을 사용해서 subscript (아래첨자 (?))가 한계 범위를 벗어났는지 확인하거나 함수가 유효한 값을 전달했는지 확인합니다. 



*You write a precondition by calling the [`precondition(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1540960-precondition) function. You pass this function an expression that evaluates to `true` or `false` and a message to display if the result of the condition is `false`. For example:*

[`precondition(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1540960-precondition) 메소드를 호출해서 전제 조건을 작성합니다. 이 함수를 true 혹은 false로 평가하는 표현식과 조건의 결과가 false인 경우 표시할 메세지를 전달합니다. 예를 들어 : 



```swift
// In the implementation of a subscript...
precondition(index > 0, "Index must be greater than zero.")
```

*You can also call the [`preconditionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539374-preconditionfailure) function to indicate that a failure has occurred—for example, if the default case of a switch was taken, but all valid input data should have been handled by one of the switch’s other cases.*

 [`preconditionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539374-preconditionfailure) 함수를 호출해서 장애가 발생했음을 나타낼 수도 있습니다. 예를 들어, 스위치문의 기본 사례를 사용했지만 모든 유효한 입력 데이터가 스위치문의 다른 사례 중 하나에 의해 처리되어야 하는 경우입니다.

> *NOTE*
> 
> *If you compile in unchecked mode (`-Ounchecked`), preconditions aren’t checked. The compiler assumes that preconditions are always true, and it optimizes your code accordingly. However, the `fatalError(_:file:line:)` function always halts execution, regardless of optimization settings.*
> 
> 선택되지 않은 모드 (`-Ounchecked`)로 컴파일하면 사전 조건이 확인되지 않습니다. 컴파일러는 전제 조건이 항상 참이라고 가정하고 그에 따라 코드를 최적화합니다. 그러나 `fatalError(_:file:line:)` 함수는 최적화 설정에 관계 없이 항상 실행을 중지합니다. 
> 
> *You can use the `fatalError(_:file:line:)` function during prototyping and early development to create stubs for functionality that hasn’t been implemented yet, by writing `fatalError("Unimplemented")` as the stub implementation. Because fatal errors are never optimized out, unlike assertions or preconditions, you can be sure that execution always halts if it encounters a stub implementation.*
> 
> 프로토타이핑과 초기 개발 시 `fatalError(_:file:line:)` 함수를 사용해서 아직 구현되지 않은 기능에 대한 stub 을 만들 수 있고 stub 구현으로 `fatalError("Unimplemented")` 를 작성합니다. 치명적인 오류는 Assertion이나 전제 조건과 달리 최적화되지 않기 때문에 stub 구현이 발생할 경우 실행이 항상 중단된다는 것을 알 수 있습니다. 


