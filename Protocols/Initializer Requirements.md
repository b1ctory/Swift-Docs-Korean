## *Initializer Requirements*

*Protocols can require specific initializers to be implemented by conforming types. You write these initializers as part of the protocol’s definition in exactly the same way as for normal initializers, but without curly braces or an initializer body:*

```swift
protocol SomeProtocol {
    init(someParameter: Int)
}
```

### *Class Implementations of Protocol Initializer Requirements*

*You can implement a protocol initializer requirement on a conforming class as either a designated initializer or a convenience initializer. In both cases, you must mark the initializer implementation with the `required` modifier:*

```swift
class SomeClass: SomeProtocol {
    required init(someParameter: Int) {
        // initializer implementation goes here
    }
}
```

*The use of the `required` modifier ensures that you provide an explicit or inherited implementation of the initializer requirement on all subclasses of the conforming class, such that they also conform to the protocol.*

*For more information on required initializers, see [Required Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID231).*

> *NOTE*
> 
> *You don’t need to mark protocol initializer implementations with the `required` modifier on classes that are marked with the `final` modifier, because final classes can’t subclassed. For more about the `final` modifier, see [Preventing Overrides](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html#ID202).*

*If a subclass overrides a designated initializer from a superclass, and also implements a matching initializer requirement from a protocol, mark the initializer implementation with both the `required` and `override` modifiers:*

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

### *Failable Initializer Requirements*

*Protocols can define failable initializer requirements for conforming types, as defined in [Failable Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID224).*

*A failable initializer requirement can be satisfied by a failable or nonfailable initializer on a conforming type. A nonfailable initializer requirement can be satisfied by a nonfailable initializer or an implicitly unwrapped failable initializer.*
