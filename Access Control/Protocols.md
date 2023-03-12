## *Protocols : 프로토콜*

*If you want to assign an explicit access level to a protocol type, do so at the point that you define the protocol. This enables you to create protocols that can only be adopted within a certain access context.*

프로토콜 탸입에 명시적 액세스 레벨을 할당하려면 프로토콜을 정의하는 지점에서 지정하세요. 이렇게 하면 특정 액세스 컨텍스트 내에서만 채택할 수 있는 프로토콜을 만들 수 있습니다.

*The access level of each requirement within a protocol definition is automatically set to the same access level as the protocol. You can’t set a protocol requirement to a different access level than the protocol it supports. This ensures that all of the protocol’s requirements will be visible on any type that adopts the protocol.*

프로토콜 정의 내 각 요구사항의 액세스 레벨은 프로토콜과 동일한 액세스 레벨로 자동 설정됩니다. 프로토콜 요구사항을 지원하는 프로토콜과 다른 액세스 레벨로 설정할 수 없습니다. 이렇게 하면 프로토콜을 채택하는 모든 타입에서 프로토콜의 모든 요구사항을 볼 수 있습니다.

> *Note*
> 
> *If you define a public protocol, the protocol’s requirements require a public access level for those requirements when they’re implemented. This behavior is different from other types, where a public type definition implies an access level of internal for the type’s members.*
> 
> 공개 프로토콜을 정의하는 경우 프로토콜의 요구사항은 구현 시 해당 요구사항에 대한 공개 액세스 레벨을 요구합니다. 이 동작은 퍼블릭 타입 정의가 타입의 구성원에 대한 내부 액세스 레벨을 의미하는 다른 타입과 다릅니다.

### *Protocol Inheritance : 프로토콜 상속*

*If you define a new protocol that inherits from an existing protocol, the new protocol can have at most the same access level as the protocol it inherits from. For example, you can’t write a public protocol that inherits from an internal protocol.*

기존 프로토콜에서 상속되는 새 프로토콜을 정의하는 경우, 새 프로토콜은 상속되는 프로토콜과 최대 동일한 액세스 레벨을 가질 수 있습니다. 예를 들어, 내부 프로토콜에서 상속되는 퍼블릭 프로토콜을 작성할 수 없습니다.

### *Protocol Conformance : 프로토콜 적합성*

*A type can conform to a protocol with a lower access level than the type itself. For example, you can define a public type that can be used in other modules, but whose conformance to an internal protocol can only be used within the internal protocol’s defining module.*

타입은 타입 자체보다 낮은 액세스 레벨의 프로토콜을 준수할 수 있습니다. 예를 들어, 다른 모듈에서 사용할 수 있지만 내부 프로토콜에 대한 적합성은 내부 프로토콜의 정의 모듈 내에서만 사용할 수 있는 퍼블릭 타입을 정의할 수 있습니다.

*The context in which a type conforms to a particular protocol is the minimum of the type’s access level and the protocol’s access level. For example, if a type is public, but a protocol it conforms to is internal, the type’s conformance to that protocol is also internal.*

타입이 특정 프로토콜을 준수하는 컨텍스트는 타입의 액세스 레벨과 프로토콜의 액세스 레벨 중 최소값입니다. 예를 들어, 타입이 퍼블릭이지만 이 타입이 준수하는 프로토콜이 내부인 경우 해당 프로토콜에 대한 타입의 준수도 내부입니다.

*When you write or extend a type to conform to a protocol, you must ensure that the type’s implementation of each protocol requirement has at least the same access level as the type’s conformance to that protocol. For example, if a public type conforms to an internal protocol, the type’s implementation of each protocol requirement must be at least internal.*

프로토콜을 준수하도록 타입을 작성하거나 확장할 때, 각 프로토콜 요구사항에 대한 타입의 구현이 해당 프로토콜에 대한 타입의 준수와 최소한 동일한 액세스 레벨을 갖도록 해야 합니다. 예를 들어, 퍼블릭 타입이 내부 프로토콜을 준수하는 경우 각 프로토콜 요구사항에 대한 타입의 구현은 적어도 내부여야 합니다.

> *Note*
> 
> *In Swift, as in Objective-C, protocol conformance is global — it isn’t possible for a type to conform to a protocol in two different ways within the same program.*
> 
> Objective-C에서와 같이 Swift에서 프로토콜 적합성은 글로벌합니다. 타입이 동일한 프로그램 내에서 두 가지 다른 방식으로 프로토콜을 준수하는 것은 불가능합니다.


