## *Class-Only Protocols : 클래스 전용 프로토콜*

*You can limit protocol adoption to class types (and not structures or enumerations) by adding the `AnyObject` protocol to a protocol’s inheritance list.*

`AnyObject` 프로토콜을 프로토콜의 상속 목록에 추가하여 프로토콜 채택을 (구조체 또는 열거형이 아닌) 클래스 타입으로 제한할 수 있습니다.

```swift
protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {
    // class-only protocol definition goes here
}
```

*In the example above, `SomeClassOnlyProtocol` can only be adopted by class types. It’s a compile-time error to write a structure or enumeration definition that tries to adopt `SomeClassOnlyProtocol`.*

위의 예에서 `SomeClassOnlyProtocol`은 클래스 타입에 의해서만 채택될 수 있습니다. `SomeClassOnlyProtocol`을 채택하려고 시도하는 구조 또는 열거형 정의를 작성하는 것은 컴파일 타임 오류입니다.

> *NOTE*
> 
> *Use a class-only protocol when the behavior defined by that protocol’s requirements assumes or requires that a conforming type has reference semantics rather than value semantics. For more about reference and value semantics, see [Structures and Enumerations Are Value Types](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID88) and [Classes Are Reference Types](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID89).*
> 
> 해당 프로토콜의 요구 사항에 의해 정의된 동작이 적합한 타입에 값 의미론이 아닌 참조 의미론이 있다고 가정하거나 요구하는 경우 클래스 전용 프로토콜을 사용합니다. 참조 및 값 의미론에 대한 자세한 내용은 [링크]및 [링크]입니다.








