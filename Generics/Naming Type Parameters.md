## *Naming Type Parameters: 네이밍 타입 매개변수*

*In most cases, type parameters have descriptive names, such as `Key` and `Value` in `Dictionary<Key, Value>` and `Element` in `Array<Element>`, which tells the reader about the relationship between the type parameter and the generic type or function it’s used in. However, when there isn’t a meaningful relationship between them, it’s traditional to name them using single letters such as `T`, `U`, and `V`, such as `T` in the `swapTwoValues(_:_:)` function above.*

대부분의 경우 타입매개 변수는 `Dictionary<Key, Value>`의 `Key`와 `Value`, 그리고 타입 매개 변수와 사용되는 일반 타입 또는 함수 사이의 관계를 알려주는 `Array<Element>`의 `Element`와 같은 설명적 이름을 가집니다. 그러나 이 둘 사이에 의미 있는 관계가 없을 때는 위의 `swapTwoValues(_:)` 함수에서 `T`와 같이 `T`, `U`, `V`와 같은 단일 문자를 사용하여 이름을 짓는 것이 보통입니다.

> *Note*
> 
> *Always give type parameters upper camel case names (such as `T` and `MyTypeParameter`) to indicate that they’re a placeholder for a type, not a value.*
> 
> 항상 대문자 카멜케이스 이름(예: `T` 및 `MyTypeParameter`)을 지정하여 값이 아닌 타입의 플레이스 홀더임을 나타냅니다.


