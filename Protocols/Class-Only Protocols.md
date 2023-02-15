## *Class-Only Protocols*

*You can limit protocol adoption to class types (and not structures or enumerations) by adding the `AnyObject` protocol to a protocol’s inheritance list.*

```swift
protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {
    // class-only protocol definition goes here
}
```

*In the example above, `SomeClassOnlyProtocol` can only be adopted by class types. It’s a compile-time error to write a structure or enumeration definition that tries to adopt `SomeClassOnlyProtocol`.*

> *NOTE*
> 
> *Use a class-only protocol when the behavior defined by that protocol’s requirements assumes or requires that a conforming type has reference semantics rather than value semantics. For more about reference and value semantics, see [Structures and Enumerations Are Value Types](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID88) and [Classes Are Reference Types](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID89).*


