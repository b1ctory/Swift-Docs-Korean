## *Strings and Characters : 문자열과 문자*

*A string is a series of characters, such as `"hello, world"` or `"albatross"`. Swift strings are represented by the `String` type. The contents of a `String` can be accessed in various ways, including as a collection of `Character` values.*

문자열은 `"hello, world"` or `"albatross"`와 같은 일련의 문자들입니다. Swift에서 string은 String 타입으로 표현됩니다. 문자열의 내용은 `Character` 값의 집합을 포함하여 다양한 방법으로 접근할 수 있습니다. 

*Swift’s `String` and `Character` types provide a fast, Unicode-compliant way to work with text in your code. The syntax for string creation and manipulation is lightweight and readable, with a string literal syntax that’s similar to C. String concatenation is as simple as combining two strings with the `+` operator, and string mutability is managed by choosing between a constant or a variable, just like any other value in Swift. You can also use strings to insert constants, variables, literals, and expressions into longer strings, in a process known as string interpolation. This makes it easy to create custom string values for display, storage, and printing.*

Swift의 `String`과 `Character` 타입은 빠르고 유니코드와 호환되는 방식을 제공합니다. 문자열 생성 및 조작을 위한 구문은 C언어와 비슷한 문자열 리터럴 구문을 사용해서 가볍고 읽기 쉽습니다. 문자열 연결은 두 문자열을 `+` 연산자와 결합하는 것처럼 간단하며,문자열 변동성은 Swift의 다른 값과 마찬가지로 상수 혹은 변수 중 하나를 선택해서 관리합니다. 또한 문자열 보간이라고 하는 프로세스에서 문자열을 사용해서 더 긴 문자열에 상수, 변수, 리터럴 및 식을 삽입할 수 있습니다. 이렇게하면 표시, 저장 및 인쇄를 위한 사용자 지정 문자열 값을 쉽게 만들 수 있습니다. 

*Despite this simplicity of syntax, Swift’s `String` type is a fast, modern string implementation. Every string is composed of encoding-independent Unicode characters, and provides support for accessing those characters in various Unicode representations.*

이런 단순한 구문에도 불구하고 스위프트의 `String` 타입은 빠르고 현대적인 문자열 구현체입니다. 모든 문자열은 인코딩 독립적인 유니코드 문자로 구성되며 다양한 유니코드 표현에서 이러한 문자에 액세스 할 수 있도록 지원합니다. 

> *NOTE*
> 
> *Swift’s `String` type is bridged with Foundation’s `NSString` class. Foundation also extends `String` to expose methods defined by `NSString`. This means, if you import Foundation, you can access those `NSString` methods on `String` without casting.*
> 
> Swift의 `String` 타입은 `Foundation`의 `NSString` 클래스와 연결되어 있습니다. `Foundation`은 또한 `String`을 확장하여 `NSString`에 의해 정의된 메서드를 호출시킵니다. 즉, `Foundation`을 가져오면 `String`에서 NSString 메서드에 캐스팅 없이 엑세스할 수 있습니다.
> 
> For more information about using `String` with Foundation and Cocoa, see [Bridging Between String and NSString](https://developer.apple.com/*documentation/swift/stri*ng#2919514).
> 
> Foundation과 Cocoa에서 String을 사용하는 방법에 대한 자세한 내용은 [링크]를 확인하세요.
