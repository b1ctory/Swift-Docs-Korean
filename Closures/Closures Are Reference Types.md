## *Closures Are Reference Types : 클로저는 참조 타입입니다.*

*In the example above, `incrementBySeven` and `incrementByTen` are constants, but the closures these constants refer to are still able to increment the `runningTotal` variables that they have captured. This is because functions and closures are reference types.*

위의 예에서 `incrementBySeven`와 `incrementByTen`는 상수 이지만, 이러한 상수가 가리키는 클로저는 여전히 캡쳐한 `runningTotal` 변수를 증가시킬 수 있습니다. 함수와 클로저는 참조 타입이기 때문입니다.

*Whenever you assign a function or a closure to a constant or a variable, you are actually setting that constant or variable to be a reference to the function or closure. In the example above, it’s the choice of closure that `incrementByTen` refers to that’s constant, and not the contents of the closure itself.*

함수 혹은 클로저를 상수 혹은 변수에 할당할 때마다 실제로 해당 상수 혹은 변수를 함수 혹은 클로저에 대한 참조로 설정합니다. .위의 예에서 클로저의 선택 `incrementByTen`은 그것이 상수인 것이지 클로저 자체의 내용은 아닙니다.

*This also means that if you assign a closure to two different constants or variables, both of those constants or variables refer to the same closure.*

따라서 두 개의 서로 다른 상수 혹은 변수에 클로저를 할당하는 경우 두 상수 혹은 변수가 모두 동일한 클로저를 참조한다는 것을 의미합니다.

```swift
let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()
// returns a value of 50

incrementByTen()
// returns a value of 60
```

*The example above shows that calling `alsoIncrementByTen` is the same as calling `incrementByTen`. Because both of them refer to the same closure, they both increment and return the same running total.*

위의 예는 `alsoIncrementByTen`을 호출하는 것이 `incrementByTen`과 같음을 보여줍니다. 둘 다 동일한 클로저를 참조하기 때문에 둘 다 증가하고 동일한 실행 합계를 반환합니다.


