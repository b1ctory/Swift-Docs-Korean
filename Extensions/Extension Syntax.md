## *Extension Syntax : 확장 구문*

*Declare extensions with the `extension` keyword:*

`extension` 키워드를 사용하여 확장을 선언합니다:

```swift
extension SomeType {
    // new functionality to add to SomeType goes here
}
```

*An extension can extend an existing type to make it adopt one or more protocols. To add protocol conformance, you write the protocol names the same way as you write them for a class or structure:*

확장은 기존 타입을 확장하여 하나 이상의 프로토콜을 채택하도록 할 수 있습니다. 프로토콜 적합성을 추가하려면 프로토콜 이름을 클래스 또는 구조체에 대해 작성하는 것과 동일한 방식으로 작성합니다:

```swift
extension SomeType: SomeProtocol, AnotherProtocol {
    // implementation of protocol requirements goes here
}
```

*Adding protocol conformance in this way is described in [Adding Protocol Conformance with an Extension](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html#ID277).* 

이러한 방식으로 프로토콜 준수를 추가하는 방법은 [링크]에 설명되어있습니다.

*An extension can be used to extend an existing generic type, as described in [Extending a Generic Type](https://docs.swift.org/swift-book/LanguageGuide/Generics.html#ID185). You can also extend a generic type to conditionally add functionality, as described in [Extensions with a Generic Where Clause](https://docs.swift.org/swift-book/LanguageGuide/Generics.html#ID553).*

[링크]에서 설명한 대로 확장을 사용하여 기존 일반 타입을 확장할 수 있습니다. 또한 [링크] 에 설명된 대로 일반 타입을 확장하여 조건부로 기능을 추가할 수도 있습니다

> *NOTE*
> 
> *If you define an extension to add new functionality to an existing type, the new functionality will be available on all existing instances of that type, even if they were created before the extension was defined.*
> 
> 기존 타입에 새 기능을 추가하기 위해 확장을 정의하면, 확장이 정의되기 전에 생성된 경우에도 마찬가지로, 해당 타입의 모든 기존 인스턴스에서 새 기능을 사용할 수 있습니다. 
