## *Associated Types with a Generic Where Clause : 제네릭 Where 절과 연결된 타입*

*You can include a generic `where` clause on an associated type. For example, suppose you want to make a version of `Container` that includes an iterator, like what the `Sequence` protocol uses in the standard library. Here’s how you write that:*

연결된 타입에 제네릭 `where` 절을 포함할 수 있습니다. 예를 들어 표준 라이브러리에서 `Sequence` 프로토콜이 사용하는 것과 같은 반복자를 포함하는 `Container` 버전을 만들고 싶다고 가정해 보겠습니다. 작성 방법은 다음과 같습니다.

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }

    associatedtype Iterator: IteratorProtocol where Iterator.Element == Item
    func makeIterator() -> Iterator
}
```

*The generic `where` clause on `Iterator` requires that the iterator must traverse over elements of the same item type as the container’s items, regardless of the iterator’s type. The `makeIterator()` function provides access to a container’s iterator.*

`Iterator`에 대한 제네릭 `where` 절은 반복자가 반복자의 타입에 관계없이 컨테이너의 아이템과 동일한 아이템 타입의 요소를 순회해야 한다고 요구합니다. `makeIterator()` 함수는 컨테이너의 반복자에 대한 액세스를 제공합니다.

*For a protocol that inherits from another protocol, you add a constraint to an inherited associated type by including the generic `where` clause in the protocol declaration. For example, the following code declares a `ComparableContainer` protocol that requires `Item` to conform to `Comparable`:*

다른 프로토콜에서 상속하는 프로토콜의 경우 프로토콜 선언에 제네릭 `where` 절을 포함하여 상속된 관련 타입에 제약 조건을 추가합니다. 예를 들어 다음 코드는 `Item`이 `Comparable`을 준수해야 하는 `ComparableContainer` 프로토콜을 선언합니다.

```swift
protocol ComparableContainer: Container where Item: Comparable { }
```
