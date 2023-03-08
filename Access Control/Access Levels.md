## *Access Levels : 접근레벨*

*Swift provides five different access levels for entities within your code. These access levels are relative to the source file in which an entity is defined, and also relative to the module that source file belongs to.*

Swift는 코드 내 엔티티에 대해 5가지 액세스 수준을 제공합니다. 이러한 액세스 수준은 엔티티가 정의된 원본 파일에 상대적이며 원본 파일이 속한 모듈에도 상대적입니다.

- *Open access and public access enable entities to be used within any source file from their defining module, and also in a source file from another module that imports the defining module. You typically use open or public access when specifying the public interface to a framework. The difference between open and public access is described below.*
  
  오픈 액세스 및 퍼블릭 액세스를 통해 엔티티를 정의 모듈의 모든 소스 파일 내에서 사용할 수 있으며 정의 모듈을 가져오는 다른 모듈의 소스 파일에서도 사용할 수 있습니다. 일반적으로 프레임워크에 대한 공용 인터페이스를 지정할 때 열린 액세스 또는 공용 액세스를 사용합니다. 오픈 액세스와 퍼블릭 액세스의 차이점은 아래에 설명되어 있습니다.

- *Internal access enables entities to be used within any source file from their defining module, but not in any source file outside of that module. You typically use internal access when defining an app’s or a framework’s internal structure.*
  
  내부 액세스를 통해 엔티티를 정의 모듈의 소스 파일 내에서 사용할 수 있지만 해당 모듈 외부의 소스 파일에서는 사용할 수 없습니다. 일반적으로 앱 또는 프레임워크의 내부 구조를 정의할 때 내부 액세스를 사용합니다.

- *File-private access restricts the use of an entity to its own defining source file. Use file-private access to hide the implementation details of a specific piece of functionality when those details are used within an entire file.*
  
  파일-프라이빗 액세스는 엔티티의 사용을 자체 정의 소스 파일로 제한합니다. 특정 기능의 구현 세부 정보가 전체 파일 내에서 사용되는 경우 파일-프라이빗 액세스를 사용하여 해당 기능의 구현 세부 정보를 숨깁니다.

- *Private access restricts the use of an entity to the enclosing declaration, and to extensions of that declaration that are in the same file. Use private access to hide the implementation details of a specific piece of functionality when those details are used only within a single declaration.*
  
  프라이빗 액세스는 엔티티의 사용을 동봉한 선언과 동일한 파일에 있는 선언의 확장자로 제한합니다. 특정 기능의 구현 세부 정보가 단일 선언 내에서만 사용되는 경우 프라이빗 액세스를 사용하여 해당 기능의 구현 세부 정보를 숨깁니다.

*Open access is the highest (least restrictive) access level and private access is the lowest (most restrictive) access level.*

ㅇㅎ푼 액세스는 가장 높은(제한성이 낮은) 액세스 수준이며, 개인 액세스는 가장 낮은(제한성이 높은) 액세스 수준입니다.

*Open access applies only to classes and class members, and it differs from public access by allowing code outside the module to subclass and override, as discussed below in [Subclassing](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol#Subclassing). Marking a class as open explicitly indicates that you’ve considered the impact of code from other modules using that class as a superclass, and that you’ve designed your class’s code accordingly.*

오픈 액세스는 클래스 및 클래스 멤버에게만 적용되며, 아래 [Subclassing](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol#Subclassing)에서 설명한 바와 같이 모듈 외부의 코드를 서브클래스 및 오버라이드 할 수 있도록 하는 등 퍼블릭액세스와 다릅니다. 클래스를 열림으로 명시적으로 표시하면 해당 클래스를 수퍼 클래스로 사용하는 다른 모듈의 코드 영향을 고려했으며 이에 따라 클래스의 코드를 설계했음을 나타냅니다.

### *Guiding Principle of Access Levels : 접근 수준의 원칙 안내*

*Access levels in Swift follow an overall guiding principle: No entity can be defined in terms of another entity that has a lower (more restrictive) access level.*

Swift의 액세스 레벨은 전반적인 안내 원칙을 따릅니다. 더 낮은(더 제한적인) 액세스 수준을 가진 다른 엔티티의 관점에서 정의할 수 없습니다.

*For example:*

예를 들어 :

- *A public variable can’t be defined as having an internal, file-private, or private type, because the type might not be available everywhere that the public variable is used.*
  
  공용 변수는 내부, 파일-프라이빗 또는 프라이빗 타입을 갖는 것으로 정의할 수 없습니다. 공용 변수가 사용되는 모든 위치에서 해당 타입을 사용할 수는 없기 때문입니다.

- *A function can’t have a higher access level than its parameter types and return type, because the function could be used in situations where its constituent types are unavailable to the surrounding code.*
  
  함수는 매개변수 타입 및 반환 타입보다 높은 액세스 수준을 가질 수 없습니다. 왜냐하면 함수의 구성 요소 타입을 주변 코드에서 사용할 수 없는 상황에서 사용될 수 있기 때문입니다.

*The specific implications of this guiding principle for different aspects of the language are covered in detail below.*

언어의 다양한 측면에 대한 이 안내 원칙의 구체적인 의미는 아래에서 자세히 다룹니다.
