## *Initializers : 이니셜라이저*

*Custom initializers can be assigned an access level less than or equal to the type that they initialize. The only exception is for required initializers (as defined in [Required Initializers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization#Required-Initializers)). A required initializer must have the same access level as the class it belongs to.*

사용자 정의 이니셜라이저에는 초기화하는 타입보다 작거나 같은 액세스 레벨이 할당될 수 있습니다. 유일한 예외는 필수 Initializer([링크]에 정의되어 있음)입니다. 필수 이니셜라이저는 해당 클래스와 동일한 액세스 수준을 가져야 합니다.

*As with function and method parameters, the types of an initializer’s parameters can’t be more private than the initializer’s own access level.*

함수 및 메서드 매개 변수와 마찬가지로 Initializer의 매개 변수 타입은 Initializer 자신의 액세스 레벨보다 프라이빗일 수 없습니다.

### *Default Initializers : 기본 이니셜라이저*

*As described in [Default Initializers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization#Default-Initializers), Swift automatically provides a default initializer without any arguments for any structure or base class that provides default values for all of its properties and doesn’t provide at least one initializer itself.*

[링크]에서 설명한 바와 같이 Swift는 모든 속성에 기본값을 제공하고 하나 이상의 Initializer 자체를 제공하지 않는 구조체 또는 기본 클래스에 대해 인수 없이 자동으로 기본 이니셜라이저를 제공합니다.

*A default initializer has the same access level as the type it initializes, unless that type is defined as `public`. For a type that’s defined as `public`, the default initializer is considered internal. If you want a public type to be initializable with a no-argument initializer when used in another module, you must explicitly provide a public no-argument initializer yourself as part of the type’s definition.*

기본 이니셜라이저는 `public`으로 정의되지 않는 한 초기화하는 타입과 동일한 액세스 수준을 가집니다. `public`으로 정의된 타입의 경우 기본 이니셜라이저는 내부로 간주됩니다. 다른 모듈에서 사용할 때 인수 없는 이니셜라이저로 공용 타입을 초기화하려면 타입 정의의 일부로 인수 없는 이니셜라이저를 명시적으로 제공해야 합니다.

### *Default Memberwise Initializers for Structure Types : 구조체 타입에 대한 기본 멤버와이즈 이니셜라이저*

*The default memberwise initializer for a structure type is considered private if any of the structure’s stored properties are private. Likewise, if any of the structure’s stored properties are file private, the initializer is file private. Otherwise, the initializer has an access level of internal.*

구조체 타입의 기본 멤버와이즈 이니셜라이저는 구조체의 저장프로퍼티 중 하나라도 비공개인 경우 프라이빗으로 간주됩니다. 마찬가지로 구조체의 저장프로퍼티가 파일-프라이빗이면 초기화 프로그램은 파일-프라이빗입니다. 그렇지 않으면 이니셜라이저의 액세스 수준이 내부입니다.

*As with the default initializer above, if you want a public structure type to be initializable with a memberwise initializer when used in another module, you must provide a public memberwise initializer yourself as part of the type’s definition.*

위의 기본 이니셜라이저와 마찬가지로 다른 모듈에서 사용할 때 공용 구조체 타입을 멤버와이즈 이니셜라이저로 초기화하려면 타입 정의의 일부로 공용 멤버와이즈 이니셜라이저를 직접 제공해야 합니다.


