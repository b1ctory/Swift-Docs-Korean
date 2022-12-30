# *Enumerations : 열거형*

*An enumeration defines a common type for a group of related values and enables you to work with those values in a type-safe way within your code.*

열거형은 관련 값 그룹의 공통 타입을 정의하고 코드 내에서 타입 세이프한 방식으로 해당 값을 작업할 수 있도록 합니다.

*If you are familiar with C, you will know that C enumerations assign related names to a set of integer values. Enumerations in Swift are much more flexible, and don’t have to provide a value for each case of the enumeration. If a value (known as a raw value) is provided for each enumeration case, the value can be a string, a character, or a value of any integer or floating-point type.*

C에 익숙하다면 C열거형이 정수 값 집합에 관련 이름을 할당한다는 것을 알게될 것입니다. Swift의 열거형은 훨씬 더 유연하며, 열거형의 각 케이스에 값을 제공할 필요가 없습니다. 각 열거형 사례에 대해 값 (원시 값이라고도 함)이 제공되는 경우 값은 문자열, 문자 혹은 임의의 정수 혹은 부동 소수점 타입의 값이 될 수 있습니다.

*Alternatively, enumeration cases can specify associated values of any type to be stored along with each different case value, much as unions or variants do in other languages. You can define a common set of related cases as part of one enumeration, each of which has a different set of values of appropriate types associated with it.*

또한, 열거형 케이스들은 다른 언어의 조합 혹은 변형과 마찬가지로 서로 다른 케이스 값과 함께 저장할 모든 타입의 관련 값을 지정할 수 있습니다. 관련 사례의 공통 집합을 하나의 열거형의 일부로 정의할 수 있으며, 각 열거형에는 서로 다른 타입의 값 집합이 연결되어 있습니다.

*Enumerations in Swift are first-class types in their own right. They adopt many features traditionally supported only by classes, such as computed properties to provide additional information about the enumeration’s current value, and instance methods to provide functionality related to the values the enumeration represents. Enumerations can also define initializers to provide an initial case value; can be extended to expand their functionality beyond their original implementation; and can conform to protocols to provide standard functionality.*

Swift의 열거형은 그 자체로 1등급 타입입니다. 이들은 열거형의 현재 값에 대한 추가 정보를 제공하는 계산된 속성과 열거형이 나타내는 값과 관련된 기능을 제공하는 인스턴스 메서드와 같이 전통적으로 클래스에서만 지원되는 많은 기능을 채택합니다.열거형은 또한 초기화기를 정의하여 초기 케이스 값을 제공할 수 있으며, 원래 구현 이상으로 기능을 확장할 수 있도록 확장할 수 있으며, 프로토콜을 준수하며 표준 기능을 제공할 수 있습니다.

*For more about these capabilities, see [Properties](https://docs.swift.org/swift-book/LanguageGuide/Properties.html), [Methods](https://docs.swift.org/swift-book/LanguageGuide/Methods.html), [Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html), [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html), and [Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).*

이러한 기능에 대한 자세한 내용은 [링크]를 참조하세요.
