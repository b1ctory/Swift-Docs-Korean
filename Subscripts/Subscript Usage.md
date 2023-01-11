## *Subscript Usage : 서브스크립트 사용*

*The exact meaning of “subscript” depends on the context in which it’s used. Subscripts are typically used as a shortcut for accessing the member elements in a collection, list, or sequence. You are free to implement subscripts in the most appropriate way for your particular class or structure’s functionality.*

"서브스크립트"의 정확한 의미는 사용되는 문맥에 따라 다릅니다. 서브스크립트는 일반적으로 집합, 목록 또는 시퀀스의 구성원 요소에 액세스하기 위한 바로 가기로 사용됩니다. 특정 클래스 또는 구조체의 기능에 가장 적합한 방법으로 구독자를 구현할 수 있습니다.

*For example, Swift’s `Dictionary` type implements a subscript to set and retrieve the values stored in a `Dictionary` instance. You can set a value in a dictionary by providing a key of the dictionary’s key type within subscript brackets, and assigning a value of the dictionary’s value type to the subscript:*

예를 들어 Swift의 `Dictionary` 타입은 `Dictionary` 인스턴스에 저장된 값을 설정하고 검색하기 위한 서브스크립트를 구현합니다. 서브스크립트 괄호 안에 딕셔너리 키 타입의 키를 입력하고 딕셔너리 값 타입의 값을 서브스크립트에 할당하여 딕셔너리의 값을 설정할 수 있습니다:

```swift
var numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
numberOfLegs["bird"] = 2
```

*The example above defines a variable called `numberOfLegs` and initializes it with a dictionary literal containing three key-value pairs. The type of the `numberOfLegs` dictionary is inferred to be `[String: Int]`. After creating the dictionary, this example uses subscript assignment to add a `String` key of `"bird"` and an `Int` value of `2` to the dictionary.*

위의 예는 `numberOfLegs`라는 변수를 정의하고 세 개의 키-값 쌍을 포함하는 딕셔너리 리터럴로 초기화합니다. `numberOfLegs` 딕셔너리의 타입은 `[String: Int]`로 유추됩니다. 딕셔너리를 만든 후 이 예에서는 서브스크립트 할당을 사용하여 딕셔너리에 `String` 키 `bird`와 `Int` 값 `2`를 추가합니다.

*For more information about `Dictionary` subscripting, see [Accessing and Modifying a Dictionary](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html#ID116).*

`Dictionary` 서브스크립트에 대한 자세한 내용은 [링크]를 확인하세요.

> *NOTE*
> 
> *Swift’s `Dictionary` type implements its key-value subscripting as a subscript that takes and returns an optional type. For the `numberOfLegs` dictionary above, the key-value subscript takes and returns a value of type `Int?`, or “optional int”. The `Dictionary` type uses an optional subscript type to model the fact that not every key will have a value, and to give a way to delete a value for a key by assigning a `nil` value for that key.*
> 
> Swift의 `Dictionary` 타입은 키-값 서브스크립트를 옵셔널 타입을 가져와서 반환하는 서브스크립트로 구현합니다. 위의 `numberOfLegs` 딕셔너리의 경우 키 값 서브스크립트는 `Int?` 또는 "optional int" 타입의 값을 가져와서 반환합니다. `Dictionary` 타입은 옵셔널 서브스크립트 타입을 사용하여 모든 키에 값이 있는 것은 아니라는 사실을 모델링하고 해당 키에 `nil` 값을 할당하여 키에 대한 값을 삭제할 수 있는 방법을 제공합니다.
