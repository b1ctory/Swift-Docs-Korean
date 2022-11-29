### The Basics

*Swift is a new programming language for iOS, macOS, watchOS, and tvOS app development. Nonetheless, many parts of Swift will be familiar from your experience of developing in C and Objective-C.*

스위프트는 iOS, macOS, watchOS 그리고 tvOS 앱 개발을 위한 새로운 언어입니다. 그럼에도 불구하고, 스위프트의 많은 부분은 C와 Objective-C에서 개발한 경험으로부터 친숙할 것입니다.



*Swift provides its own versions of all fundamental C and Objective-C types, including `Int` for integers, `Double` and `Float` for floating-point values, `Bool` for Boolean values, and `String` for textual data. Swift also provides powerful versions of the three primary collection types, `Array`, `Set`, and `Dictionary`, as described in [Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html).*

스위프트는 정수형을 위한 Int, 부동소수점 값을 위한 Double, Float, 불린값을 위한 Bool, 텍스트 데이터를 위한 String을 포함하여 C와 Objective-C의 자체적인 버전을 제공합니다. 스위프트는 또한 세가지 컬렉션 타입인 Array, Set, Dictionary의 강력한 버전을 제공합니다. 



*Like C, Swift uses variables to store and refer to values by an identifying name. Swift also makes extensive use of variables whose values can’t be changed. These are known as constants, and are much more powerful than constants in C. Constants are used throughout Swift to make code safer and clearer in intent when you work with values that don’t need to change.*

C언어와 마찬가지로, 스위프트는 변수를 사용해서 식별된 이름으로 값을 저장하고 참조합니다. 또한 스위프트는 값을 변경할 수 없는 변수를 광범위하게 사용합니다. 이것을 상수라고 하며, C에서의 상수보다 훨씬 강력합니다. 상수는 Swift 전체에서 변경할 필요가 없는 값으로 작업할 때, 코드를 보다 안전하고 명확하게 만들기 위해 사용됩니다.



*In addition to familiar types, Swift introduces advanced types not found in Objective-C, such as tuples. Tuples enable you to create and pass around groupings of values. You can use a tuple to return multiple values from a function as a single compound value.*

익숙한 타입 이외에도, 스위프트는 Objective-C에서는 볼 수 없는 튜플과 같은 고급 타입들을 제공합니다. 튜플을 사용하면 값의 그룹을 만들고 전달할 수 있습니다. 튜플을 사용하여 함수의 여러 값을 하나의 복합 값으로 반환할 수 있습니다.



*Swift also introduces optional types, which handle the absence of a value. Optionals say either “there is a value, and it equals x” or “there isn’t a value at all”. Using optionals is similar to using `nil` with pointers in Objective-C, but they work for any type, not just classes. Not only are optionals safer and more expressive than `nil` pointers in Objective-C, they’re at the heart of many of Swift’s most powerful features.*

스위프트는 또한 값의 부재를 처리하는 옵셔널 타입을 소개합니다. 옵셔널은 "값이 있고 X와 같다." 혹은 "이것은 값이 전혀 없다." 중 하나입니다. 옵셔널을 사용하는 것은 Objective-C에서 포인터와 함께 nil을 사용하는 것과 유사하지만, 클래스에서 뿐만 아니라 모든 타입에서 작동합니다. 옵셔널은 Objective-C의 nil 포인터보다 더 안전하고 표현력이 뛰어날 뿐 아니라 옵셔널의 가장 강력한 기능의 중심에 있습니다.



*Swift is a type-safe language, which means the language helps you to be clear about the types of values your code can work with. If part of your code requires a `String`, type safety prevents you from passing it an `Int` by mistake. Likewise, type safety prevents you from accidentally passing an optional `String` to a piece of code that requires a non-optional `String`. Type safety helps you catch and fix errors as early as possible in the development process.*

Swift는 타입에 안전한 언어로, 이는 코드가 작동할 수 있는 값의 유형을 명확하게 하는데 도움이 된다는 것을 의미합니다. 만약 코드 일부에 문자열이 필요한경우 Type Safety를 사용해서 실수로 정수형을 전달하는 것을 방지할 수 있습니다. 마찬가지로, Type Safety는 옵셔널이 아닌 문자열을 요구하는 코드에 옵셔널 타입의 문자열을 실수로 전달하는 것을 방지합니다. Type Safety는 개발 프로세스에서 오류를 가능한 초기에 발견하고 수정하는데 도움을 줍니다.








