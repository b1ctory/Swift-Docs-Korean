## *Customizing Initialization : 초기화 커스터마이징*

*You can customize the initialization process with input parameters and optional property types, or by assigning constant properties during initialization, as described in the following sections.*

다음 섹션에 설명된 대로 입력 매개 변수 및 옵셔널 프로퍼티 타입을 사용하여 초기화 프로세스를 사용자 정의하거나 초기화 중에 상수 프로퍼티를 할당할 수 있습니다.

### *Initialization Parameters : 초기화 매개변수*

*You can provide initialization parameters as part of an initializer’s definition, to define the types and names of values that customize the initialization process. Initialization parameters have the same capabilities and syntax as function and method parameters.*

초기화 프로세스를 사용자 정의하는 값의 타입과 이름을 정의하기 위해 초기화 매개 변수를 초기화 정의의 일부로 제공할 수 있습니다. 초기화 매개 변수는 함수 및 메서드 매개 변수와 동일한 기능 및 구문을 가집니다.

*The following example defines a structure called `Celsius`, which stores temperatures expressed in degrees Celsius. The `Celsius` structure implements two custom initializers called `init(fromFahrenheit:)` and `init(fromKelvin:)`, which initialize a new instance of the structure with a value from a different temperature scale:*

다음 예제는 섭씨로 표시된 온도를 저장하는 `Celsius`라는 구조체를 정의합니다. `Celsius` 구조체는 `init(fromFahrenheit:)`와 `init(fromKelvin:)`이라는 두 가지 사용자 정의 이니셜라이저를 구현합니다. 이 두 이니셜라이저는 다른 온도 척도의 값으로 구조체의 새 인스턴스를 초기화합니다:

```swift
struct Celsius {
    var temperatureInCelsius: Double
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}
let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
// boilingPointOfWater.temperatureInCelsius is 100.0
let freezingPointOfWater = Celsius(fromKelvin: 273.15)
// freezingPointOfWater.temperatureInCelsius is 0.0
```

*The first initializer has a single initialization parameter with an argument label of `fromFahrenheit` and a parameter name of `fahrenheit`. The second initializer has a single initialization parameter with an argument label of `fromKelvin` and a parameter name of `kelvin`. Both initializers convert their single argument into the corresponding Celsius value and store this value in a property called `temperatureInCelsius`.*

첫번째 이니셜라이저는 `fromFahrenheit`라는 인수 레이블과 `fahrenheit`라는 매개 변수 이름을 가진 단일 초기화 매개변수를 가지고 있습니다. 두 번째 이니셜라이저에는 인수 레이블이 `fromKelvin`이고 매개 변수 이름이 `kelvin`인 단일 초기화 매개 변수가 있습니다. 두 이ㅣ셜라이저는 모두 단일 인수를 해당 섭씨 값으로 변환하고 이 값을 `temperatureInCelsius`라는 프로퍼티에 저장합니다.

### *Parameter Names and Argument Labels : 매개변수 이름과 인수 레이블*

*As with function and method parameters, initialization parameters can have both a parameter name for use within the initializer’s body and an argument label for use when calling the initializer.*

함수 및 메서드 매개 변수와 마찬가지로 초기화 매개 변수는 이니셜라이저 본문 내에서 사용할 매개변수 이름과 이니셜라이저를 호출할 때 사용할 인수 레이블을 모두 가질 수 있습니다.

*However, initializers don’t have an identifying function name before their parentheses in the way that functions and methods do. Therefore, the names and types of an initializer’s parameters play a particularly important role in identifying which initializer should be called. Because of this, Swift provides an automatic argument label for every parameter in an initializer if you don’t provide one.*

그러나 이니셜라이저는 함수와 메서드가 하는 방식으로 괄호 앞에 식별할 수 있는 함수 이름이 없습니다. 따라서 이니셜라이저 매개변수의 이름과 타입은 어떤 이니셜라이저를 호출해야 하는지 식별하는데 특히 중요한 역할을 합니다. 이 때문에 Swift는 사용자가 제공하지 않을 경우 이니셜라이저의 모든 매개변수에 대한 자동 인수 레이블을 제공합니다.

*The following example defines a structure called `Color`, with three constant properties called `red`, `green`, and `blue`. These properties store a value between `0.0` and `1.0` to indicate the amount of red, green, and blue in the color.*

다음 예제에서는 `Color`라는 구조체를 정의하고 `red`, `green`, `blue`라는 세 가지 상수 프로퍼티를 사용합니다. 이러한 프로퍼티는 `0.0`과 `1.0` 사이의 값을 저장하여 색상의 빨간색, 녹색 및 파란색 양을 나타냅니다.

*`Color` provides an initializer with three appropriately named parameters of type `Double` for its red, green, and blue components. `Color` also provides a second initializer with a single `white` parameter, which is used to provide the same value for all three color components.*

`Color`는 빨강, 초록, 파랑 구성요소에 대해 적절한 이름을 가진 `Double` 타입의 세 가지 매개변수를 가진 이니셜라이저를 제공합니다. `Color`는 또한 세 가지 색상 구성요소 모두에 동일한 값을 제공하는 데 사용되는 단일 `white` 매개변수를 가진 두 번째 이니셜라이저를 제공합니다.

```swift
struct Color {
    let red, green, blue: Double
    init(red: Double, green: Double, blue: Double) {
        self.red   = red
        self.green = green
        self.blue  = blue
    }
    init(white: Double) {
        red   = white
        green = white
        blue  = white
    }
}
```

*Both initializers can be used to create a new `Color` instance, by providing named values for each initializer parameter:*

각 이니셜라이저 매개변수에 대해 명명된 값을 제공하여 두 이니셜라이저를 사용하여 새 `Color` 인스턴스를 만들 수 있습니다:

```swift
let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
let halfGray = Color(white: 0.5)
```

*Note that it isn’t possible to call these initializers without using argument labels. Argument labels must always be used in an initializer if they’re defined, and omitting them is a compile-time error:*

인수 레이블을 사용하지 않고는 이러한 이니셜라이저를 호출할 수 없습니다. 인수 레이블이 정의되어 있는 경우에는 항상 이니셜라이저에서 사용해야 하며 이를 생략하면 컴파일 타임에서 에러가 발생합니다:

```swift
let veryGreen = Color(0.0, 1.0, 0.0)
// this reports a compile-time error - argument labels are required
```

### *Initializer Parameters Without Argument Labels : 인수 레이블이 없는 이니셜라이저 매개 변수*

*If you don’t want to use an argument label for an initializer parameter, write an underscore (`_`) instead of an explicit argument label for that parameter to override the default behavior.*

Initializer 매개 변수에 인수 레이블을 사용하지 않으려면 해당 매개 변수에 대한 명시적 인수 레이블 대신 밑줄(`_`)을 작성하여 기본 동작을 재정의합니다.

*Here’s an expanded version of the `Celsius` example from [Initialization Parameters](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID208) above, with an additional initializer to create a new `Celsius` instance from a `Double` value that’s already in the Celsius scale:*

다음은 위의 [링크]에서 확장된 버전의 `Celsius` 예제입니다. 여기에는 이미 섭씨 눈금에 있는 `Double` 값에서 새로운 `Celsius` 인스턴스를 생성하는 추가 이니셜라이저가 포함되어 있습니다:

```swift
struct Celsius {
    var temperatureInCelsius: Double
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
    init(_ celsius: Double) {
        temperatureInCelsius = celsius
    }
}
let bodyTemperature = Celsius(37.0)
// bodyTemperature.temperatureInCelsius is 37.0
```

*The initializer call `Celsius(37.0)` is clear in its intent without the need for an argument label. It’s therefore appropriate to write this initializer as `init(_ celsius: Double)` so that it can be called by providing an unnamed `Double` value.*

이니셜라이저 호출 `Celsius(37.0)`는 인수 레이블 없이도 의도가 명확합니다. 따라서 이 이니셜라이저를 `init(_℃: Double)`로 작성하여 이름 없는 `Double` 값을 제공하여 호출할 수 있도록 하는 것이 적절합니다.

### *Optional Property Types : 옵셔널 프로퍼티 타입*

*If your custom type has a stored property that’s logically allowed to have “no value”—perhaps because its value can’t be set during initialization, or because it’s allowed to have “no value” at some later point—declare the property with an optional type. Properties of optional type are automatically initialized with a value of `nil`, indicating that the property is deliberately intended to have “no value yet” during initialization.*

사용자 정의 타입에 "값 없음"이 논리적으로 허용되는 저장된 프로퍼티가 있는 경우(초기화 중에 값을 설정할 수 없거나 나중에 "값 없음"이 허용되기 때문일 수 있습니다.), 프로퍼티를 옵셔널 타입으로 선언합니다. 옵셔널 타입의 프로퍼티는 자동으로 `nil` 값으로 초기화되며, 이는 프로퍼티가 초기화 중에 "아직 값이 없음"을 의도적으로 의도했음을 나타냅니다.

*The following example defines a class called `SurveyQuestion`, with an optional `String` property called `response`:*

다음 예제에서는 옵셔널 `String` 프로퍼티인 `response`를 사용하여 `SurveyQuestion`이라는 클래스를 정의합니다:

```swift
class SurveyQuestion {
    var text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        print(text)
    }
}
let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
cheeseQuestion.ask()
// Prints "Do you like cheese?"
cheeseQuestion.response = "Yes, I do like cheese."
```

*The response to a survey question can’t be known until it’s asked, and so the `response` property is declared with a type of `String?`, or “optional `String`”. It’s automatically assigned a default value of `nil`, meaning “no string yet”, when a new instance of `SurveyQuestion` is initialized.*

설문조사 질문에 대한 응답은 질문하기 전에는 알 수 없으므로 `response` 프로퍼티는 `String?` 또는 '옵셔널 `String`' 타입으로 선언됩니다. `SurveyQuestion`의 새 인스턴스가 초기화되면 "아직 문자열이 없음"을 의미하는 기본값 `nil`이 자동으로 할당됩니다.

### *Assigning Constant Properties During Initialization : 초기화 중에 상수 프로퍼티 할당*

*You can assign a value to a constant property at any point during initialization, as long as it’s set to a definite value by the time initialization finishes. Once a constant property is assigned a value, it can’t be further modified.*

초기화가 완료될 때까지 값이 확실한 값으로 설정되어 있으면 초기화 중에 언제든지 상수 프로퍼티에 값을 할당할 수 있습니다. 상수 프로퍼티에 값이 할당되면 더 이상 수정할 수 없습니다.

> *NOTE*
> 
> *For class instances, a constant property can be modified during initialization only by the class that introduces it. It can’t be modified by a subclass.*
> 
> 클래스 인스턴스의 경우 초기화 중에 상수 프로퍼티를 도입하는 클래스에서만 수정할 수 있습니다. 하위 클래스에서 수정할 수 없습니다.

*You can revise the `SurveyQuestion` example from above to use a constant property rather than a variable property for the `text` property of the question, to indicate that the question doesn’t change once an instance of `SurveyQuestion` is created. Even though the `text` property is now a constant, it can still be set within the class’s initializer:*

위에서 설문조사 질문 예제를 수정하여 질문의 `text` 프로퍼티에 변수 프로퍼티가 아닌 상수 프로퍼티를 사용하여 설문조사 질문의 인스턴스가 생성된 후에도 질문이 변경되지 않음을 나타낼 수 있습니다. 이제 `text` 프로퍼티가 상수가 되더라도 클래스의 이니셜라이저 내에서 설정할 수 있습니다:

```swift
class SurveyQuestion {
    let text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        print(text)
    }
}
let beetsQuestion = SurveyQuestion(text: "How about beets?")
beetsQuestion.ask()
// Prints "How about beets?"
beetsQuestion.response = "I also like beets. (But not with cheese.)"
```
