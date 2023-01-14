## *Setting Initial Values for Stored Properties : 저장 프로퍼티의 초기값 설정*

*Classes and structures must set all of their stored properties to an appropriate initial value by the time an instance of that class or structure is created. Stored properties can’t be left in an indeterminate state.*

클래스 및 구조체는 해당 클래스 또는 구조체의 인스턴스가 생성될 때까지 저장된 모든 프로퍼티를 적절한 초기값으로 설정해야 합니다. 저장 프로퍼티를 불확실한 상태로 둘 수 없습니다.

*You can set an initial value for a stored property within an initializer, or by assigning a default property value as part of the property’s definition. These actions are described in the following sections.*

이니셜라이저 내에서 저장 프로퍼티의 초기값을 설정하거나 프로퍼티 정의의 일부로 기본 프로퍼티 값을 할당할 수 있습니다. 이러한 작업은 다음 섹션에서 설명합니다.

> *NOTE*
> 
> *When you assign a default value to a stored property, or set its initial value within an initializer, the value of that property is set directly, without calling any property observers.*
> 
> 저장 프로퍼티에 기본값을 할당하거나 이니셜라이저 내에서 초기값을 설정하면 프로퍼티 옵저버를 호출하지 않고 해당 프로퍼티의 값이 직접 설정됩니다.

### *Initializers : 이니셜라이저 (초기화자)*

*Initializers are called to create a new instance of a particular type. In its simplest form, an initializer is like an instance method with no parameters, written using the `init` keyword:*

이니셜라이저는 특정 타입의 새 인스턴스를 만들기 위해 호출됩니다. 가장 간단한 형태로, 이니셜라이저는 `init` 키워드를 사용하여 작성된 매개 변수가 없는 인스턴스 메서드와 같습니다:

```swift
init() {
    // perform some initialization here
}
```

*The example below defines a new structure called `Fahrenheit` to store temperatures expressed in the Fahrenheit scale. The `Fahrenheit` structure has one stored property, `temperature`, which is of type `Double`:*

아래 예제는 화씨 척도로 표현된 온도를 저장하기 위해 `Fahrenheit`라는 새로운 구조체를 정의합니다. `Fahrenheit` 구조에는 `temperature`라는 `Double`타입의 하나의 저장프로퍼티가 있습니다:

```swift
struct Fahrenheit {
    var temperature: Double
    init() {
        temperature = 32.0
    }
}
var f = Fahrenheit()
print("The default temperature is \(f.temperature)° Fahrenheit")
// Prints "The default temperature is 32.0° Fahrenheit"
```

*The structure defines a single initializer, `init`, with no parameters, which initializes the stored temperature with a value of `32.0` (the freezing point of water in degrees Fahrenheit).*

이 구조체는 매개 변수가 없는 단일 이니셜라이저 `init`를 정의하며, 이는 저장된 온도를 `32.0`(화씨로 표시된 물의 어는점)의 값으로 초기화합니다.

### *Default Property Values : 기본 프로퍼티 값*

*You can set the initial value of a stored property from within an initializer, as shown above. Alternatively, specify a default property value as part of the property’s declaration. You specify a default property value by assigning an initial value to the property when it’s defined.*

위와 같이 이니셜라이저 내에서 저장프로퍼티의 초기값을 설정할 수 있습니다. 또는 프로퍼티 선언의 일부로 기본 프로퍼티 값을 지정합니다. 프로퍼티가 정의될 때 프로퍼티에 초기값을 할당하여 기본 프로퍼티 값을 지정합니다.

> *NOTE*
> 
> *If a property always takes the same initial value, provide a default value rather than setting a value within an initializer. The end result is the same, but the default value ties the property’s initialization more closely to its declaration. It makes for shorter, clearer initializers and enables you to infer the type of the property from its default value. The default value also makes it easier for you to take advantage of default initializers and initializer inheritance, as described later in this chapter.*
> 
> 프로퍼티가 항상 동일한 초기 값을 사용하는 경우 이니셜라이저 내에서 값을 설정하는 대신 기본값을 제공하세요. 최종 결과는 동일하지만 기본값은 프로퍼티의 초기화를 선언에 더 가깝게 연결합니다. 더 짧고 명확한 이니셜라이저를 제공하고 기본값에서 프로퍼티 타입 을 유추할 수 있습니다. 또한 기본값을 사용하면 이 장 뒷부분에 설명된 대로 기본 이니셜라이저 및 이니셜라이저 상속을 쉽게 이용할 수 있습니다.

*You can write the `Fahrenheit` structure from above in a simpler form by providing a default value for its `temperature` property at the point that the property is declared:*

프로퍼티가 선언된 시점에서 `temperature` 프로퍼티의 기본값을 제공하여 위에서 `Fahrenheit` 구조체를 보다 간단한 형태로 작성할 수 있습니다:

```swift
struct Fahrenheit {
    var temperature = 32.0
}
```
