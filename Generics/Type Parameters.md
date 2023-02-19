## *Type Parameters : 타입 매개변수*

*In the `swapTwoValues(_:_:)` example above, the placeholder type `T` is an example of a type parameter. Type parameters specify and name a placeholder type, and are written immediately after the function’s name, between a pair of matching angle brackets (such as `<T>`).*

위의 `swapTwoValues(_:_:)` 예시에서 플레이스 홀더 타입 `T`는 타입 매개변수의 예시입니다. 타입 매개변수는 플레이스홀더 타입을 지정하고 이름을 지정하며 함수 이름 바로 뒤에 일치하는 꺾쇠 괄호 쌍(예: `<T>`) 사이에 작성됩니다.

*Once you specify a type parameter, you can use it to define the type of a function’s parameters (such as the `a` and `b` parameters of the `swapTwoValues(_:_:)` function), or as the function’s return type, or as a type annotation within the body of the function. In each case, the type parameter is replaced with an actual type whenever the function is called. (In the `swapTwoValues(_:_:)` example above, `T` was replaced with `Int` the first time the function was called, and was replaced with `String` the second time it was called.)*

타입 매개변수를 지정하면 이를 사용하여 함수의 매개변수 타입(예: `swapTwoValues(_:_:)` 함수의 `a` 및 `b` 매개변수)을 정의하거나 함수의 매개변수로 사용할 수 있습니다. 반환 타입 또는 함수 본문 내의 타입 주석으로. 각각의 경우에 type 매개변수는 함수가 호출될 때마다 실제 타입으로 대체됩니다. (위의 `swapTwoValues(_:_:)` 예에서 `T`는 함수가 처음 호출될 때 `Int`로 대체되었고 두 번째 호출될 때 `String`으로 대체되었습니다.)

*You can provide more than one type parameter by writing multiple type parameter names within the angle brackets, separated by commas.*

각괄호 안에 쉼표로 구분하여 여러 타입 매개변수 이름을 작성하여 유형 매개변수를 두 개 이상 제공할 수 있습니다.
