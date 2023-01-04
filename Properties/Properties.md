# *Properties : 프로퍼티*

*Properties associate values with a particular class, structure, or enumeration. Stored properties store constant and variable values as part of an instance, whereas computed properties calculate (rather than store) a value. Computed properties are provided by classes, structures, and enumerations. Stored properties are provided only by classes and structures.*

프로퍼티는 값을 특정 클래스 , 구조체 혹은 열거형과 연결합니다. 저장 프로퍼티는 상수 및 변수 값을 인스턴스의 일부로 저장하는 반면 연산 프로퍼티는 값을 (저장하지 않고) 계산합니다. 연산 프로퍼티는 클래스, 구조체, 열거형에 의해 제공됩니다. 저장 프로퍼티는 클래스 및 구조체에서만 제공됩니다. 

*Stored and computed properties are usually associated with instances of a particular type. However, properties can also be associated with the type itself. Such properties are known as type properties.*

저장 및 연산 프로퍼티는 일반적으로 특정 타입의 인스턴스와 연결됩니다. 그러나 프로퍼티는 타입 자체와 연결될 수도 있습니다. 이러한 프로퍼티는 타입 프로퍼티라고 합니다. 

*In addition, you can define property observers to monitor changes in a property’s value, which you can respond to with custom actions. Property observers can be added to stored properties you define yourself, and also to properties that a subclass inherits from its superclass.*

또한 프로퍼티 관찰자를 정의해서 프로퍼티 값의 변경 사항을 모니터링할 수 있으며, 이에 대해 사용자 지정 작업으로 대응할 수 있습니다. 프로퍼티 관찰자는 사용자가 직접 정의한 저장 프로퍼티와 하위 클래스가 해당 슈퍼 클래스에서 상속하는 프로퍼티에 추가할 수 있습니다.

*You can also use a property wrapper to reuse code in the getter and setter of multiple properties.*

또한 프로퍼티 래퍼를 사용해서 여러 프로퍼티의 getter 및 setter에서 코드를 재사용할 수 있습니다. 
