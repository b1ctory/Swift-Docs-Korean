# *Basic Operators : 기본 연산자*

*An operator is a special symbol or phrase that you use to check, change, or combine values. For example, the addition operator (`+`) adds two numbers, as in `let i = 1 + 2`, and the logical AND operator (`&&`) combines two Boolean values, as in `if enteredDoorCode && passedRetinaScan`.*

연산자는 값을 확인, 변경 혹은 결합하는데 사용하는 특수 기호 혹은 구문입니다. 예를 들어, 덧셈 연산자 (+)는 `let i = 1 + 2` 와 같이 두 개의 숫자를 더하고, 논리 AND 연산자 (&&)는 `if enteredDoorCode && passedRetinaScan` 와 같이 두 개의 Bool 값을 결합합니다.



*Swift supports the operators you may already know from languages like C, and improves several capabilities to eliminate common coding errors. The assignment operator (`=`) doesn’t return a value, to prevent it from being mistakenly used when the equal to operator (`==`) is intended.*  *Arithmetic operators (`+`, `-`, `*`, `/`, `%` and so forth) detect and disallow value overflow, to avoid unexpected results when working with numbers that become larger or smaller than the allowed value range of the type that stores them. You can opt in to value overflow behavior by using Swift’s overflow operators, as described in [Overflow Operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID37).*

Swift는 C와 같은 언어를 통해 미리 알고있는 연산자를 지원하며, 일반적인 코딩 오류를 제거하기 위해 몇 가지 기능을 개선합니다. 할당 연산자 (=)은 등호 연산자 (==)를 사용할 때 실수로 사용되는 것을 방지하기 위해 값을 반환하지 않습니다. 산술 연산자 (`+`, `-`, `*`, `/`, `%` 등) 는 값을 저장하는 타입의 허용값 범위보다 크거나 작은 숫자로 작업할 때 예기치 않은 결과를 피하기 위해 값 오버플로우를 감지하고 허용하지 않습니다. [링크]에 설명된대로 Swift의 오버플로우 연산자를 사용하여 오버플로우 동작을 선택할 수 있습니다.



*Swift also provides range operators that aren’t found in C, such as `a..<b` and `a...b`, as a shortcut for expressing a range of values.*

Swift는 또한 값의 범위를 표현하는 지름길로서  `a..<b` and `a...b` 와 같이 C언어에서는 찾을 수 없는 범위 연산자를 제공합니다.



*This chapter describes the common operators in Swift. [Advanced Operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html) covers Swift’s advanced operators, and describes how to define your own custom operators and implement the standard operators for your own custom types.*

이 챕터에서는 Swift의 기본 연산자에 대해 설명합니다. [링크]에서는 Swift의 고급 연산자에 대해 설명하고, 사용자 정의 연산자를 정의하고 사용자 정의 타입에 맞는 표준 연산자를 구현하는 방법을 설명합니다.
