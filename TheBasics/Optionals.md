## *Optionals*

*You use optionals in situations where a value may be absent. An optional represents two possibilities: Either there is a value, and you can unwrap the optional to access that value, or there isn’t a value at all.*

값이 없을 수 있는 상황에서는 옵셔널을 사용합니다. 옵셔널은 다음 두가지 가능성을 나타냅니다 : 값이 있거나 옵셔널을 언래핑하여 값에 접근할 수 있거나 값이 전혀 없습니다.



> *NOTE*
> 
> *The concept of optionals doesn’t exist in C or Objective-C. The nearest thing in Objective-C is the ability to return `nil` from a method that would otherwise return an object, with `nil` meaning “the absence of a valid object.” However, this only works for objects—it doesn’t work for structures, basic C types, or enumeration values. For these types, Objective-C methods typically return a special value (such as `NSNotFound`) to indicate the absence of a value. This approach assumes that the method’s caller knows there’s a special value to test against and remembers to check for it. Swift’s optionals let you indicate the absence of a value for any type at all, without the need for special constants.*
> 
> C나 Objective-C에는 옵셔널의 개념이 존재하지 않습니다. Objective-C에서 가장 가까운 것은 객체를 반환하는 메서드에서 nil을 반환하는 기능이며, nil은 "유효한 객체의 부재"를 의미합니다. 그러나 이것은 구조체, 기본 C 유형 혹은 열거형 값에 대해서는 작동하지 않습니다. 이러한 타입의 경우 Objective-C 메서드는 일반적으로 값이 없음을 나타내기 위해 특수값 (NSNotFound 같은) 을 반환합니다. 이 접근법은 메소드 호출자가 테스트할 특별한 값이 있다는 것을 알고 이 값을 확인하는 것을 기억한다고 가정합니다. Swift의 옵셔널을 사용하면 특수 상수 없이도 모든 유형에 대한 값이 없음을 표시할 수 있습니다. 



*Here’s an example of how optionals can be used to cope with the absence of a value. Swift’s `Int` type has an initializer which tries to convert a `String` value into an `Int` value. However, not every string can be converted into an integer. The string `"123"` can be converted into the numeric value `123`, but the string `"hello, world"` doesn’t have an obvious numeric value to convert to.*

다음은 옵셔널을 사용하여 값이 없는 경우 대처하는 방법에 대한 예시입니다. 스위프트는 Int형에는 String 값을 Int 값으로 변환하는 이니셜라이저가 있습니다. 그러나 모든 문자열이 정수로 반환될 수 있는 것은 아닙니다. "123"이라는 문자열은 123이라는 숫자로 변환할 수 있지만 "hello, world"라는 문자열에는 변환할 명확한 숫자 값이 없습니다. 



*The example below uses the initializer to try to convert a `String` into an `Int`:*

아래는 String을 Int로 변환하는 이니셜라이저를 이용한 예시입니다.

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber is inferred to be of type "Int?", or "optional Int"
```

*Because the initializer might fail, it returns an optional `Int`, rather than an `Int`. An optional `Int` is written as `Int?`, not `Int`. The question mark indicates that the value it contains is optional, meaning that it might contain some `Int` value, or it might contain no value at all. (It can’t contain anything else, such as a `Bool` value or a `String` value. It’s either an `Int`, or it’s nothing at all.)*

이니셜라이저가 실패할 수 있으므로 Int가 아닌 optional Int 를 반환합니다.옵셔널 Int는 Int가 아닌 Int? 로 표기합니다. 물음표는 포함된 값이 옵셔널임을 나타냅니다. 즉, 일부 Int 값을 포함하거나 값을 전혀 포함하지 않을 수 있습니다. (Bool 값 혹은 String 값과 같은 다른 값은 퐇마할 수 없습니다. 그것은 Int 값이거나 아무것도 아닙니다.)



### *nil*

*You set an optional variable to a valueless state by assigning it the special value `nil`:*

옵셔널 변수에 특수 값 nil을 할당하여 값이 없는 상태로 설정합니다.

```swift
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
```

> *NOTE*
> 
> *You can’t use `nil` with non-optional constants and variables. If a constant or variable in your code needs to work with the absence of a value under certain conditions, always declare it as an optional value of the appropriate type.*
> 
> nil은 옵셔널 상수 및 변수와 함께 사용할 수 없습니다. 코드의 상수 혹은 변수가 특정 조건에서 값이 없는 경우 항상 적절한 유형의 옵셔널 값으로 선언하세요.

*If you define an optional variable without providing a default value, the variable is automatically set to `nil` for you:*

기본값을 제공하지 않고 옵셔널 변수를 정의하면 변수가 자동으로 nil로 설정됩니다.



```swift
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
```

> *NOTE*
> 
> *Swift’s `nil` isn’t the same as `nil` in Objective-C. In Objective-C, `nil` is a pointer to a nonexistent object. In Swift, `nil` isn’t a pointer—it’s the absence of a value of a certain type. Optionals of any type can be set to `nil`, not just object types.*
> 
> Swift의 nil은 Objective-C의 nil과 다릅니다. Objective-C에서 nil은 존재하지 않는 객체에 대한 포인터입니다. Swift에서 nil은 포인터가 아니라 특정 유형의 값이 없는 것입니다. 옵셔널은 객체 타입 뿐 아니라 모든 타입을 nil로 설정할 수 있습니다.



### *If Statements and Forced Unwrapping : If 문 및 강제 언래핑*

*You can use an `if` statement to find out whether an optional contains a value by comparing the optional against `nil`. You perform this comparison with the “equal to” operator (`==`) or the “not equal to” operator (`!=`).*

if 문을 사용하여 옵셔널과 nil을 비교하여 옵셔널에 값이 포함되어 있는지 여부를 확인할 수 있습니다. 이 비교는 대수 연산자 (==) 혹은 같지 않음 연산자 (!=) 로 수행합니다.



*If an optional has a value, it’s considered to be “not equal to” `nil`:*

optional이 값을 가지면 값은 "not equal to" nil로 간주됩니다.

```swift
if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
// Prints "convertedNumber contains some integer value."
```

*Once you’re sure that the optional does contain a value, you can access its underlying value by adding an exclamation point (`!`) to the end of the optional’s name. The exclamation point effectively says, “I know that this optional definitely has a value; please use it.” This is known as forced unwrapping of the optional’s value:*

옵셔널에 값이 포함되어있으면 옵셔널 끝에 느낌포를 추가하여 기본 값에 엑세스 할 수 있습니다. 느낌표는 효과적으로 "나는 이 옵셔널이 확실히 값이 있다는 것을 알고 있습니다. 그것을 사용하세요." 라고 말합니다. 이를 옵셔널 값의 강제 언래핑이라고 합니다.



```swift
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
// Prints "convertedNumber has an integer value of 123."
```

*For more about the `if` statement, see [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html).*

if문에 대해 더 많은 정보를 알고 싶다면 [링크]를 확인하세요.

> *NOTE*
> 
> *Trying to use `!` to access a nonexistent optional value triggers a runtime error. Always make sure that an optional contains a non-`nil` value before using `!` to force-unwrap its value.*
> 
> 존재하지 않는 옵셔널 값에 엑세스하기 위해 ! 를 사용하려고 하면 런타임 오류가 발생합니다. ! 를 사용해서 값을 강제로 언래핑하기 전에 옵셔널에 nil이 아닌 값이 포함되어 있는지 항상 확인하세요.



### *Optional Binding : 옵셔널 바인딩*

*You use optional binding to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable. Optional binding can be used with `if` and `while` statements to check for a value inside an optional, and to extract that value into a constant or variable, as part of a single action. `if` and `while` statements are described in more detail in [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html).*

옵셔널 바인딩을 사용하여 옵셔널에 값이 포함되어 있는지 여부를 확인하고, 포함되어 있는 경우 해당 값을 임시 상수 혹은 변수를 사용할 수 있도록 합니다. 옵셔널 바인딩은 옵셔널 내부의 값을 확인하고 단일 동작의 일부로 해당 값을 상수 혹은 변수로 추출하기 위해 if 및 while 문과 함께 사용할 수 있습니다. if 문과 while 문은 [링크]에 자세히 설명되어 있습니다.



*Write an optional binding for an `if` statement as follows:*

if 문에 대한 옵셔널 바인딩을 다음과 같이 작성합니다.

```swift
if let constantName = someOptional {
    statements
}
```

*You can rewrite the `possibleNumber` example from the [Optionals](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID330) section to use optional binding rather than forced unwrapping:*

[Optionals 링크] 섹션으로부터  possibleNumber 예제를 다시 작성하여 강제 언래핑이 아닌 옵셔널 바인딩을 사용할 수 있습니다.

```swift
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" couldn't be converted to an integer")
}
// Prints "The string "123" has an integer value of 123"
```

*This code can be read as:*

*“If the optional `Int` returned by `Int(possibleNumber)` contains a value, set a new constant called `actualNumber` to the value contained in the optional.”*

이 코드는 이렇게 읽을 수 있습니다:

"만약 옵셔널 Int 값이 값을 포함하는 Int(possibleNumber) 로 반환된다면 actualNumber라는 새 상수를 옵셔널에 포함된 값으로 설정하세요"

*If the conversion is successful, the `actualNumber` constant becomes available for use within the first branch of the `if` statement. It has already been initialized with the value contained within the optional, and so you don’t use the `!` suffix to access its value. In this example, `actualNumber` is simply used to print the result of the conversion.*

변환이 성공하면 actualNumber 상수를 if 문의 첫번째 분기 내에서 사용할 수 있게됩니다. 옵셔널에 포함된 값으로 이미 초기화되어 있으므로 ! 접미사를 사용하여 값에 엑세스 하지 않아도 됩니다. 이 예시에서는 actualNumber가 변환 결과를 프린트하는데만 사용됩니다.

*If you don’t need to refer to the original, optional constant or variable after accessing the value it contains, you can use the same name for the new constant or variable:*

포함된 값에 접근한 후 원래의 상수 혹은 변수를 참조할 필요가 없다면 새 상수 혹은 변수에 동일한 이름을 사용할 수 있습니다.

```swift
let myNumber = Int(possibleNumber)
// Here, myNumber is an optional integer
if let myNumber = myNumber {
    // Here, myNumber is a non-optional integer
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```

*This code starts by checking whether `myNumber` contains a value, just like the code in the previous example. If `myNumber` has a value, the value of a new constant named `myNumber` is set to that value. Inside the body of the `if` statement, writing `myNumber` refers to that new non-optional constant. Before the beginning of the `if` statement and after its end, writing `myNumber` refers to the optional integer constant.*

이 코드는 이전 예제 코드와 마찬가지로 myNumber에 값이 포함되어 있는지 확인하는 것으로 시작합니다. 만약 myNumber에 값이 있으면 myNumber라는 이름의 새로운 상수 값이 해당 값으로 설정됩니다. if 문 안에 myNumber라고 적는 것은 새로운 비옵셔널 상수를 의미합니다. if 문의 앞과 끝 뒤에 myNumber 라고 적으면 옵셔널 정수와 상수를 나타냅니다.



*Because this kind of code is so common, you can use a shorter spelling to unwrap an optional value: write just the name of the constant or variable that you’re unwrapping. The new, unwrapped constant or variable implicitly uses the same name as the optional value.*

이런 종류의 코드는 매우 일반적이기 때문에 짧은 철자를 사용하여 옵셔널 값을 언래핑할 수 있습니다 : 당신이 언래핑하고자 하는 상수나 변수를 적으세요. 새로운 언래핑된 상수 혹은 변수는 옵셔널 값과 동일한 이름을 암시적으로 사용합니다.

```swift
if let myNumber {
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```

*You can use both constants and variables with optional binding. If you wanted to manipulate the value of `myNumber` within the first branch of the `if` statement, you could write `if var myNumber` instead, and the value contained within the optional would be made available as a variable rather than a constant. Changes you make to `myNumber` inside the body of the `if` statement apply only to that local variable, not to the original, optional constant or variable that you unwrapped.*

옵셔널 바인딩과 함께 상수와 변수를 모두 사용할 수 있습니다. if 문의 첫번째 분기 내에서 myNumber 값을 조작하려면 대신 `if var myNumber` 를 사용하면 됩니다. 그러면 옵셔널에 포함된 값을 상수가 아닌 변수로 사용할 수 있습니다. if 문의 본문 안에 있는 myNumber에 대한 변경 내용은 해당 로컬 변수에만 적용되며 언래핑한 원래의 옵셔널 상수 혹은 변수에는 적용되지 않습니다.



*You can include as many optional bindings and Boolean conditions in a single `if` statement as you need to, separated by commas. If any of the values in the optional bindings are `nil` or any Boolean condition evaluates to `false`, the whole `if` statement’s condition is considered to be `false`. The following `if` statements are equivalent:*

하나의 if문에 필요한만큼 많은 옵셔널 바인딩과 Boolean 조건을 쉼표로 구분하여 표기할 수 있습니다. 옵셔널 바인딩 값 중 하나가 nil이거나 Boolean 조건이 false로 평가되면 전체 if 문의 조건은 false로 간주됩니다. 다음의 if 조건문과 동등합니다 :

```swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// Prints "4 < 42 < 100"

if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
// Prints "4 < 42 < 100"
```

> *NOTE*
> 
> *Constants and variables created with optional binding in an `if` statement are available only within the body of the `if` statement. In contrast, the constants and variables created with a `guard` statement are available in the lines of code that follow the `guard` statement, as described in [Early Exit](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID525).*
> 
> if 문에서 옵셔널 바인딩으로 생성된 상수와 변수는 if문의 본문 내에서만 사용할 수 있습니다. 반대로 guard 문으로 생성된 상수와 변수는 [링크]에 설명된대로 guard문 뒤에 오는 코드 행에서 사용할 수 있습니다. 



### *Implicitly Unwrapped Optionals : 암묵적으로 옵셔널 언래핑*

*As described above, optionals indicate that a constant or variable is allowed to have “no value”. Optionals can be checked with an `if` statement to see if a value exists, and can be conditionally unwrapped with optional binding to access the optional’s value if it does exist.*

위에서 설명한대로, 옵셔널은 상수 혹은 변수가 "값 없음"으로 허용됨을 나타냅니다. 옵셔널은 if 문을 사용하여 값이 존재하는지 확인할 수 있으며, 옵셔널 바인딩이 존재하는 경우 옵셔널의 값에 엑세스하기 위해 조건부로 옵셔널 바인딩으로 언래핑될 수 있습니다.



*Sometimes it’s clear from a program’s structure that an optional will always have a value, after that value is first set. In these cases, it’s useful to remove the need to check and unwrap the optional’s value every time it’s accessed, because it can be safely assumed to have a value all of the time.*

가끔은 프로그램 구조에서 옵셔널이 처음 설정된 후 항상 값을 가지는 것이 확실합니다. 이러한 경우, 옵셔널이 항상 값을 가지는 것으로 안전하게 추정될 수 있기 때문에 옵셔널에 엑세스 할 때마다 값을 확인하고 언래핑할 필요가 없습니다.



*These kinds of optionals are defined as implicitly unwrapped optionals. You write an implicitly unwrapped optional by placing an exclamation point (`String!`) rather than a question mark (`String?`) after the type that you want to make optional. Rather than placing an exclamation point after the optional’s name when you use it, you place an exclamation point after the optional’s type when you declare it.*

이러한 종류의 옵셔널은 암묵적으로 언래핑된 옵셔널로 정의됩니다. 옵셔널로 만들고 싶은 타입에 물음표 (String?) 대신에 (String!)을 배치해서 암묵적으로 언래핑된 옵셔널을 작성합니다. 옵셔널을 사용할 때 옵셔널의 이름 뒤에 느낌표를 넣는 대신, 당신이 선언할 때 옵셔널 타입 뒤에 느낌표를 배치할 수 있습니다. 



*Implicitly unwrapped optionals are useful when an optional’s value is confirmed to exist immediately after the optional is first defined and can definitely be assumed to exist at every point thereafter. The primary use of implicitly unwrapped optionals in Swift is during class initialization, as described in [Unowned References and Implicitly Unwrapped Optional Properties](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID55).*

암묵적으로 언래핑된 옵셔널은 옵셔널 값이 처음 정의된 직후에 옵셔널의 값이 존재하는 것이 확인되고 그 이후의 모든 시점에 존재한다고 확실히 가정할 수 있을 때 유용합니다. Swift에서 암묵적으로 언래핑된 옵셔널의 초기 사용은 [링크]에 설명된 클래스 초기화 도중에 일어납니다.



*An implicitly unwrapped optional is a normal optional behind the scenes, but can also be used like a non-optional value, without the need to unwrap the optional value each time it’s accessed. The following example shows the difference in behavior between an optional string and an implicitly unwrapped optional string when accessing their wrapped value as an explicit `String`:*

암묵적으로 언래핑된 옵셔널은 일반적인 옵셔널이지만, 매번 엑세스할 때 마다 옵셔널 값을 언래핑할 필요가 없이 비옵셔널 값처럼 사용할 수 있습니다. 다음 예제는 래핑된 값을 명시적인 String으로 액세스할 때 옵셔널 문자열과 암묵적으로 언래핑된 옵셔널 문자열의 동작 차이를 보여줍니다.



```swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation point

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation point
```

*You can think of an implicitly unwrapped optional as giving permission for the optional to be force-unwrapped if needed. When you use an implicitly unwrapped optional value, Swift first tries to use it as an ordinary optional value; if it can’t be used as an optional, Swift force-unwraps the value. In the code above, the optional value `assumedString` is force-unwrapped before assigning its value to `implicitString` because `implicitString` has an explicit, non-optional type of `String`. In code below, `optionalString` doesn’t have an explicit type so it’s an ordinary optional.*

암묵적으로 언래핑된 옵셔널은 강제 언래핑할 수 있는 권한을 부여하는 것으로 생각할 수 있습니다.  암묵적으로 언래핑된 옵셔널 값을 사용할 경우 Swift는 먼저 일반적인 옵셔널 값으로 사용하려고 합니다; 옵셔널로 사용될 수 없는 경우 Swift가 값을 강제로 언래핑합니다. 위의 코드에서 옵셔널 값인 assumptedString은 implicitString에 명시적이고 비옵셔널 타입인 String이 있기 때문에 값을 implicitString에 할당하기 전에 강제로 언래핑됩니다. 아래의 코드에서 optionalString은 명시적인 타입이 없으므로 일반적인 옵셔널입니다.



```swift
let optionalString = assumedString
// The type of optionalString is "String?" and assumedString isn't force-unwrapped.
```

*If an implicitly unwrapped optional is `nil` and you try to access its wrapped value, you’ll trigger a runtime error. The result is exactly the same as if you place an exclamation point after a normal optional that doesn’t contain a value.*

암시적으로 언래핑된 옵셔널이 nil이고 그것의 래핑된 값에 접근하려고 할 때 런타임 에러가 일어나게 됩니다. 결과는 값이 포함되지 않은 일반 옵셔널 값 뒤에 느낌표를 배치하는 경우와 완전히 동일합니다.

*You can check whether an implicitly unwrapped optional is `nil` the same way you check a normal optional:*

암시적으로 언래핑된 옵셔널이 일반 옵셔널을 선택하는 것과 같은 방식으로 nil 인지 여부를 확인할 수 있습니다.

```swift
if assumedString != nil {
    print(assumedString!)
}
// Prints "An implicitly unwrapped optional string."
```

*You can also use an implicitly unwrapped optional with optional binding, to check and unwrap its value in a single statement:*

또한 옵셔널 바인딩과 함께 명시적으로 언래핑된 옵셔널을 사용하여 단일 문에서 값을 확인하고 언래핑할 수 있습니다.

```swift
if let definiteString = assumedString {
    print(definiteString)
}
// Prints "An implicitly unwrapped optional string."
```

> *NOTE*
> 
> *Don’t use an implicitly unwrapped optional when there’s a possibility of a variable becoming `nil` at a later point. Always use a normal optional type if you need to check for a `nil` value during the lifetime of a variable.*
> 
> 변수가 나중에 nil이 될 가능성이 있는 경우에는 암묵적으로 언래핑된 옵셔널을 사용하지 마세요. 변수의 생명주기 동안 nil 값을 확인해야 하는 경우에는 항상 일반적인 옵셔널 유형을 사용하세요.


