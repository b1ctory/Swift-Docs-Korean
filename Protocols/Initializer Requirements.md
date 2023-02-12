## *Initializer Requirements : 초기화 요구사항*

*Protocols can require specific initializers to be implemented by conforming types. You write these initializers as part of the protocol’s definition in exactly the same way as for normal initializers, but without curly braces or an initializer body:*

프로토콜은 특정 이니셜라이저를 적합한 타입으로 구현해야 할 수 있습니다. 이러한 이니셜라이저는 일반 이니셜라이저와 동일한 방식으로 프로토콜 정의의 일부로 작성하지만, 중괄호나 이니셜라이저 본문은 사용하지 않습니다:

```swift
protocol SomeProtocol {
    init(someParameter: Int)
}
```

### *Class Implementations of Protocol Initializer Requirements : 프로토콜 이니셜라이저 요구사항의 클래스 구현*

*You can implement a protocol initializer requirement on a conforming class as either a designated initializer or a convenience initializer. In both cases, you must mark the initializer implementation with the `required` modifier:*

프로토콜 이니셜라이저 요구사항을 지정된 이니셜라이저 또는 편의 이니셜라이저로 적합한 클래스에 구현할 수 있습니다. 두 경우 모두 이니셜라이저 구현을 `required` 수식자로 표시해야 합니다:

```swift
class SomeClass: SomeProtocol {
    required init(someParameter: Int) {
        // initializer implementation goes here
    }
}
```

*The use of the `required` modifier ensures that you provide an explicit or inherited implementation of the initializer requirement on all subclasses of the conforming class, such that they also conform to the protocol.*

`required` 수식자를 사용하면 적합 클래스의 모든 하위 클래스에 대한 초기화 요구 사항의 명시적 또는 상속된 구현을 제공하여 프로토콜도 준수하도록 합니다.

*For more information on required initializers, see [Required Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID231).*

필수 이니셜라이저에 대한 자세한 내용은 [링크]를 참조하세요.

> *NOTE*
> 
> *You don’t need to mark protocol initializer implementations with the `required` modifier on classes that are marked with the `final` modifier, because final classes can’t subclassed. For more about the `final` modifier, see [Preventing Overrides](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html#ID202).*
> 
> 최종 클래스는 하위 분류할 수 없기 때문에 `final` 수식자로 표시된 클래스에서는 프로토콜 이니셜라이저 구현을 `required` 수식자로 표시할 필요가 없습니다. `final` 수식어에 대한 자세한 내용은 [링크]를 참조하세요.

*If a subclass overrides a designated initializer from a superclass, and also implements a matching initializer requirement from a protocol, mark the initializer implementation with both the `required` and `override` modifiers:*

하위 클래스가 슈퍼 클래스의 지정된 이니셜라이저를 재정의하고 프로토콜의 일치하는 이니셜라이저 요구사항을 구현하는 경우, 이니셜라이저 구현을 모두 `required` 및 `override` 수식자로 표시합니다:

```swift
protocol SomeProtocol {
    init()
}

class SomeSuperClass {
    init() {
        // initializer implementation goes here
    }
}

class SomeSubClass: SomeSuperClass, SomeProtocol {
    // "required" from SomeProtocol conformance; "override" from SomeSuperClass
    required override init() {
        // initializer implementation goes here
    }
}
```

### *Failable Initializer Requirements : 실패할 수 있는 이니셜라이저 요구사항*

*Protocols can define failable initializer requirements for conforming types, as defined in [Failable Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID224).*

프로토콜은 [링크]에 정의된 대로 적합한 타입에 대한 실패 가능한 이니셜라이저 요구사항을 정의할 수 있습니다.

*A failable initializer requirement can be satisfied by a failable or nonfailable initializer on a conforming type. A nonfailable initializer requirement can be satisfied by a nonfailable initializer or an implicitly unwrapped failable initializer.*

실패할 수 있는 이니셜라이저 요구사항은 적합한 타입의 실패할 수 있는 또는 실패할 수 없는 이니셜라이저에 의해 충족될 수 있습니다. 사용불가능한 이니셜라이저 요구 사항은 사용 불가능한 이니셜라이저 또는 암시적으로 언래핑된 이니셜라이저를 통해 충족될 수 있습니다.


