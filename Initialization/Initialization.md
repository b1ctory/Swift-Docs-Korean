# *Initialization : 초기화*

*Initialization is the process of preparing an instance of a class, structure, or enumeration for use. This process involves setting an initial value for each stored property on that instance and performing any other setup or initialization that’s required before the new instance is ready for use.*

초기화는 클래스, 구조체 또는 열거의 인스턴스를 사용하기 위해 준비하는 프로세스입니다. 이 프로세스에는 해당 인스턴스에 저장된 각 프로퍼티의 초기 값을 설정하고 새 인스턴스를 사용할 준비가 되기 전에 필요한 다른 설정 또는 초기화를 수행하는 작업이 포함됩니다.

*You implement this initialization process by defining initializers, which are like special methods that can be called to create a new instance of a particular type. Unlike Objective-C initializers, Swift initializers don’t return a value. Their primary role is to ensure that new instances of a type are correctly initialized before they’re used for the first time.*

특정 타입의 새 인스턴스를 만들기 위해 호출할 수 있는 특수 메서드와 같은 초기화 프로세스를 정의하여 이 초기화 프로세스를 구현합니다. Objective-C 이니셜라이저와 달리 Swift 이니셜라이저는 값을 반환하지 않습니다. 기본적인 역할은 처음 사용하기 전에 타입의 새 인스턴스가 올바르게 초기화되도록 하는 것입니다.

*Instances of class types can also implement a deinitializer, which performs any custom cleanup just before an instance of that class is deallocated. For more information about deinitializers, see [Deinitialization](https://docs.swift.org/swift-book/LanguageGuide/Deinitialization.html).*

클래스 타입의 인스턴스는 해당 클래스의 인스턴스 할당이 해제되기 직전에 사용자 지정 정리를 수행하는 초기화 해제자를 구현할 수도 있습니다. 초기화 해제에 대한 자세한 내용은 [링크]를 참조하세요.
