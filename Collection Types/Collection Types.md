# *Collection Types : 컬렉션 타입*

*Swift provides three primary collection types, known as arrays, sets, and dictionaries, for storing collections of values. Arrays are ordered collections of values. Sets are unordered collections of unique values. Dictionaries are unordered collections of key-value associations.*

Swift는 배열, 집합 및 딕셔너리로 알려진 세가지 주요 컬렉션 유형을 제공해서 컬렉션의 값을 저장합니다. 배열은 순서가 지정된 값의 집합입니다. 집합은 고유값의 순서 없는 집합입니다. 딕셔너리는 키-값 연결의 순서가 지정되지 않은 컬렉션입니다.

*![](https://docs.swift.org/swift-book/_images/CollectionTypes_intro_2x.png)*

*Arrays, sets, and dictionaries in Swift are always clear about the types of values and keys that they can store. This means that you can’t insert a value of the wrong type into a collection by mistake. It also means you can be confident about the type of values you will retrieve from a collection.*

Swift 의 배열, 집합 및 딕셔너리는 저장할 수 있는 값과 키의 유형을 명확하게 알 수 있습니다. 이것은 잘못된 유형의 값을 실수로 컬렉션에 삽입할 수 없다는 것입니다. 또한 컬렉션에서 검색할 값의 타입에 대해 자신감을 가질 수 있습니다.

> *NOTE*
> 
> *Swift’s array, set, and dictionary types are implemented as generic collections. For more about generic types and collections, see [Generics](https://docs.swift.org/swift-book/LanguageGuide/Generics.html).*
> 
> Swift의 배열, 집합, 딕셔너리 타입은 일반 컬렉션으로 구현됩니다. 일반 타입 및 컬렉션에 대한 자세한 내용은 [링크]를 참조하세요.

## *Mutability of Collections : 컬렉션의 가변성*

*If you create an array, a set, or a dictionary, and assign it to a variable, the collection that’s created will be mutable. This means that you can change (or mutate) the collection after it’s created by adding, removing, or changing items in the collection. If you assign an array, a set, or a dictionary to a constant, that collection is immutable, and its size and contents can’t be changed.*

배열, 집합 혹은 딕셔너리를 만들고 이를 변수에 할당하면 생성된 컬렉션이 변경될 수 있습니다. 즉, 컬렉션의 항목을 추가, 제거 혹은 변경하여 컬렉션을 만든 후에 변경 (혹은 변경)할 수 있습니다. 배열, 집합 혹은 딕셔너리를 상수에 할당하면 해당 컬렉션은 변경할 수 없으며 크기와 내용은 변경할 수 없습니다. 

> *NOTE*
> 
> *It’s good practice to create immutable collections in all cases where the collection doesn’t need to change. Doing so makes it easier for you to reason about your code and enables the Swift compiler to optimize the performance of the collections you create.*
> 
> 컬렉션을 변경할 필요가 없는 모든 경우에 불변 컬렉션을 만드는 것이 좋습니다. 이렇게 하면 코드에 대한 추론이 더 쉬워지고 Swift 컴파일러가 생성한 컬렉션의 성능을 최적화할 수 있습니다.
