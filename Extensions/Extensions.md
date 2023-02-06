# *Extensions : 확장*

*Extensions add new functionality to an existing class, structure, enumeration, or protocol type. This includes the ability to extend types for which you don’t have access to the original source code (known as retroactive modeling). Extensions are similar to categories in Objective-C. (Unlike Objective-C categories, Swift extensions don’t have names.)*

확장 기능은 기존 클래스, 구조체, 열거형 또는 프로토콜 타입에 새 기능을 추가합니다. 여기에는 원본 소스 코드에 액세스할 수 없는 유형(회귀 모델링이라고 함)을 확장할 수 있는 기능이 포함됩니다. 확장명은 Objective-C의 카테고리와 유사합니다. (Objective-C 범주와 달리 Swift 확장명에는 이름이 없습니다.)

*Extensions in Swift can:*

Swift의 확장 기능은 다음을 할 수 있습니다:

- *Add computed instance properties and computed type properties*
  
  연산 인스턴스 프로퍼티 및 연산 타입 프로퍼티를 추가합니다.

- *Define instance methods and type methods*
  
  인스턴스 메서드 및 타입 메서드를 정의합니다.

- *Provide new initializers*
  
  새로운 이니셜라이저를 제공합니다.

- *Define subscripts*
  
  서브스크립트를 정의합니다. 

- *Define and use new nested types*
  
  새로운 중첩 타입을 정의하고 사용합니다.

- *Make an existing type conform to a protocol*
  
  기존 타입이 프로토콜을 준수하도록 합니다.

*In Swift, you can even extend a protocol to provide implementations of its requirements or add additional functionality that conforming types can take advantage of. For more details, see [Protocol Extensions](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html#ID521).*

Swift에서는 프로토콜을 확장하여 요구사항의 구현을 제공하거나 적합한 타입을 활용할 수 있는 추가 기능을 추가할 수도 있습니다. 자세한 내용은 [링크]를 참조하세요.

> *NOTE*
> 
> *Extensions can add new functionality to a type, but they can’t override existing functionality.*
> 
> 확장 기능은 타입에 새 기능을 추가할 수 있지만 기존 기능을 재정의할 수는 없습니다.
