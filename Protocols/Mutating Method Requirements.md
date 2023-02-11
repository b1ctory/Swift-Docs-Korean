## *Mutating Method Requirements*

*It’s sometimes necessary for a method to modify (or mutate) the instance it belongs to. For instance methods on value types (that is, structures and enumerations) you place the `mutating` keyword before a method’s `func` keyword to indicate that the method is allowed to modify the instance it belongs to and any properties of that instance. This process is described in [Modifying Value Types from Within Instance Methods](https://docs.swift.org/swift-book/LanguageGuide/Methods.html#ID239).*

메서드가 속한 인스턴스를 수정(또는 변환)해야 하는 경우가 있습니다. 값 타입(즉, 구조체 및 열거형)에 대한 인스턴스 메서드의 경우 메서드의 `func` 키워드 앞에 `mutating` 키워드를 배치하여 메서드가 해당 인스턴스에 속하는 인스턴스와 해당 인스턴스의 프로퍼티를 수정할 수 있음을 나타냅니다. 이 프로세스는 [링크]에 설명되어 있습니다.

*If you define a protocol instance method requirement that’s intended to mutate instances of any type that adopts the protocol, mark the method with the `mutating` keyword as part of the protocol’s definition. This enables structures and enumerations to adopt the protocol and satisfy that method requirement.*

프로토콜을 채택하는 모든 타입의 인스턴스를 변환하기 위한 프로토콜 인스턴스 메서드 요구사항을 정의하는 경우 프로토콜 정의의 일부로 `mutating` 키워드를 사용하여 메서드를 표시합니다. 이를 통해 구조 체 및 열거형이 프로토콜을 채택하고 해당 메서드 요구 사항을 충족할 수 있습니다.

> *NOTE*
> 
> *If you mark a protocol instance method requirement as `mutating`, you don’t need to write the `mutating` keyword when writing an implementation of that method for a class. The `mutating` keyword is only used by structures and enumerations.*
> 
> 프로토콜 인스턴스 메서드 요구 사항을 `mutating`으로 표시하면 클래스에 대한 해당 메서드의 구현을 작성할 때 `mutating` 키워드를 작성할 필요가 없습니다. `mutating` 키워드는 구조체 및 열거형에만 사용됩니다.

*The example below defines a protocol called `Togglable`, which defines a single instance method requirement called `toggle`. As its name suggests, the `toggle()` method is intended to toggle or invert the state of any conforming type, typically by modifying a property of that type.*

아래 예제에서는 `Togglable`이라는 프로토콜을 정의하고 있으며, 이 프로토콜은 `Togglable`이라는 단일 인스턴스 메서드 요구 사항을 정의합니다. 이름에서 알 수 있듯이, `toggle()` 메서드는 일반적으로 해당 타입의 프로퍼티를 수정하여 적합한 타입의 상태를 전환하거나 반전시키기 위한 것입니다.

*The `toggle()` method is marked with the `mutating` keyword as part of the `Togglable` protocol definition, to indicate that the method is expected to mutate the state of a conforming instance when it’s called:*

`Togglable`프로토콜 정의의 일부로 `mutating` 키워드를 사용하여 `toggle()` 메서드가 호출될 때 적합한 인스턴스의 상태를 변환할 것으로 예상됨을 나타냅니다:

```swift
protocol Togglable {
    mutating func toggle()
}
```

*If you implement the `Togglable` protocol for a structure or enumeration, that structure or enumeration can conform to the protocol by providing an implementation of the `toggle()` method that’s also marked as `mutating`.*

구조체 또는 열거형에 대해 `Togglable` 프로토콜을 구현하는 경우, 해당 구조체 또는 열거형은 `mutating`으로 표시된 `togglle()` 메서드의 구현을 제공하여 프로토콜을 준수할 수 있습니다.*  

*The example below defines an enumeration called `OnOffSwitch`. This enumeration toggles between two states, indicated by the enumeration cases `on` and `off`. The enumeration’s `toggle` implementation is marked as `mutating`, to match the `Togglable` protocol’s requirements:*

아래 예제에서는 `OnOffSwitch`라는 열거형을 정의합니다. 이 열거형은 케이스 `on`과 `off`로 표시되는 두 상태를 전환합니다. 열거형의 `toggle` 구현은 `toggle` 프로토콜의 요구 사항과 일치하도록 mutating으로 표시됩니다:

```swift
enum OnOffSwitch: Togglable {
    case off, on
    mutating func toggle() {
        switch self {
        case .off:
            self = .on
        case .on:
            self = .off
        }
    }
}
var lightSwitch = OnOffSwitch.off
lightSwitch.toggle()
// lightSwitch is now equal to .on
```
