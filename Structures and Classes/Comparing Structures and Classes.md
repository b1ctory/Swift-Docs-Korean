## *Comparing Structures and Classes : 구조체와 클래스 비교*

*Structures and classes in Swift have many things in common. Both can:*

Swift의 구조체와 클래스는 공통점이 많습니다. 둘 다 가능합니다 :

- *Define properties to store values*
  
  값을 저장할 속성을 정의합니다.

- *Define methods to provide functionality*
  
  기능을 제공하는 메서드를 정의합니다. 

- *Define subscripts to provide access to their values using subscript syntax*
  
  첨자 구문을 사용하여 값에 액세스할 수 있도록 첨자를 정의합니다.

- *Define initializers to set up their initial state*
  
  이니셜라이저를 사용해서 초기 상태를 설정합니다. 

- *Be extended to expand their functionality beyond a default implementation*
  
  기본 구현 이상으로 기능을 확장할 수 있습니다.

- *Conform to protocols to provide standard functionality of a certain kind*
  
  프로토콜을 준수하여 특정 종류의 표준 기능을 제공합니다.

*For more information, see [Properties](https://docs.swift.org/swift-book/LanguageGuide/Properties.html), [Methods](https://docs.swift.org/swift-book/LanguageGuide/Methods.html), [Subscripts](https://docs.swift.org/swift-book/LanguageGuide/Subscripts.html), [Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html), [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html), and [Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html).*

자세한 내용은 [링크들]을 참조하세요.

*Classes have additional capabilities that structures don’t have:*

클래스에는 구조체에는 없는 추가적인 기능이 있습니다.

- *Inheritance enables one class to inherit the characteristics of another.*
  
  상속을 통해 한 클래스가 다른 클래스의 특성을 상속할 수 있습니다. 

- *Type casting enables you to check and interpret the type of a class instance at runtime.*
  
  타입 캐스팅을 사용하면 런타임에 클래스 인스턴스의 타입을 확인하고 해석할 수 있습니다. 

- *Deinitializers enable an instance of a class to free up any resources it has assigned.*
  
  초기화 해제자를 사용하면 클래스 인스턴스에서 할당된 리소스를 모두 사용할 수 있습니다.

- *Reference counting allows more than one reference to a class instance.*
  
  참조 카운트는 클래스 인스턴스에 대한 참조를 두 개 이상 허용합니다.

*For more information, see [Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html), [Type Casting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html), [Deinitialization](https://docs.swift.org/swift-book/LanguageGuide/Deinitialization.html), and [Automatic Reference Counting](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html).*

더 많은 정보는 [링크들]을 참조하세요.

*The additional capabilities that classes support come at the cost of increased complexity. As a general guideline, prefer structures because they’re easier to reason about, and use classes when they’re appropriate or necessary. In practice, this means most of the custom data types you define will be structures and enumerations. For a more detailed comparison, see [Choosing Between Structures and Classes](https://developer.apple.com/documentation/swift/choosing_between_structures_and_classes).*

클래스에서 지원하는 추가 기능은 복잡성 증가의 비용으로 발생합니다. 일반적인 지침으로, 구조체는 추론하기 때문에 쉽게 선호하고, 적절하거나 필요할 때 클래스를 사용하세요. 실제로 이는 사용자가 정의하는 사용자 정의 데이터 타입의 대부분이 구조체 및 열거형임을 의미합니다. 자세한 비교는 [링크]를 보세요.

> *NOTE*
> 
> *Classes and actors share many of the same characteristics and behaviors. For information about actors, see [Concurrency](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html).*
> 
> 클래스와 actors는 많은 동일한 특성과 행동을 공유합니다. actors 에 대한 자세한 내용은 [링크]를 참조하세요.

### *Definition Syntax : 정의 구문*

*Structures and classes have a similar definition syntax. You introduce structures with the `struct` keyword and classes with the `class` keyword. Both place their entire definition within a pair of braces:*

구조체 및 클래스의 정의 구문은 유사합니다. `struct` 키워드를 가진 구조체와 `class` 키워드를 가진 클래스를 소개합니다. 둘 다 전체 정의를 한 쌍의 괄호 안에 배치합니다.

```swift
struct SomeStructure {
    // structure definition goes here
}
class SomeClass {
    // class definition goes here
}
```

> *NOTE*
> 
> *Whenever you define a new structure or class, you define a new Swift type. Give types `UpperCamelCase` names (such as `SomeStructure` and `SomeClass` here) to match the capitalization of standard Swift types (such as `String`, `Int`, and `Bool`). Give properties and methods `lowerCamelCase` names (such as `frameRate` and `incrementCount`) to differentiate them from type names.*
> 
> 새 구조체 혹은 클래스를 정의할 때마다 새 Swift 타입을 정의합니다. 표준 Swift 타입 (`String`, `Int` 그리고 `Bool`) 의 대문자와 일치하도록 `UpperCamelCase` 타입 이름 (`SomeStructure` 이나 `SomeClass`)을 지정합니다. 속성과 메서드 lowerCalemCase 이름 (`frameRate` 및 `incrementCount`)를 입력해서 타입 이름과 구별합니다.

*Here’s an example of a structure definition and a class definition:*

구조체 정의 및 클래스 정의의 예는 다음과 같습니다.

```swift
struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```

*The example above defines a new structure called `Resolution`, to describe a pixel-based display resolution. This structure has two stored properties called `width` and `height`. Stored properties are constants or variables that are bundled up and stored as part of the structure or class. These two properties are inferred to be of type `Int` by setting them to an initial integer value of `0`.*

위의 에는 픽셀 기반 디스플레이 해상도를 설명하기 위해 `Resolution` 이라는 새로운 구조체를 정의합니다. 이 구조체에는 `width`와 `height`라는 두가지 저장된 특성이 있습니다. 저정된 속성은 구조체 혹은 클래스의 일부로 번들되어 저장되는 상수 혹은 변수입니다. 이 두가지 특성은 초기 정수값 `0`으로 설정하여 `Int` 타입으로 추론됩니다.

*The example above also defines a new class called `VideoMode`, to describe a specific video mode for video display. This class has four variable stored properties. The first, `resolution`, is initialized with a new `Resolution` structure instance, which infers a property type of `Resolution`. For the other three properties, new `VideoMode` instances will be initialized with an `interlaced` setting of `false` (meaning “noninterlaced video”), a playback frame rate of `0.0`, and an optional `String` value called `name`. The `name` property is automatically given a default value of `nil`, or “no `name` value”, because it’s of an optional type.*

위의 예는 또한 비디오 디스플레이를 위한 특정 비디오 모드를 설명하기 위해 `VideoMode`라는 새로운 클래스를 정의합니다. 이 클래스에는 네 개의 변수 저장 프로퍼티가 있습니다. 첫번째 `resolution`은 새로운 `Resolution` 구조체 인스턴스로 초기화됩니다. 다른 세가지 속성의 경우 새 `VideoMode` 인스턴스는 `interlaced` 설정인 `false` ("noninterlaced video"를 의미하는) 재생 프레임률인 `0.0` 및 옵셔널 `String` 값은 `name`으로 초기화됩니다. `name` 프로퍼티는 옵셔널 타입이므로 기본값인 `nil` 혹은 "no name value"값이 자동으로 제공됩니다.

### *Structure and Class Instances : 구조체 및 클래스 인스턴스*

*The `Resolution` structure definition and the `VideoMode` class definition only describe what a `Resolution` or `VideoMode` will look like. They themselves don’t describe a specific resolution or video mode. To do that, you need to create an instance of the structure or class.*

`Resolution` 구조체 정의와 `VideoMode` 클래스 정의는 `Resolution` 혹은 `VideoMode` 가 어떻게 표시되는지만 설명합니다. 특정 해상도나 비디오모드를 설명하지 않습니다. 이렇게 하려면 구조체 혹은 클래스의 인스턴스를 만들어야 합니다.

*The syntax for creating instances is very similar for both structures and classes:*

인스턴스를 만드는 구문은 구조체와 클래스 모두에서 매우 유사합니다.

```swift
let someResolution = Resolution()
let someVideoMode = VideoMode()
```

*Structures and classes both use initializer syntax for new instances. The simplest form of initializer syntax uses the type name of the class or structure followed by empty parentheses, such as `Resolution()` or `VideoMode()`. This creates a new instance of the class or structure, with any properties initialized to their default values. Class and structure initialization is described in more detail in* [Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html).

구조체 및 클래스는 모두 새 인스턴스에 대해 이니셜라이즈 구문을 사용합니다. 가장 간단한 형태의 이니셜라이저 구문은 클래스 혹은 구조체의 타입 이름 다음에 `Resolution()` 혹은 `VideoMode()`와 같은 빈 괄호를 사용합니다. 그러면 프로퍼티가 기본값으로 초기화된 클래스 혹은 구조체의 새 인스턴스가 만들어집니다. 클래스 및 구조체 초기화에 대한 자세한 내용은 [링크]를 참조하세요.

### *Accessing Properties : 프로퍼티 접근*

*You can access the properties of an instance using dot syntax. In dot syntax, you write the property name immediately after the instance name, separated by a period (`.`), without any spaces:*

점 구문을 사용해서 인스턴스의 프로퍼티에 엑세스할 수 있습니다. 점 구문에서는 인스턴스 이름 바로 뒤에 공백없이 마침표 (`.`)로 구분하여 프로퍼티 이름을 사용합니다.

```swift
print("The width of someResolution is \(someResolution.width)")
// Prints "The width of someResolution is 0"
```

*In this example, `someResolution.width` refers to the `width` property of `someResolution`, and returns its default initial value of `0`.*

이 예에서는 `somResoultion.width`가 `someResolution`의 `width` 프로퍼티를 나타내고, 기본 초기값인 `0`을 반환합니다.

*You can drill down into subproperties, such as the `width` property in the `resolution` property of a `VideoMode`:*

`VideoMode`의 `resolution` 프로퍼티에 있는 `width` 프로퍼티와 같은 하위 프로퍼티를 드릴다운 할 수 있습니다.

```swift
print("The width of someVideoMode is \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is 0"
```

*You can also use dot syntax to assign a new value to a variable property:*

점 구문을 사용해서 변수 프로퍼티에 새 값을 할당할 수도 있습니다. 

```swift
someVideoMode.resolution.width = 1280
print("The width of someVideoMode is now \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is now 1280"
```

### *Memberwise Initializers for Structure Types : 구조체 타입에 대한 Memberwise  이니셜라이저*

*All structures have an automatically generated memberwise initializer, which you can use to initialize the member properties of new structure instances. Initial values for the properties of the new instance can be passed to the memberwise initializer by name:*

모든 구조체에는 자동으로 생성된 멤버별 이니셜라이저가 있으며, 이를 사용해서 새 구조체 인스턴스의   멤버 프로퍼티를 초기화할 수 있습니다 새 인스턴수의 속성에 대한 초기 값은 다음 이름으로 memberwise 이니셜라이저에 전달할 수 있습니다.

```swift
let vga = Resolution(width: 640, height: 480)
```

*Unlike structures*, *class instances don’t receive a default memberwise initializer. Initializers are described in more detail in* [Initialization](https://docs.swift.org/swift-book*/LanguageGuide/Initialization.html).

구조체와 다르게, 클래스 인스턴스는 기본 memberwise initializer를 받지 않습니다. 이니셜라이저에 대한 자세한 내용은 [링크]를 참조하세요.
