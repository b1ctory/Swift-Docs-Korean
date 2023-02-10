## *Property Requirements : 프로퍼티 요구사항*

*A protocol can require any conforming type to provide an instance property or type property with a particular name and type. The protocol doesn’t specify whether the property should be a stored property or a computed property—it only specifies the required property name and type. The protocol also specifies whether each property must be gettable or gettable and settable.*

프로토콜은 특정 이름과 타입을 가진 인스턴스 프로퍼티 또는 타입 프로퍼티를 제공하기 위해 모든 적합한 타입을 요구할 수 있습니다. 프로토콜은 프로퍼티가 저장 프로퍼티인지 연산 프로퍼티인지를 지정하지 않고 필요한 이름과 타입만 지정합니다.또한 프로토콜은 각 속성이 gettable이어야 하는지 gettable 및 settable이어야 하는지도 지정합니다.

*If a protocol requires a property to be gettable and settable, that property requirement can’t be fulfilled by a constant stored property or a read-only computed property. If the protocol only requires a property to be gettable, the requirement can be satisfied by any kind of property, and it’s valid for the property to be also settable if this is useful for your own code.*

프로토콜에서 설정 가능한 프로퍼티가 필요한 경우, 해당 프로퍼티 요구사항은 지속적으로 저장프로퍼티나 읽기 전용 연산 프로퍼티로 충족될 수 없습니다. 프로토콜이 gettable 프로퍼티만 필요로 하는 경우 모든 종류의 프로퍼티에서 요구 사항을 충족할 수 있으며, 사용자 코드에 유용한 경우 프로퍼티도 설정할 수 있습니다.

*Property requirements are always declared as variable properties, prefixed with the `var` keyword. Gettable and settable properties are indicated by writing `{ get set }` after their type declaration, and gettable properties are indicated by writing `{ get }`.*

프로퍼티 요구사항은 항상 변수 프로퍼티로 선언되며 `var` 키워드가 앞에 붙습니다. Gettable과 settable 프로퍼티는 타입 선언 뒤에 `{get set}`을 작성하여 표시하고, Gettable 속성은 `{ get }`를 작성하여 표시합니다.

```swift
protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
}
```

*Always prefix type property requirements with the `static` keyword when you define them in a protocol. This rule pertains even though type property requirements can be prefixed with the `class` or `static` keyword when implemented by a class:*

프로토콜에서 프로퍼티 요구사항을 정의할 때는 항상 `static` 키워드를 사용하여 프로퍼티 타입 요구사항을 접두사로 붙여야 합니다. 이 규칙은 타입 프로퍼티 요구사항이 클래스에 의해 구현될 때 `class` 또는 `static` 키워드로 접두사가 붙을 수 있는 경우에도 적용됩니다.

```swift
protocol AnotherProtocol {
    static var someTypeProperty: Int { get set }
}
```

*Here’s an example of a protocol with a single instance property requirement:*

다음은 단일 인스턴스 프로퍼티 요구사항이 있는 프로토콜의 예입니다:

```swift
protocol FullyNamed {
    var fullName: String { get }
}
```

*The `FullyNamed` protocol requires a conforming type to provide a fully qualified name. The protocol doesn’t specify anything else about the nature of the conforming type—it only specifies that the type must be able to provide a full name for itself. The protocol states that any `FullyNamed` type must have a gettable instance property called `fullName`, which is of type `String`.*

`FullyNamed` 프로토콜에는 정규화된 이름을 제공하기 위해 준수 타입이 필요합니다. 프로토콜은 준수 타입의 특성에 대해 다른 어떤 것도 지정하지 않습니다. 단지 타입이 전체 이름을 제공할 수 있어야 한다는 것만 지정합니다. 프로토콜에 따르면 모든 `FullyNamed` 타입에는 `String` 타입인 `fullName`이라는 gettable 인스턴스 프로퍼티가 있어야 합니다.

*Here’s an example of a simple structure that adopts and conforms to the `FullyNamed` protocol:*

다음은 `FullyNamed` 프로토콜을 채택하고 준수하는 간단한 구조의 예입니다.

```swift
struct Person: FullyNamed {
    var fullName: String
}
let john = Person(fullName: "John Appleseed")
// john.fullName is "John Appleseed"
```

*This example defines a structure called `Person`, which represents a specific named person. It states that it adopts the `FullyNamed` protocol as part of the first line of its definition.*

이 예는 이름이 지정된 특정 사람을 나타내는 `Person`이라는 구조체를 정의합니다. 정의의 첫 번째 줄의 일부로 `FullyNamed` 프로토콜을 채택한다고 명시되어 있습니다.

*Each instance of `Person` has a single stored property called `fullName`, which is of type `String`. This matches the single requirement of the `FullyNamed` protocol, and means that `Person` has correctly conformed to the protocol. (Swift reports an error at compile time if a protocol requirement isn’t fulfilled.)*

`Person`의 각 인스턴스에는 `String` 타입인 `fullName`이라는 단일 저장 프로퍼티가 있습니다. 이는 `FullyNamed` 프로토콜의 단일 요구 사항과 일치하며 `Person`이 프로토콜을 올바르게 준수했음을 의미합니다. (Swift는 프로토콜 요구 사항이 충족되지 않으면 컴파일 타임에 오류를 보고합니다.)

*Here’s a more complex class, which also adopts and conforms to the `FullyNamed` protocol:*

다음은 `FullyNamed` 프로토콜을 채택하고 준수하는 보다 복잡한 클래스입니다.

```swift
class Starship: FullyNamed {
    var prefix: String?
    var name: String
    init(name: String, prefix: String? = nil) {
        self.name = name
        self.prefix = prefix
    }
    var fullName: String {
        return (prefix != nil ? prefix! + " " : "") + name
    }
}
var ncc1701 = Starship(name: "Enterprise", prefix: "USS")
// ncc1701.fullName is "USS Enterprise"
```

*This class implements the `fullName` property requirement as a computed read-only property for a starship. Each `Starship` class instance stores a mandatory `name` and an optional `prefix`. The `fullName` property uses the `prefix` value if it exists, and prepends it to the beginning of `name` to create a full name for the starship.*

이 클래스는 우주선에 대해 계산된 읽기 전용 프로퍼티로 `fullName` 프로퍼티 요구사항을 구현합니다. 각 `Starship` 클래스 인스턴스는 필수 `name`과 옵셔널 `prefix`를 저장합니다. `fullName` 프로퍼티는 `prefix` 값이 있는 경우 이를 사용하고 우주선의 전체 이름을 생성하기 위해 `name` 앞에 추가합니다.
