## *Generic Where Clauses : 제네릭 Where 절*

*Type constraints, as described in [Type Constraints](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics#Type-Constraints), enable you to define requirements on the type parameters associated with a generic function, subscript, or type.*

[링크]에 설명된 대로 타입 제약 조건을 사용하면 일반 함수, 서브스크립트 또는 타입과 관련된 타입 매개변수에 대한 요구 사항을 정의할 수 있습니다.

*It can also be useful to define requirements for associated types. You do this by defining a generic where clause. A generic `where` clause enables you to require that an associated type must conform to a certain protocol, or that certain type parameters and associated types must be the same. A generic `where` clause starts with the `where` keyword, followed by constraints for associated types or equality relationships between types and associated types. You write a generic `where` clause right before the opening curly brace of a type or function’s body.*

관련 타입에 대한 요구 사항을 정의하는 것도 유용할 수 있습니다. 제네릭 `where` 절을 정의하면 됩니다. 제네릭 `where` 절을 사용하면 연결된 타입이 특정 프로토콜을 준수해야 하거나 특정 타입 매개변수와 연결된 타입이 동일해야 한다고 요구할 수 있습니다. 제네릭 `where` 절은 `where` 키워드로 시작하고 그 뒤에 관련 타입에 대한 제약 조건 또는 타입과 관련 타입 간의 동등 관계가 옵니다. 타입 또는 함수 본문의 여는 중괄호 바로 앞에 제네릭 `where` 절을 작성합니다.

*The example below defines a generic function called `allItemsMatch`, which checks to see if two `Container` instances contain the same items in the same order. The function returns a Boolean value of `true` if all items match and a value of `false` if they don’t.*

아래 예는 `allItemsMatch`라는 일반 함수를 정의하여 두 개의 `Container` 인스턴스에 동일한 항목이 동일한 순서로 포함되어 있는지 확인합니다. 이 함수는 모든 항목이 일치하면 부울 값 `true`를 반환하고 일치하지 않으면 `false` 값을 반환합니다.

*The two containers to be checked don’t have to be the same type of container (although they can be), but they do have to hold the same type of items. This requirement is expressed through a combination of type constraints and a generic `where` clause:*

확인할 두 개의 컨테이너는 동일한 타입의 컨테이너일 필요는 없지만(그럴 수도 있음) 동일한 타입의 항목을 보관해야 합니다. 이 요구 사항은 타입 제약 조건과 일반적인 `where` 절의 조합을 통해 표현됩니다.

```swift
func allItemsMatch<C1: Container, C2: Container>
        (_ someContainer: C1, _ anotherContainer: C2) -> Bool
        where C1.Item == C2.Item, C1.Item: Equatable {

    // Check that both containers contain the same number of items.
    if someContainer.count != anotherContainer.count {
        return false
    }

    // Check each pair of items to see if they're equivalent.
    for i in 0..<someContainer.count {
        if someContainer[i] != anotherContainer[i] {
            return false
        }
    }

    // All items match, so return true.
    return true
}
```

*This function takes two arguments called `someContainer` and `anotherContainer`. The `someContainer` argument is of type `C1`, and the `anotherContainer` argument is of type `C2`. Both `C1` and `C2` are type parameters for two container types to be determined when the function is called.*

이 함수는 `someContainer`와 `anotherContainer`라는 두 개의 인수를 사용합니다. `someContainer` 인수는 `C1` 타입이고 `anotherContainer` 인수는 `C2` 타입입니다. `C1`과 `C2`는 모두 함수가 호출될 때 결정되는 두 개의 컨테이너 타입에 대한 타입 매개 변수입니다.

*The following requirements are placed on the function’s two type parameters:*

함수의 두 가지 타입 매개변수에는 다음과 같은 요구사항이 있습니다:

- *`C1` must conform to the `Container` protocol (written as `C1: Container`).*
  
  `C1`은 `Container` 프로토콜(`C1: Container`로 작성됨)을 준수해야 합니다.

- *`C2` must also conform to the `Container` protocol (written as `C2: Container`).*
  
  `C2`도 `Container` 프로토콜(`C2: Container`로 작성됨)을 준수해야 합니다.

- *The `Item` for `C1` must be the same as the `Item` for `C2` (written as `C1.Item == C2.Item`).*
  
  `C1`의 `Item`은 `C2`의 `Item`과 같아야 합니다. (`C1.Item == C2.Item` 이라고 작성됨).

- *The `Item` for `C1` must conform to the `Equatable` protocol (written as `C1.Item: Equatable`).*
  
  `C1`에 대한 `Item`은 `Equatable` 프로토콜(`C1.Item: Equatable`로 작성됨)을 준수해야 합니다.

*The first and second requirements are defined in the function’s type parameter list, and the third and fourth requirements are defined in the function’s generic `where` clause.*

첫 번째 및 두 번째 요구 사항은 함수의 타입 매개변수 목록에 정의되어 있고 세 번째 및 네 번째 요구 사항은 함수의 제네릭 `where` 절에 정의되어 있습니다.

*These requirements mean:*

이러한 요구사항은 다음을 의미합니다.

- *`someContainer` is a container of type `C1`.*
  
  `someContainer`는 `C1` 타입의 컨테이너입니다.

- *`anotherContainer` is a container of type `C2`.*
  
  `anotherContainer`는 `C2` 타입의 컨테이너입니다.

- *`someContainer` and `anotherContainer` contain the same type of items.*
  
  `someContainer` 및 `anotherContainer`는 동일한 타입의 항목을 포함합니다.

- *The items in `someContainer` can be checked with the not equal operator (`!=`) to see if they’re different from each other.*
  
  `someContainer`의 항목은 같지 않음 연산자(`!=`)를 사용하여 서로 다른지 확인할 수 있습니다.

*The third and fourth requirements combine to mean that the items in `anotherContainer` can also be checked with the `!=` operator, because they’re exactly the same type as the items in `someContainer`.*

세 번째와 네 번째 요구사항이 결합되어 `anotherContainer`의 항목이 `someContainer`의 항목과 정확히 동일한 타입이기 때문에 `!=` 연산자로도 확인할 수 있음을 의미합니다. 

*These requirements enable the `allItemsMatch(_:_:)` function to compare the two containers, even if they’re of a different container type.*

이러한 요구사항을 통해 `allItemsMatch(_:_:)` 함수는 컨테이너 타입이 다른 경우에도 두 컨테이너를 비교할 수 있습니다.

*The `allItemsMatch(_:_:)` function starts by checking that both containers contain the same number of items. If they contain a different number of items, there’s no way that they can match, and the function returns `false`.*

`allItemsMatch(_:_:)` 함수는 두 컨테이너에 동일한 수의 항목이 포함되어 있는지 확인하는 것으로 시작합니다. 다른 개수의 항목이 포함된 경우 일치시킬 수 있는 방법이 없으며 함수는 `false`를 반환합니다.

*After making this check, the function iterates over all of the items in `someContainer` with a `for`-`in` loop and the half-open range operator (`..<`). For each item, the function checks whether the item from `someContainer` isn’t equal to the corresponding item in `anotherContainer`. If the two items aren’t equal, then the two containers don’t match, and the function returns `false`.*

이 확인을 수행한 후 함수는 `for`-`in` 루프 및 반개방 범위 연산자(`..<`)를 사용하여 `someContainer`의 모든 항목을 반복합니다. 각 항목에 대해 함수는 `someContainer`의 항목이 `anotherContainer`의 해당 항목과 같지 않은지 확인합니다. 두 항목이 같지 않으면 두 컨테이너가 일치하지 않으며 함수는 `false`를 반환합니다.

*If the loop finishes without finding a mismatch, the two containers match, and the function returns `true`.*

루프가 불일치를 찾지 않고 완료되면 두 컨테이너가 일치하고 함수가 `true`를 반환합니다.

*Here’s how the `allItemsMatch(_:_:)` function looks in action:*

`allItemsMatch(_:_:)` 함수가 작동하는 방식은 다음과 같습니다.

```swift
var stackOfStrings = Stack<String>()
stackOfStrings.push("uno")
stackOfStrings.push("dos")
stackOfStrings.push("tres")

var arrayOfStrings = ["uno", "dos", "tres"]

if allItemsMatch(stackOfStrings, arrayOfStrings) {
    print("All items match.")
} else {
    print("Not all items match.")
}
// Prints "All items match."
```

*The example above creates a `Stack` instance to store `String` values, and pushes three strings onto the stack. The example also creates an `Array` instance initialized with an array literal containing the same three strings as the stack. Even though the stack and the array are of a different type, they both conform to the `Container` protocol, and both contain the same type of values. You can therefore call the `allItemsMatch(_:_:)` function with these two containers as its arguments. In the example above, the `allItemsMatch(_:_:)` function correctly reports that all of the items in the two containers match.*

위의 예는 `String` 값을 저장하기 위해 `Stack` 인스턴스를 만들고 3개의 문자열을 스택에 푸시합니다. 이 예에서는 스택과 동일한 3개의 문자열을 포함하는 배열 리터럴로 초기화된 `Array` 인스턴스도 생성합니다. 스택과 배열은 다른 타입이지만 둘 다 `Container` 프로토콜을 준수하고 동일한 타입의 값을 포함합니다. 따라서 이 두 컨테이너를 인수로 사용하여 `allItemsMatch(_:_:)` 함수를 호출할 수 있습니다. 위의 예에서 `allItemsMatch(_:_:)` 함수는 두 컨테이너의 모든 항목이 일치한다고 올바르게 보고합니다.
