## *Property Wrappers : 프로퍼티 래퍼*

*A property wrapper adds a layer of separation between code that manages how a property is stored and the code that defines a property. For example, if you have properties that provide thread-safety checks or store their underlying data in a database, you have to write that code on every property. When you use a property wrapper, you write the management code once when you define the wrapper, and then reuse that management code by applying it to multiple properties.*

프로퍼티 래퍼는 프로퍼티가 저장되는 방법을 관리하는 코드와 프로퍼티를 정의하는 코드 사이에 분리 계층을 추가합니다. 예를 들어 스레드 안전 검사를 제공하거나 해당 기본 데이터를 데이터베이스에 저장하는 프로퍼티가 있는 경우 모든 프로퍼티에 해당 코드를 작성해야 합니다. 프로퍼티 래퍼를 사용하는 경우 래퍼를 정의할 때 관리 코드를 한 번 작성한 다음 여러 프로퍼티에 적용하여 해당 관리 코드를 다시 사용합니다.

*To define a property wrapper, you make a structure, enumeration, or class that defines a `wrappedValue` property. In the code below, the `TwelveOrLess` structure ensures that the value it wraps always contains a number less than or equal to 12. If you ask it to store a larger number, it stores 12 instead.*

프로퍼티 래퍼를 정의하려면 `wrappedValue`프로퍼티를 정의하는 구조체, 열거형 또는 클래스를 만듭니다. 아래 코드에서 `TwelveOrLess` 구조체는 래핑되는 값이 항상 12보다 작거나 같은 숫자를 포함하도록 합니다. 더 큰 숫자를 저장하도록 요청하면 대신 12개를 저장합니다.

```swift
@propertyWrapper
struct TwelveOrLess {
    private var number = 0
    var wrappedValue: Int {
        get { return number }
        set { number = min(newValue, 12) }
    }
}
```

*The setter ensures that new values are less than or equal to 12, and the getter returns the stored value.*

세터는 새 값이 12보다 작거나 같은지 확인하고, 게터는 저장된 값을 반환합니다.

> *NOTE*
> 
> *The declaration for `number` in the example above marks the variable as `private`, which ensures `number` is used only in the implementation of `TwelveOrLess`. Code that’s written anywhere else accesses the value using the getter and setter for `wrappedValue`, and can’t use `number` directly. For information about `private`, see [Access Control](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html).*
> 
> 위의 예에서 `number`에 대한 선언은 변수를 `private`로 표시하여 `number`가 `TwelveOrLess`의 구현에서만 사용되도록 합니다. 다른 곳에 작성된 코드는 `wrappedValue`에 대한 getter 및 setter를 사용하여 값에 액세스하고 `number`를 직접 사용할 수 없습니다. `private`에 대한 자세한 내용은 [링크]를 참조하세요.

*You apply a wrapper to a property by writing the wrapper’s name before the property as an attribute. Here’s a structure that stores a rectangle that uses the `TwelveOrLess` property wrapper to ensure its dimensions are always 12 or less:*

프로퍼티 앞에 래퍼의 이름을 프로퍼티로 작성하여 프로퍼티에 래퍼를 적용합니다. 다음은 `TwelveOrLess` 프로퍼티 래퍼를 사용하여 치수가 항상 12 이하가 되도록 하는 직사각형을 저장하는 구조입니다:

```swift
struct SmallRectangle {
    @TwelveOrLess var height: Int
    @TwelveOrLess var width: Int
}

var rectangle = SmallRectangle()
print(rectangle.height)
// Prints "0"

rectangle.height = 10
print(rectangle.height)
// Prints "10"

rectangle.height = 24
print(rectangle.height)
// Prints "12"
```

*The `height` and `width` properties get their initial values from the definition of `TwelveOrLess`, which sets `TwelveOrLess.number` to zero. The setter in `TwelveOrLess` treats 10 as a valid value so storing the number 10 in `rectangle.height` proceeds as written. However, 24 is larger than `TwelveOrLess` allows, so trying to store 24 end up setting `rectangle.height` to 12 instead, the largest allowed value.*

 `height` 와 `width`프로퍼티는 `TwelveOrLess.number`를 0으로 설정하는 `TwelveOrLess`의 정의에서 초기 값을 가져옵니다. `TwelveOrLess`의 세터는 10을 유효한 값으로 취급하여 숫자 10을 `rectangle.height`에 저장하고 쓰여진 대로 진행됩니다. 그러나 24는 `TwelveOrLess`가 허용하는 것보다 크기 때문에 24를 저장하려고 하면 `rectangle.height`을 대신 허용되는 가장 큰 값인12로 설정하게 됩니다.

*When you apply a wrapper to a property, the compiler synthesizes code that provides storage for the wrapper and code that provides access to the property through the wrapper. (The property wrapper is responsible for storing the wrapped value, so there’s no synthesized code for that.) You could write code that uses the behavior of a property wrapper, without taking advantage of the special attribute syntax. For example, here’s a version of `SmallRectangle` from the previous code listing that wraps its properties in the `TwelveOrLess` structure explicitly, instead of writing `@TwelveOrLess` as an attribute:*

래퍼를 프로퍼티에 적용하면 컴파일러는 래퍼에 대한 저장소를 제공하는 코드와 래퍼를 통해 프로퍼티에 대한 액세스를 제공하는 코드를 합성합니다. (프로퍼티 래퍼는 랩핑된 값을 저장하는 역할을 하므로 합성된 코드는 없습니다.) 특수 프로퍼티 구문을 사용하지 않고 프로퍼티 래퍼의 동작을 사용하는 코드를 작성할 수 있습니다. 예를 들어 다음은 프로퍼티로 `@TwelveOrLess`를 쓰는 대신 명시적으로 `TwelveOrLess` 구조체로 프로퍼티를 감싸는 이전 코드 목록의 `SmallRectangle` 버전입니다:

```swift
struct SmallRectangle {
    private var _height = TwelveOrLess()
    private var _width = TwelveOrLess()
    var height: Int {
        get { return _height.wrappedValue }
        set { _height.wrappedValue = newValue }
    }
    var width: Int {
        get { return _width.wrappedValue }
        set { _width.wrappedValue = newValue }
    }
}
```

*The `_height` and `_width` properties store an instance of the property wrapper, `TwelveOrLess`. The getter and setter for `height` and `width` wrap access to the `wrappedValue` property.*

`_height` 및 `_width` 프로퍼티는 프로퍼티 래퍼 `TwelveOrLess`의 인스턴스를 저장합니다. `height` 및 `width`에 대한 게터 및 세터는 `wrappedValue` 프로퍼티에 대한 액세스를 래핑합니다.

### *Setting Initial Values for Wrapped Properties : 래핑된 특성의 초기 값을 설정*

*The code in the examples above sets the initial value for the wrapped property by giving `number` an initial value in the definition of `TwelveOrLess`. Code that uses this property wrapper can’t specify a different initial value for a property that’s wrapped by `TwelveOrLess`—for example, the definition of `SmallRectangle` can’t give `height` or `width` initial values. To support setting an initial value or other customization, the property wrapper needs to add an initializer. Here’s an expanded version of `TwelveOrLess` called `SmallNumber` that defines initializers that set the wrapped and maximum value:*

위 예제의 코드는 `TwelveOrLess`의 정의에서 `number`에게 초기 값을 제공하여 랩핑된 프로퍼티의 초기 값을 설정합니다. 이 프로퍼티 래퍼를 사용하는 코드는 `TwelveOrLess`로 둘러싸인 프로퍼티의 다른 초기 값을 지정할 수 없습니다. 예를 들어, `SmallRectangle`의 정의는 `height` 또는 `width` 초기 값을 제공할 수 없습니다. 초기 값 설정 또는 기타 사용자 지정을 지원하려면 프로퍼티 래퍼에서 이니셜라이저를 추가해야 합니다. 다음은 래핑된 값과 최대값을 설정하는 초기화자를 정의하는 `SmallNumber`라는 확장 버전의 `TwelveOrLess`입니다:

```swift
@propertyWrapper
struct SmallNumber {
    private var maximum: Int
    private var number: Int

    var wrappedValue: Int {
        get { return number }
        set { number = min(newValue, maximum) }
    }

    init() {
        maximum = 12
        number = 0
    }
    init(wrappedValue: Int) {
        maximum = 12
        number = min(wrappedValue, maximum)
    }
    init(wrappedValue: Int, maximum: Int) {
        self.maximum = maximum
        number = min(wrappedValue, maximum)
    }
}
```

*The definition of `SmallNumber` includes three initializers—`init()`, `init(wrappedValue:)`, and `init(wrappedValue:maximum:)`—which the examples below use to set the wrapped value and the maximum value. For information about initialization and initializer syntax, see [Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html).*

`SmallNumber`의 정의에는 `init()`, `init(wrappedValue:)`와 `init(wrappedValue:maximum:)`의 세 가지 이니셜라이저가 포함됩니다—아래 예제에서는 래핑된 값과 최대값을 설정하는 데 사용합니다. 초기화 및 초기화 구문에 대한 자세한 내용은 [Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)을 참조하세요.

*When you apply a wrapper to a property and you don’t specify an initial value, Swift uses the `init()` initializer to set up the wrapper. For example:*

프로퍼티에 래퍼를 적용하고 초기 값을 지정하지 않으면 Swift는 `init()` 이니셜라이저를 사용하여 래퍼를 설정합니다. 예를 들어 다음과 같습니다:

```swift
struct ZeroRectangle {
    @SmallNumber var height: Int
    @SmallNumber var width: Int
}

var zeroRectangle = ZeroRectangle()
print(zeroRectangle.height, zeroRectangle.width)
// Prints "0 0"
```

*The instances of `SmallNumber` that wrap `height` and `width` are created by calling `SmallNumber()`. The code inside that initializer sets the initial wrapped value and the initial maximum value, using the default values of zero and 12. The property wrapper still provides all of the initial values, like the earlier example that used `TwelveOrLess` in `SmallRectangle`. Unlike that example, `SmallNumber` also supports writing those initial values as part of declaring the property.*

`height`와 `width`를 감싸는 `SmallNumber`의 인스턴스는 `SmallNumber()`를 호출하여 생성됩니다. 이 이니셜라이저 내부의 코드는 기본값 0과 12를 사용하여 초기 래핑 값과 초기 최대값을 설정합니다. 프로퍼티 래퍼는 `SmallRectangle`에서 `TwelveOrLess`를 사용한 이전 예제와 같이 여전히 모든 초기 값을 제공합니다. 이 예와 달리 `SmallNumber`는 프로퍼티 선언의 일부로 이러한 초기 값을 쓰는 것도 지원합니다.

*When you specify an initial value for the property, Swift uses the `init(wrappedValue:)` initializer to set up the wrapper. For example:*

프로퍼티의 초기 값을 지정하면 Swift는 `init(wrappedValue:)` 이니셜라이저를 사용하여 래퍼를 설정합니다. 예를 들어 다음과 같습니다:

```swift
struct UnitRectangle {
    @SmallNumber var height: Int = 1
    @SmallNumber var width: Int = 1
}

var unitRectangle = UnitRectangle()
print(unitRectangle.height, unitRectangle.width)
// Prints "1 1"
```

*When you write `= 1` on a property with a wrapper, that’s translated into a call to the `init(wrappedValue:)` initializer. The instances of `SmallNumber` that wrap `height` and `width` are created by calling `SmallNumber(wrappedValue: 1)`. The initializer uses the wrapped value that’s specified here, and it uses the default maximum value of 12.*

래퍼가 있는 프로퍼티에 `= 1`을 쓰면 `init(wrappedValue:)` 이니셜라이저 호출로 변환됩니다. `height`와 `width`를 감싸는 `SmallNumber`의 인스턴스는 `SmallNumber(wrappedValue: 1)`를 호출하여 생성됩니다. 이니셜라이저는 여기에 지정된 래핑된 값을 사용하며 기본 최대값인 12를 사용합니다.

*When you write arguments in parentheses after the custom attribute, Swift uses the initializer that accepts those arguments to set up the wrapper. For example, if you provide an initial value and a maximum value, Swift uses the `init(wrappedValue:maximum:)` initializer:*

사용자 지정 프로퍼티 뒤에 괄호 안에 인수를 작성하면 Swift는 해당 인수를 수락하는 이니셜라이저를 사용하여 래퍼를 설정합니다. 예를 들어, 초기 값과 최대값을 제공하는 경우 Swift는 `init(wrappedValue:maximum:)` 이니셜라이저를 사용합니다.

```swift
struct NarrowRectangle {
    @SmallNumber(wrappedValue: 2, maximum: 5) var height: Int
    @SmallNumber(wrappedValue: 3, maximum: 4) var width: Int
}

var narrowRectangle = NarrowRectangle()
print(narrowRectangle.height, narrowRectangle.width)
// Prints "2 3"

narrowRectangle.height = 100
narrowRectangle.width = 100
print(narrowRectangle.height, narrowRectangle.width)
// Prints "5 4"
```

*The instance of `SmallNumber` that wraps `height` is created by calling `SmallNumber(wrappedValue: 2, maximum: 5)`, and the instance that wraps `width` is created by calling `SmallNumber(wrappedValue: 3, maximum: 4)`.*

`height`를 감싸는 `SmallNumber`의 인스턴스는 `SmallNumber(wrappedValue: 2, maximum: 5)`를 호출하여 생성되고, `width`를 감싸는 인스턴스는  `SmallNumber(wrappedValue: 3, maximum: 4)`를 호출하여 생성됩니다.

*By including arguments to the property wrapper, you can set up the initial state in the wrapper or pass other options to the wrapper when it’s created. This syntax is the most general way to use a property wrapper. You can provide whatever arguments you need to the attribute, and they’re passed to the initializer.*

프로퍼티 래퍼에 인수를 포함하여 래퍼의 초기 상태를 설정하거나 래퍼가 생성될 때 다른 옵션을 래퍼에 전달할 수 있습니다. 이 구문은 프로퍼티 래퍼를 사용하는 가장 일반적인 방법입니다. 프로퍼티에 필요한 모든 인수를 제공할 수 있으며 이 인수는 이니셜라이저로 전달됩니다.

*When you include property wrapper arguments, you can also specify an initial value using assignment. Swift treats the assignment like a `wrappedValue` argument and uses the initializer that accepts the arguments you include. For example:*

프로퍼티 래퍼 인수를 포함할 때 할당을 사용하여 초기 값을 지정할 수도 있습니다. Swift는 할당을 'wrappedValue' 인수처럼 처리하고 사용자가 포함한 인수를 수락하는 이니셜라이저를 사용합니다. 예를 들어 :

```swift
struct MixedRectangle {
    @SmallNumber var height: Int = 1
    @SmallNumber(maximum: 9) var width: Int = 2
}

var mixedRectangle = MixedRectangle()
print(mixedRectangle.height)
// Prints "1"

mixedRectangle.height = 20
print(mixedRectangle.height)
// Prints "12"
```

*The instance of `SmallNumber` that wraps `height` is created by calling `SmallNumber(wrappedValue: 1)`, which uses the default maximum value of 12. The instance that wraps `width` is created by calling `SmallNumber(wrappedValue: 2, maximum: 9)`.*

`height`를 감싸는 `SmallNumber` 인스턴스는 기본 최대값인 12를 사용하는 `SmallNumber(wrappedValue: 1)`를 호출하여 생성됩니다. `width`를 래핑하는 인스턴스는 `SmallNumber(wrappedValue: 2, maximum: 9)`를 호출하여 생성됩니다.

### *Projecting a Value From a Property Wrapper : 프로퍼티 래퍼에서 값을 투영*

*In addition to the wrapped value, a property wrapper can expose additional functionality by defining a projected value—for example, a property wrapper that manages access to a database can expose a `flushDatabaseConnection()` method on its projected value. The name of the projected value is the same as the wrapped value, except it begins with a dollar sign (`$`). Because your code can’t define properties that start with `$` the projected value never interferes with properties you define.*

래핑된 값 외에도 프로퍼티 래퍼는 투영된 값을 정의하여 추가 기능을 노출할 수 있습니다. 예를 들어 데이터베이스에 대한 액세스를 관리하는 프로퍼티 래퍼는 투영된 값에 `flushDatabaseConnection()` 메서드를 노출할 수 있습니다. 예상 값의 이름은 달러 기호(`$`)로 시작하는 것을 제외하고는 포장된 값과 동일합니다. 코드가 `$`로 시작하는 프로퍼티를 정의할 수 없기 때문에 투영된 값은 정의하는 프로퍼티를 간섭하지 않습니다.

*In the `SmallNumber` example above, if you try to set the property to a number that’s too large, the property wrapper adjusts the number before storing it. The code below adds a `projectedValue` property to the `SmallNumber` structure to keep track of whether the property wrapper adjusted the new value for the property before storing that new value.*

위의 `SmallNumber` 예제에서 프로퍼티를 너무 큰 숫자로 설정하려고 하면 프로퍼티 래퍼가 저장하기 전에 값을 조정합니다. 아래 코드는 프로퍼티 래퍼가 새 값을 저장하기 전에 프로퍼티에 대한 새 값을 조정했는지 여부를 추적하기 위해 `smallNumber` 구조체에 `projectedValue` 프로퍼티를 추가합니다.

```swift
@propertyWrapper
struct SmallNumber {
    private var number: Int
    private(set) var projectedValue: Bool

    var wrappedValue: Int {
        get { return number }
        set {
            if newValue > 12 {
                number = 12
                projectedValue = true
            } else {
                number = newValue
                projectedValue = false
            }
        }
    }

    init() {
        self.number = 0
        self.projectedValue = false
    }
}
struct SomeStructure {
    @SmallNumber var someNumber: Int
}
var someStructure = SomeStructure()

someStructure.someNumber = 4
print(someStructure.$someNumber)
// Prints "false"

someStructure.someNumber = 55
print(someStructure.$someNumber)
// Prints "true"
```

*Writing `someStructure.$someNumber` accesses the wrapper’s projected value. After storing a small number like four, the value of `someStructure.$someNumber` is `false`. However, the projected value is `true` after trying to store a number that’s too large, like 55.*

`someStructure.$someNumber`를 쓰면 래퍼의 투영된 값에 액세스합니다. 4와 같이 작은 숫자를 저장한 후 `someStructure.$someNumber`의 값은 `false`입니다. 그러나 55와 같이 너무 큰 숫자를 저장하려고 하면 예상 값이 `true`가 됩니다.

*A property wrapper can return a value of any type as its projected value. In this example, the property wrapper exposes only one piece of information—whether the number was adjusted—so it exposes that Boolean value as its projected value. A wrapper that needs to expose more information can return an instance of some other data type, or it can return `self` to expose the instance of the wrapper as its projected value.*

프로퍼티 래퍼는 모든 타입의 값을 투영된 값으로 반환할 수 있습니다. 이 예에서 프로퍼티 래퍼는 숫자가 조정되었는지 여부에 관계없이 하나의 정보만 표시하므로 Bool 값을 투영된 값으로 표시합니다. 더 많은 정보를 노출해야 하는 래퍼는 다른 데이터 타입의 인스턴스를 반환하거나 `self`를 반환하여 래퍼의 인스턴스를 투영된 값으로 노출할 수 있습니다.

*When you access a projected value from code that’s part of the type, like a property getter or an instance method, you can omit `self.` before the property name, just like accessing other properties. The code in the following example refers to the projected value of the wrapper around `height` and `width` as `$height` and `$width`:*

프로퍼티 게터나 인스턴스 메서드와 같이 타입의 일부인 코드에서 투영된 값에 액세스할 때 다른 프로퍼티에 액세스하는 것과 마찬가지로 프로퍼티 이름 앞에 `self.`를 생략할 수 있습니다. 다음 예제의 코드는 `height`와 `width` 주변의 래퍼의 예상 값을 `$height`와 `$width`로 나타냅니다:

```swift
enum Size {
    case small, large
}

struct SizedRectangle {
    @SmallNumber var height: Int
    @SmallNumber var width: Int

    mutating func resize(to size: Size) -> Bool {
        switch size {
        case .small:
            height = 10
            width = 20
        case .large:
            height = 100
            width = 100
        }
        return $height || $width
    }
}
```

*Because property wrapper syntax is just syntactic sugar for a property with a getter and a setter, accessing `height` and `width` behaves the same as accessing any other property. For example, the code in `resize(to:)` accesses `height` and `width` using their property wrapper. If you call `resize(to: .large)`, the switch case for `.large` sets the rectangle’s height and width to 100. The wrapper prevents the value of those properties from being larger than 12, and it sets the projected value to `true`, to record the fact that it adjusted their values. At the end of `resize(to:)`, the return statement checks `$height` and `$width` to determine whether the property wrapper adjusted either `height` or `width`.*

프로퍼티 래퍼 구문은 게터와 세터가 있는 프로퍼티에 대한 syntactic sugar일 뿐이므로 `height`와 `height`에 액세스하는 것은 다른 프로퍼티에 액세스하는 것과 동일하게 동작합니다. 예를 들어 `resize(to:)`의 코드는 프로퍼티 래퍼를 사용하여 `height`와 `width`에 액세스합니다. `resize (to: .large)`를 호출하면 `.large`의 스위치 케이스가 직사각형의 높이와 너비를 100으로 설정합니다. 래퍼는 이러한  프로퍼티의 값이 12보다 큰 것을 방지하고 예측 값을 `true`로 설정하여 값을 조정했다는 사실을 기록합니다. `resize(to:)`가 끝나면 반환문은"`$hight`와 `$width`를 확인하여 프로퍼티 래퍼가 `height` 또는 `width`를 조정했는지 여부를 결정합니다.
