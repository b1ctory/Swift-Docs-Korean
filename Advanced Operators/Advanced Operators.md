# *Advanced Operators : 고급 연산자*

*Define custom operators, perform bitwise operations, and use builder syntax.*

사용자 지정 연산자를 정의하고, 비트 연산을 수행하며, 빌더 구문을 사용합니다.

*In addition to the operators described in [Basic Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators), Swift provides several advanced operators that perform more complex value manipulation. These include all of the bitwise and bit shifting operators you will be familiar with from C and Objective-C.*

Swift는 [링크]에 설명된 연산자 외에도 보다 복잡한 값 조작을 수행하는 여러 고급 연산자를 제공합니다. 여기에는 C 및 Objective-C의 모든 비트 단위 및 비트 이동 연산자가 포함됩니다.

*Unlike arithmetic operators in C, arithmetic operators in Swift don’t overflow by default. Overflow behavior is trapped and reported as an error. To opt in to overflow behavior, use Swift’s second set of arithmetic operators that overflow by default, such as the overflow addition operator (`&+`). All of these overflow operators begin with an ampersand (`&`).*

C의 산술 연산자와 달리 Swift의 산술 연산자는 기본적으로 오버플로되지 않습니다. 오버플로 동작이 트랩되어 오류로 보고됩니다. 오버플로 동작을 선택하려면 오버플로 덧셈 연산자(`&+`)와 같이 기본적으로 오버플로되는 Swift의 두 번째 산술 연산자 집합을 사용합니다. 이러한 모든 오버플로 연산자는 앰퍼샌드(`&`)로 시작합니다.

*When you define your own structures, classes, and enumerations, it can be useful to provide your own implementations of the standard Swift operators for these custom types. Swift makes it easy to provide tailored implementations of these operators and to determine exactly what their behavior should be for each type you create.*

자체 구조체, 클래스 및 열거형을 정의할 때 이러한 사용자 정의 타입에 대한 표준 Swift 연산자의 자체 구현을 제공하는 것이 유용할 수 있습니다. Swift를 사용하면 이러한 연산자의 맞춤형 구현을 쉽게 제공하고 생성하는 각 타입에 대해 연산자의 동작을 정확하게 결정할 수 있습니다.*

*You’re not limited to the predefined operators. Swift gives you the freedom to define your own custom infix, prefix, postfix, and assignment operators, with custom precedence and associativity values. These operators can be used and adopted in your code like any of the predefined operators, and you can even extend existing types to support the custom operators you define.*

사전 정의된 연산자로 제한되지 않습니다. Swift를 사용하면 사용자 지정 우선 순위 및 연관 값을 사용하여 사용자 지정 중위, 접두사, 후위 및 대입 연산자를 자유롭게 정의할 수 있습니다. 이러한 연산자는 미리 정의된 연산자와 마찬가지로 코드에서 사용 및 채택될 수 있으며, 기존 타입을 확장하여 정의한 사용자 정의 연산자를 지원할 수도 있습니다.
