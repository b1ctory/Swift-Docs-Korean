## *Type Properties : 타입 프로퍼티*

*Instance properties are properties that belong to an instance of a particular type. Every time you create a new instance of that type, it has its own set of property values, separate from any other instance.*

인스턴스 프로퍼티는 특정 타입의 인스턴스에 속하는 프로퍼티입니다. 해당 타입의 새 인스턴스를 생성할 때마다 다른 인스턴스와는 별도로 고유한 프로퍼티 값 집합이 있습니다.

*You can also define properties that belong to the type itself, not to any one instance of that type. There will only ever be one copy of these properties, no matter how many instances of that type you create. These kinds of properties are called type properties.*

또한 해당 타입의 인스턴스가 아닌 타입 자체에 속하는 프로퍼티를 정의할 수 있습니다. 해당 타입의 인스턴스 수에 관계없이 이러한 프로퍼티의 복사본은 하나만 있습니다. 이러한 프로퍼티를 타입 프로퍼티라고 합니다.

*Type properties are useful for defining values that are universal to all instances of a particular type, such as a constant property that all instances can use (like a static constant in C), or a variable property that stores a value that’s global to all instances of that type (like a static variable in C).*

타입 프로퍼티는 모든 인스턴스가 사용할 수 있는 상수 프로퍼티(예: C의 정적 상수) 또는 해당 타입의 모든 인스턴스에 대해 전역적인 값(예: C의 스태틱한 변수)을 저장하는 변수 프로퍼티와 같이 특정 타입의 모든 인스턴스에 공통적인 값을 정의하는 데 유용합니다.

*Stored type properties can be variables or constants. Computed type properties are always declared as variable properties, in the same way as computed instance properties.*

저장 프로퍼티는 변수 또는 상수일 수 있습니다. 연산 프로퍼티는 연산 인스턴스 프로퍼티와 동일한 방식으로 항상 변수 프로퍼티로 선언됩니다.

> *NOTE*
> 
> *Unlike stored instance properties, you must always give stored type properties a default value. This is because the type itself doesn’t have an initializer that can assign a value to a stored type property at initialization time.*
> 
> 저장된 인스턴스 프로퍼티와 달리 저장 타입 프로퍼티에는 항상 기본값을 지정해야 합니다. 이는 타입 자체에 초기화 시 저장된 타입 프로퍼티에 값을 할당할 수 있는 이니셜라이저가 없기 때문입니다.
> 
> *Stored type properties are lazily initialized on their first access. They’re guaranteed to be initialized only once, even when accessed by multiple threads simultaneously, and they don’t need to be marked with the `lazy` modifier.*
> 
> 저장 타입 프로퍼티는 첫번째 액세스 시 느리게 초기화됩니다. 여러 스레드가 동시에 액세스하는 경우에도 한 번만 초기화할 수 있으며 `lazy` 수정자로 표시할 필요가 없습니다.

### *Type Property Syntax : 타입 프로퍼티 구문*

*In C and Objective-C, you define static constants and variables associated with a type as global static variables. In Swift, however, type properties are written as part of the type’s definition, within the type’s outer curly braces, and each type property is explicitly scoped to the type it supports.*

C 및 Objective-C에서는 타입과 관련된 정적 상수 및 변수를 전역 스태틱 변수로 정의합니다. 그러나 Swift에서 타입 프로퍼티는 타입 정의의 일부로 타입의 바깥쪽 중괄호 내에 기록되고 각 타입 프로퍼티는 지원하는 타입에 명시적으로 범위가 지정됩니다.

*You define type properties with the `static` keyword. For computed type properties for class types, you can use the `class` keyword instead to allow subclasses to override the superclass’s implementation. The example below shows the syntax for stored and computed type properties:*

`static` 키워드를 사용하여 타입 프로퍼티를 정의합니다. 클래스 타입에 대한 연산 타입 프로퍼티의 경우 대신 `class` 키워드를 사용하여 하위 클래스가 슈퍼 클래스의 구현을 재정의하도록 허용할 수 있습니다. 아래 예제에서는 저장 및 연산 타입 프로퍼티의 구문을 보여 줍니다:

```swift
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 1
    }
}
enum SomeEnumeration {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 6
    }
}
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 27
    }
    class var overrideableComputedTypeProperty: Int {
        return 107
    }
}
```

> *NOTE*
> 
> *The computed type property examples above are for read-only computed type properties, but you can also define read-write computed type properties with the same syntax as for computed instance properties.*
> 
> 위의 연산 타입 프로퍼티 예제는 읽기 전용 연산 타입 프로퍼티에 대한 것이지만 연산 인스턴스 프로퍼티와 동일한 구문으로 읽기-쓰기 연산 타입 프로퍼티를 정의할 수도 있습니다.

### *Querying and Setting Type Properties : 타입 프로퍼티 쿼리 및 설정*

*Type properties are queried and set with dot syntax, just like instance properties. However, type properties are queried and set on the type, not on an instance of that type. For example:*

타입 프로퍼티는 인스턴스 프로퍼티와 마찬가지로 점 구문으로 쿼리 및 설정됩니다. 그러나 타입 프로퍼티는 해당 타입의 인스턴스가 아닌 타입에 대해 쿼리되고 설정됩니다. 예를 들어 다음과 같습니다:

```swift
print(SomeStructure.storedTypeProperty)
// Prints "Some value."
SomeStructure.storedTypeProperty = "Another value."
print(SomeStructure.storedTypeProperty)
// Prints "Another value."
print(SomeEnumeration.computedTypeProperty)
// Prints "6"
print(SomeClass.computedTypeProperty)
// Prints "27"
```

*The examples that follow use two stored type properties as part of a structure that models an audio level meter for a number of audio channels. Each channel has an integer audio level between `0` and `10` inclusive.*

다음 예제에서는 여러 오디오 채널에 대한 오디오 레벨 미터를 모델링하는 구조체의 일부로 두 개의 저장 타입 프로퍼티를 사용합니다. 각 채널에는 `0`과 `10` 사이의 정수 오디오 레벨이 있습니다.

*The figure below illustrates how two of these audio channels can be combined to model a stereo audio level meter. When a channel’s audio level is `0`, none of the lights for that channel are lit. When the audio level is `10`, all of the lights for that channel are lit. In this figure, the left channel has a current level of `9`, and the right channel has a current level of `7`:*

아래 그림은 이러한 오디오 채널 두 개를 결합하여 스테레오 오디오 레벨 미터를 모델링하는 방법을 보여줍니다. 채널의 오디오 레벨이 `0`이면 해당 채널의 표시등이 하나도 켜지지 않습니다. 오디오 레벨이 `10`이면 해당 채널의 모든 조명이 켜집니다. 이 그림에서 왼쪽 채널의 전류 레벨은 `9`이고 오른쪽 채널의 전류 레벨은 `7`입니다:

![](https://docs.swift.org/swift-book/_images/staticPropertiesVUMeter_2x.png)

*The audio channels described above are represented by instances of the `AudioChannel` structure:*

위에서 설명한 오디오 채널은 `AudioChannel`구조체의 인스턴스로 표시됩니다:

```swift
struct AudioChannel {
    static let thresholdLevel = 10
    static var maxInputLevelForAllChannels = 0
    var currentLevel: Int = 0 {
        didSet {
            if currentLevel > AudioChannel.thresholdLevel {
                // cap the new audio level to the threshold level
                currentLevel = AudioChannel.thresholdLevel
            }
            if currentLevel > AudioChannel.maxInputLevelForAllChannels {
                // store this as the new overall maximum input level
                AudioChannel.maxInputLevelForAllChannels = currentLevel
            }
        }
    }
}
```

*The `AudioChannel` structure defines two stored type properties to support its functionality. The first, `thresholdLevel`, defines the maximum threshold value an audio level can take. This is a constant value of `10` for all `AudioChannel` instances. If an audio signal comes in with a higher value than `10`, it will be capped to this threshold value (as described below).*

`AudioChannel` 구조체는 그 기능을 지원하기 위해 두 개의 저장 타입 프로퍼티를 정의합니다. 첫 번째 `thresholdLevel`은 오디오 레벨이 취할 수 있는 최대 임계값을 정의합니다. 이 값은 모든 `AudioChannel`인스턴스에 대해 상수 값 `10`입니다. 오디오 신호가 `10`보다 높은 값으로 들어오면 아래 설명된 대로 이 임계값으로 제한됩니다.

*The second type property is a variable stored property called `maxInputLevelForAllChannels`. This keeps track of the maximum input value that has been received by any `AudioChannel` instance. It starts with an initial value of `0`.*

두 번째 타입 프로퍼티는 `maxInputLevelForAllChannels`라는 변수 저장 프로퍼티입니다. 이것은 모든 `AudioChannel`인스턴스가 수신한 최대 입력 값을 추적합니다. 초기값 `0`으로 시작합니다.

*The `AudioChannel` structure also defines a stored instance property called `currentLevel`, which represents the channel’s current audio level on a scale of `0` to `10`.*

 `AudioChannel`구조체는 또한 `currentLevel`이라는 저장 인스턴스 프로퍼티를 정의합니다. 이 프로퍼티는 채널의 현재 오디오 레벨을 `0`에서 `10`사이의 척도로 나타냅니다.

*The `currentLevel` property has a `didSet` property observer to check the value of `currentLevel` whenever it’s set. This observer performs two checks:*

`currentLevel` 프로퍼티에는 설정될 때마다 `currentLevel` 값을 확인하는 `didSet` 프로퍼티 옵저버가 있습니다. 이 옵저버는 두 가지 검사를 수행합니다:

- *If the new value of `currentLevel` is greater than the allowed `thresholdLevel`, the property observer caps `currentLevel` to `thresholdLevel`.*
  
  `currentLevel`의 새 값이 허용된 `thresholdLevel`보다 크면 프로퍼티 옵저버는 `currentLevel`을 `thresholdLevel`로 캡핑(?)합니다.

- *If the new value of `currentLevel` (after any capping) is higher than any value previously received by any `AudioChannel` instance, the property observer stores the new `currentLevel` value in the `maxInputLevelForAllChannels` type property.*
  
  `currentLevel`의 새 값(캡핑 후)이 이전에 `AudioChannel` 인스턴스에서 수신한 값보다 높은 경우  프로퍼티 옵저버는 새 `currentLevel` 값을 `maxInputLevelForAllChannels` 타입 프로퍼티에 저장합니다.

> *NOTE*
> 
> *In the first of these two checks, the `didSet` observer sets `currentLevel` to a different value. This doesn’t, however, cause the observer to be called again.*
> 
> 이 두 검사 중 첫 번째 검사에서 `didSet` 옵저버는 `currentLevel`을 다른 값으로 설정합니다. 그러나 이것이 옵저버를 다시 불러오게 하는 원인은 아닙니다.

*You can use the `AudioChannel` structure to create two new audio channels called `leftChannel` and `rightChannel`, to represent the audio levels of a stereo sound system:*

`AudioChannel`구조체를 사용하여 스테레오 사운드 시스템의 오디오 레벨을 나타내기 위해 `leftChannel`과 `rightChannel`이라는 두 개의 새로운 오디오 채널을 만들 수 있습니다:

```swift
var leftChannel = AudioChannel()
var rightChannel = AudioChannel()
```

*If you set the `currentLevel` of the left channel to `7`, you can see that the `maxInputLevelForAllChannels` type property is updated to equal `7`:*

왼쪽 채널의 `currentLevel`을 `7`로 설정하면 `maxInputLevelForAllChannels` 타입 프로퍼티가 `7`과 동일하게 업데이트됨을 알 수 있습니다.

```swift
leftChannel.currentLevel = 7
print(leftChannel.currentLevel)
// Prints "7"
print(AudioChannel.maxInputLevelForAllChannels)
// Prints "7"
```

*If you try to set the `currentLevel` of the right channel to `11`, you can see that the right channel’s `currentLevel` property is capped to the maximum value of `10`, and the `maxInputLevelForAllChannels` type property is updated to equal `10`:*

오른쪽 채널의 `currentLevel`을 `11`로 설정하려고 하면 오른쪽 채널의 `currentLevel` 프로퍼티가 최대값인 `10`으로 제한되고 `maxInputLevelForAllChannels` 타입 프로퍼티가 10과 동일하게 업데이트됨을 알 수 있습니다:

```swift
rightChannel.currentLevel = 11
print(rightChannel.currentLevel)
// Prints "10"
print(AudioChannel.maxInputLevelForAllChannels)
// Prints "10"
```
