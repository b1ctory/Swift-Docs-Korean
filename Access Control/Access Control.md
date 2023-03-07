# *Access Control : 접근 제어*

*Manage the visibility of code by declaration, file, and module.*

선언, 파일, 모듈별로 코드의 가시성을 관리합니다.

*Access control restricts access to parts of your code from code in other source files and modules. This feature enables you to hide the implementation details of your code, and to specify a preferred interface through which that code can be accessed and used.*

접근 제어는 다른 소스 파일 및 모듈의 코드에서 코드의 일부에 대한 액세스를 제한합니다. 이 기능을 사용하면 코드의 구현 세부 정보를 숨기고 해당 코드에 액세스하고 사용할 수 있는 기본 인터페이스를 지정할 수 있습니다.

*You can assign specific access levels to individual types (classes, structures, and enumerations), as well as to properties, methods, initializers, and subscripts belonging to those types. Protocols can be restricted to a certain context, as can global constants, variables, and functions.*

개별 타입(클래스, 구조체 및 열거형)뿐만 아니라 이러한 타입에 속하는 프로퍼티, 메서드, 이니셜라이저 및 서브스크립트에 특정 액세스 수준을 할당할 수 있습니다. 전역 상수, 변수 및 함수와 마찬가지로 프로토콜을 특정 컨텍스트로 제한할 수 있습니다.

*In addition to offering various levels of access control, Swift reduces the need to specify explicit access control levels by providing default access levels for typical scenarios. Indeed, if you are writing a single-target app, you may not need to specify explicit access control levels at all.*

Swift는 다양한 수준의 접근 제어를 제공하는 것 외에도 일반적인 시나리오에 대한 기본 액세스 수준을 제공하여 명시적인 접근 제어 수준을 지정할 필요성을 줄입니다. 실제로 단일 대상 앱을 작성하는 경우 명시적인 액세스 제어 수준을 전혀 지정할 필요가 없을 수 있습니다.

> *Note*
> 
> *The various aspects of your code that can have access control applied to them (properties, types, functions, and so on) are referred to as “entities” in the sections below, for brevity.*
> 
> 접근 제어를 적용할 수 있는 코드의 다양한 측면(프로퍼티, 타입, 함수 등)은 간결성을 위해 아래 섹션에서 "엔티티"라고 합니다.


