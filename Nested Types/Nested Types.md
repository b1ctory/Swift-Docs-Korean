# *Nested Types: 중첩 타입*

*Enumerations are often created to support a specific class or structure’s functionality. Similarly, it can be convenient to define utility classes and structures purely for use within the context of a more complex type. To accomplish this, Swift enables you to define nested types, whereby you nest supporting enumerations, classes, and structures within the definition of the type they support.*

특정 클래스 또는 구조체의 기능을 지원하기 위해 열거형이 생성되는 경우가 많습니다. 마찬가지로, 더 복잡한 타입의 컨텍스트 내에서 사용하기 위해 유틸리티 클래스와 구조체를 정의하는 것이 편리할 수 있습니다. 이를 위해 Swift를 사용하면 중첩 타입을 정의할 수 있으며, 이를 통해 지원하는 열거형, 클래스 및 구조체를 지원하는 타입의 정의 내에 중첩할 수 있습니다.

*To nest a type within another type, write its definition within the outer braces of the type it supports. Types can be nested to as many levels as are required.*

다른 타입 내에 타입 중첩하려면 해당 타입 지원하는 유형의 바깥쪽 괄호 안에 정의를 작성합니다. 유형은 필요한 수의 수준으로 중첩될 수 있습니다.
