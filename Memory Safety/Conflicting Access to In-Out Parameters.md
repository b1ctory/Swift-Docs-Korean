## *Conflicting Access to In-Out Parameters : In-Out 매개 변수에 대한 액세스 충돌*

*A function has long-term write access to all of its in-out parameters. The write access for an in-out parameter starts after all of the non-in-out parameters have been evaluated and lasts for the entire duration of that function call. If there are multiple in-out parameters, the write accesses start in the same order as the parameters appear.*

함수는 모든 입력 매개 변수에 대한 장기 쓰기 액세스 권한을 가집니다. in-out 매개 변수에 대한 쓰기 액세스는 모든 non-in-out 매개 변수가 평가된 후 시작되며 해당 함수 호출의 전체 기간 동안 지속됩니다. 입력 매개 변수가 여러 개인 경우 쓰기 액세스는 매개 변수가 나타나는 순서와 동일한 순서로 시작됩니다.

*One consequence of this long-term write access is that you can’t access the original variable that was passed as in-out, even if scoping rules and access control would otherwise permit it — any access to the original creates a conflict. For example:*

이 장기 쓰기 액세스의 한 가지 결과는 범위 지정 규칙과 액세스 제어가 허용하지 않더라도 in-out으로 전달된 원래 변수에 액세스할 수 없다는 것입니다. 원본에 대한 액세스는 충돌을 일으킵니다. 예를 들어 다음과 같습니다:

```swift
var stepSize = 1

func increment(_ number: inout Int) {
    number += stepSize
}

increment(&stepSize)
// Error: conflicting accesses to stepSize
```

*In the code above, `stepSize` is a global variable, and it’s normally accessible from within `increment(_:)`. However, the read access to `stepSize` overlaps with the write access to `number`. As shown in the figure below, both `number` and `stepSize` refer to the same location in memory. The read and write accesses refer to the same memory and they overlap, producing a conflict.*

위의 코드에서 `stepSize`는 전역 변수이며, 일반적으로 `increment(_:)` 내에서 액세스할 수 있습니다. 그러나 `stepSize`에 대한 읽기 액세스 권한은 `number`에 대한 쓰기 액세스 권한과 겹칩니다. 아래 그림과 같이 `number`와 `stepSize`는 모두 메모리에서 동일한 위치를 나타냅니다. 읽기 및 쓰기 액세스가 동일한 메모리를 참조하고 오버랩되어 충돌이 발생합니다.

*![](https://docs.swift.org/swift-book/images/memory_increment@2x.png)*

*One way to solve this conflict is to make an explicit copy of `stepSize`:*

이 충돌을 해결하는 한 가지 방법은 `stepSize`를 명시적으로 복사하는 것입니다:

```swift
// Make an explicit copy.
var copyOfStepSize = stepSize
increment(&copyOfStepSize)

// Update the original.
stepSize = copyOfStepSize
// stepSize is now 2
```

*When you make a copy of `stepSize` before calling `increment(_:)`, it’s clear that the value of `copyOfStepSize` is incremented by the current step size. The read access ends before the write access starts, so there isn’t a conflict.*

`increment(_:)`를 호출하기 전에 `stepSize`를 복사하면 `copyOfStepSize` 값이 현재 스텝 크기만큼 증가하는 것이 분명합니다. 쓰기 액세스가 시작되기 전에 읽기 액세스가 종료되므로 충돌이 발생하지 않습니다.

*Another consequence of long-term write access to in-out parameters is that passing a single variable as the argument for multiple in-out parameters of the same function produces a conflict. For example:*

인아웃 매개 변수에 대한 장기 쓰기 액세스의 또 다른 결과는 단일 변수를 동일한 함수의 여러 인아웃 매개 변수에 대한 인수로 전달하면 충돌이 발생한다는 것입니다. 예를 들어 다음과 같습니다:

```swift
func balance(_ x: inout Int, _ y: inout Int) {
    let sum = x + y
    x = sum / 2
    y = sum - x
}
var playerOneScore = 42
var playerTwoScore = 30
balance(&playerOneScore, &playerTwoScore)  // OK
balance(&playerOneScore, &playerOneScore)
// Error: conflicting accesses to playerOneScore
```

*The `balance(_:_:)` function above modifies its two parameters to divide the total value evenly between them. Calling it with `playerOneScore` and `playerTwoScore` as arguments doesn’t produce a conflict — there are two write accesses that overlap in time, but they access different locations in memory. In contrast, passing `playerOneScore` as the value for both parameters produces a conflict because it tries to perform two write accesses to the same location in memory at the same time.*

위의 `balance(_:)` 함수는 두 매개변수를 수정하여 전체 값을 두 매개변수 사이에 균등하게 나눕니다. `PlayerOneScore`와 `PlayerTwoScore`를 인수로 사용하면 충돌이 발생하지 않습니다. 즉, 시간적으로 중복되는 두 개의 쓰기 액세스가 있지만 메모리의 다른 위치에 액세스합니다. 반대로 `playerOneScore`를 두 매개 변수의 값으로 전달하면 메모리의 동일한 위치에 동시에 두 번의 쓰기 액세스를 수행하려고 하기 때문에 충돌이 발생합니다.

> *Note*
> 
> *Because operators are functions, they can also have long-term accesses to their in-out parameters. For example, if `balance(_:_:)` was an operator function named `<^>`, writing `playerOneScore <^> playerOneScore` would result in the same conflict as `balance(&playerOneScore, &playerOneScore)`.*
> 
> 연산자는 함수이기 때문에 인아웃 매개변수에 대한 장기적인 액세스 권한도 가질 수 있습니다. 예를 들어 `balance(_:)`가 `<^>`라는 연산자 함수라면 `playerOneScore <^> playerOneScore`를 쓰면 `balance(&playerOneScore, &playerOneScore)`와 동일한 충돌이 발생합니다.
