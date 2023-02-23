## *Generic Subscripts : 제네릭 서브스크립트*

*Subscripts can be generic, and they can include generic `where` clauses. You write the placeholder type name inside angle brackets after `subscript`, and you write a generic `where` clause right before the opening curly brace of the subscript’s body. For example:*

서브스크립트는 제네릭일 수 있으며 제네릭 `where` 절을 포함할 수 있습니다. 플레이스홀더 타입 이름은 `subscript`뒤의 꺾쇠 괄호 안에 쓰고, 서브스크립트 본문의 여는 중괄호 바로 앞에 제네릭 `where` 절을 씁니다. 예를 들어:

```swift
extension Container {
    subscript<Indices: Sequence>(indices: Indices) -> [Item]
            where Indices.Iterator.Element == Int {
        var result: [Item] = []
        for index in indices {
            result.append(self[index])
        }
        return result
    }
}
```

*This extension to the `Container` protocol adds a subscript that takes a sequence of indices and returns an array containing the items at each given index. This generic subscript is constrained as follows:*

`Container` 프로토콜에 대한 이 확장은 일련의 인덱스를 취하고 지정된 각 색인의 항목을 포함하는 배열을 반환하는 서브스크립트를 추가합니다. 이 제네릭 서브스크립트는 다음과 같이 제한됩니다.

- *The generic parameter `Indices` in angle brackets has to be a type that conforms to the `Sequence` protocol from the standard library.*
  
  꺽쇠 괄호 안의 제네릭 매개변수 `Indices`는 표준 라이브러리의 `Sequence` 프로토콜을 준수하는 타입이어야 합니다.

- *The subscript takes a single parameter, `indices`, which is an instance of that `Indices` type.*
  
  서브스크립트는 해당 `Indices` 타입의 인스턴스인 `indices`라는 단일 매개변수를 사용합니다.

- *The generic `where` clause requires that the iterator for the sequence must traverse over elements of type `Int`. This ensures that the indices in the sequence are the same type as the indices used for a container.*
  
  제네릭 `where` 절에서는 시퀀스의 반복자가 `Int`타입의 요소를 통과해야 합니다. 이렇게 하면 시퀀스의 인덱스가 컨테이너에 사용되는 인덱스와 동일한 타입이 됩니다.

*Taken together, these constraints mean that the value passed for the `indices` parameter is a sequence of integers.*

 종합하면 이러한 제약 조건은 `indices` 매개변수에 전달된 값이 일련의 정수임을 의미합니다.
