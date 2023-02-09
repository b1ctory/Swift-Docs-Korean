## *Protocol Syntax: 프로토콜 구문*

*You define protocols in a very similar way to classes, structures, and enumerations:*

프로토콜은 클래스, 구조체 혹은 열거형과 매우 비슷한 방식으로 정의할 수 있습니다.

```swift
protocol SomeProtocol {
    // protocol definition goes here
}
```

*Custom types state that they adopt a particular protocol by placing the protocol’s name after the type’s name, separated by a colon, as part of their definition. Multiple protocols can be listed, and are separated by commas:*

사용자 정의 타입은 정의의 일부로 콜론으로 구분된 타입 이름 뒤에 프로토콜 이름을 배치하여 특정 프로토콜을 채택함을 나타냅니다. 여러 개의 프로토콜을 나열할 수 있으며 쉼표로 구분됩니다:

```swift
struct SomeStructure: FirstProtocol, AnotherProtocol {
    // structure definition goes here
}
```

*If a class has a superclass, list the superclass name before any protocols it adopts, followed by a comma:*

클래스에 superclass가 있는 경우 채택하는 프로토콜 앞에 superclass 이름을 나열하고 쉼표를 표시합니다:

```swift
class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
    // class definition goes here
}
```
