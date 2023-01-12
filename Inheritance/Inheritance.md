# *Inheritance : 상속*

*A class can inherit methods, properties, and other characteristics from another class. When one class inherits from another, the inheriting class is known as a subclass, and the class it inherits from is known as its superclass. Inheritance is a fundamental behavior that differentiates classes from other types in Swift.*

클래스는 다른 클래스에서 메서드, 프로퍼티 및 기타 특성을 상속할 수 있습니다. 한 클래스가 다른 클래스에서 상속되는 경우 상속받는 클래스를 하위 클래스라고 하며 상속하는 클래스를 슈퍼 클래스라고 합니다. 상속은 Swift의 다른 타입과 클래스를 차별화하는 기본 동작입니다.

*Classes in Swift can call and access methods, properties, and subscripts belonging to their superclass and can provide their own overriding versions of those methods, properties, and subscripts to refine or modify their behavior. Swift helps to ensure your overrides are correct by checking that the override definition has a matching superclass definition.*

Swift의 클래스는 슈퍼 클래스에 속하는 메서드, 프로퍼티 및 서브스크립트를 호출하고 액세스할 수 있으며 이러한 메서드, 프로퍼티 및 서브스크립트의 우선 버전을 제공하여 동작을 세분화하거나 수정할 수 있습니다. Swift는 재정의 정의에 일치하는 슈퍼클래스 정의가 있는지 확인하여 재정의가 올바른지 확인하는 데 도움이 됩니다.

*Classes can also add property observers to inherited properties in order to be notified when the value of a property changes. Property observers can be added to any property, regardless of whether it was originally defined as a stored or computed property.*

클래스는 프로퍼티 값이 변경될 때 알림을 받기 위해 상속된 프로퍼티에 프로퍼티 옵저버를 추가할 수도 있습니다. 프로퍼티 옵저버는 원래 프로퍼티가 저장 프로퍼티로 정의되었는지 연산 프로퍼티로 정의되었는지에 관계없이 모든 프로퍼티에 추가할 수 있습니다.
