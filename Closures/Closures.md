# *Closures : 클로저*

*Closures are self-contained blocks of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and to lambdas in other programming languages.*

클로저는 코드에서 전달하고 사용할 수 있는 독립적인 기능 블록입니다. Swift의 클로저는 C와 Objective-C의 블록과 유사하며 다른 프로그래밍 언어의 람다와 유사합니다.

*Closures can capture and store references to any constants and variables from the context in which they’re defined. This is known as closing over those constants and variables. Swift handles all of the memory management of capturing for you.*

클로저는 상수 및 변수가 정의된 컨텍스트에서 해당 상수 및 변수에 대한 참조를 캡쳐하고 저장할 수 있습니다. 이를 상수 및 변수에 대한 닫힘이라고 합니다. Swift는 캡쳐의 모든 메모리 관리를 처리합니다.

> *NOTE*
> 
> *Don’t worry if you aren’t familiar with the concept of capturing. It’s explained in detail below in [Capturing Values](https://docs.swift.org/swift-book/LanguageGuide/Closures.html#ID103).*
> 
> 캡처 개념에 대해서 익숙하지 않더라도 걱정하지 마십시오. 아래의 [링크]에 자세히 설명되어있습니다.

*Global and nested functions, as introduced in [Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html), are actually special cases of closures. Closures take one of three forms:*

[링크]에 소개된 전역 및 중첩함수는 실제로 클로저의 특수한 경우입니다. 클로저는 다음 세가지 형태 중 하나로 이루어집니다.

- *Global functions are closures that have a name and don’t capture any values.*
  
  전역 함수는 이름이 있고 값을 캡처하지 않는 클로저입니다.

- *Nested functions are closures that have a name and can capture values from their enclosing function.*
  
  중첩 함수는 이름이 있는 클로저 함수이며 내포한 함수에서 값을 캡처할 수 있습니다.

- *Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.*
  
  클로저 표현식은 주변 컨텍스트에서 값을 캡쳐할 수 있는 경량 구문으로 작성된 이름 없는 클로저입니다.

*Swift’s closure expressions have a clean, clear style, with optimizations that encourage brief, clutter-free syntax in common scenarios. These optimizations include:*

Swift의 클로저 표현은 일반적인 시나리오에서 간결하고 어수선하지 않은 구문을 권장하는 최적화와 함께 깨끗하고 명확한 스타일을 가지고 있습니다. 이러한 최적화에는 다음이 포함됩니다 :

- *Inferring parameter and return value types from context*
  
  콘텍스트에서 매개변수 및 반환값 타입을 유추합니다.

- *Implicit returns from single-expression closures*
  
  단일 표현식 클로저로 인한 암묵적인 반환합니다.

- *Shorthand argument names*
  
  단축 인수 이름

- *Trailing closure syntax*
  
  후행 클로저 구문


