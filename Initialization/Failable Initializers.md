## *Failable Initializers : 실패할 수 있는 이니셜라이저*

*It’s sometimes useful to define a class, structure, or enumeration for which initialization can fail. This failure might be triggered by invalid initialization parameter values, the absence of a required external resource, or some other condition that prevents initialization from succeeding.*

초기화가 실패할 수 있는 클래스, 구조체 또는 열거형을 정의하는 것이 유용할 수 있습니다. 이 실패는 잘못된 초기화 매개 변수 값, 필요한 외부 리소스가 없거나 초기화가 성공하지 못하게 하는 다른 조건으로 인해 트리거될 수 있습니다.

*To cope with initialization conditions that can fail, define one or more failable initializers as part of a class, structure, or enumeration definition. You write a failable initializer by placing a question mark after the `init` keyword (`init?`).*

실패할 수 있는 초기화 조건에 대처하려면 클래스, 구조체 또는 열거형 정의의 일부로 하나 이상의 실패할 수 있는 이니셜라이저를 정의합니다. `init` 키워드 뒤에 물음표를 붙여 실패한 이니셜라이저를 작성합니다.(`init?`)

> *NOTE*
> 
> *You can’t define a failable and a nonfailable initializer with the same parameter types and names.*
> 
> 실패 가능한 이니셜라이저와 사용 불가능한 이니셜라이저를 동일한 매개 변수 타입 및 이름으로 정의할 수 없습니다.

*A failable initializer creates an optional value of the type it initializes. You write `return nil` within a failable initializer to indicate a point at which initialization failure can be triggered.*

실패 가능한 이니셜라이저는 초기화하는 타입의 옵셔널 값을 생성합니다. 초기화 실패가 트리거될 수 있는 지점을 나타내기 위해 실패 가능한 이니셜라이저 내에 `return nil`을 씁니다.

> *NOTE*
> 
> *Strictly speaking, initializers don’t return a value. Rather, their role is to ensure that `self` is fully and correctly initialized by the time that initialization ends. Although you write `return nil` to trigger an initialization failure, you don’t use the `return` keyword to indicate initialization success.*
> 
> 엄밀히 말하면 이니셜라이저는 값을 반환하지 않습니다. 오히려 그들의 역할은 초기화가 끝날 때까지 `self`가 완전하고 정확하게 초기화되도록 하는 것입니다. 초기화 실패를 트리거하기 위해 `return nil`을 쓰더라도 초기화 성공을 나타내기 위해 `return` 키워드를 사용하지는 않습니다.

*For instance, failable initializers are implemented for numeric type conversions. To ensure conversion between numeric types maintains the value exactly, use the `init(exactly:)` initializer. If the type conversion can’t maintain the value, the initializer fails.*

예를 들어, 숫자 타입 변환에는 실패 가능한 이니셜라이저가 구현됩니다. 숫자 타입 간의 변환이 값을 정확하게 유지하도록 하려면 `init(exactly:)` 이니셜라이저를 사용하십시오. 타입 변환에서 값을 유지할 수 없으면 초기화가 실패합니다.

```swift
let wholeNumber: Double = 12345.0
let pi = 3.14159

if let valueMaintained = Int(exactly: wholeNumber) {
    print("\(wholeNumber) conversion to Int maintains value of \(valueMaintained)")
}
// Prints "12345.0 conversion to Int maintains value of 12345"

let valueChanged = Int(exactly: pi)
// valueChanged is of type Int?, not Int

if valueChanged == nil {
    print("\(pi) conversion to Int doesn't maintain value")
}
// Prints "3.14159 conversion to Int doesn't maintain value"
```

*The example below defines a structure called `Animal`, with a constant `String` property called `species`. The `Animal` structure also defines a failable initializer with a single parameter called `species`. This initializer checks if the `species` value passed to the initializer is an empty string. If an empty string is found, an initialization failure is triggered. Otherwise, the `species` property’s value is set, and initialization succeeds:*

아래 예제는 `species`라는 상수 `String` 프로퍼티를 가지는 `Animal`이라는 구조체를 정의합니다. `Animal` 구조체는 또한 `species`라는 단일 매개 변수를 사용하여 실패 가능한 이니셜라이저를 정의합니다. 이 이니셜라이저는 이니셜라이저에 전달된 `species` 값이 빈 문자열인지 확인합니다. 빈 문자열이 발견되면 초기화 실패가 트리거됩니다. 그렇지 않으면  `species` 프로퍼티의 값이 설정되고 초기화가 성공합니다:

```swift
struct Animal {
    let species: String
    init?(species: String) {
        if species.isEmpty { return nil }
        self.species = species
    }
}
```

*You can use this failable initializer to try to initialize a new `Animal` instance and to check if initialization succeeded:*

이 실패 가능한 이니셜라이저를 사용하여 새 `Animal` 인스턴스를 초기화하고 초기화가 성공했는지 확인할 수 있습니다:

```swift
let someCreature = Animal(species: "Giraffe")
// someCreature is of type Animal?, not Animal

if let giraffe = someCreature {
    print("An animal was initialized with a species of \(giraffe.species)")
}
// Prints "An animal was initialized with a species of Giraffe"
```

*If you pass an empty string value to the failable initializer’s `species` parameter, the initializer triggers an initialization failure:*

빈 문자열 값을 실패한 이니셜라이저의 `species` 매개 변수에 전달하면 이니셜라이저가 초기화 실패를 트리거합니다:

```swift
let anonymousCreature = Animal(species: "")
// anonymousCreature is of type Animal?, not Animal

if anonymousCreature == nil {
    print("The anonymous creature couldn't be initialized")
}
// Prints "The anonymous creature couldn't be initialized"
```

> *NOTE*
> 
> *Checking for an empty string value (such as `""` rather than `"Giraffe"`) isn’t the same as checking for `nil` to indicate the absence of an optional `String` value. In the example above, an empty string (`""`) is a valid, non-optional `String`. However, it’s not appropriate for an animal to have an empty string as the value of its `species` property. To model this restriction, the failable initializer triggers an initialization failure if an empty string is found.*
> 
> 빈 문자열 값(예: `"Giraffe"`가 아닌 `""`)을 확인하는 것은 옵셔널 `String` 값이 없음을 나타내기 위해 `nil`을 확인하는 것과 같지 않습니다. 위의 예에서 빈 문자열(`""`)은 옵셔널이 아닌 유효한 문자열입니다. 그러나 동물이 `species`의 프로퍼티 값으로 빈 String을 갖는 것은 적절치 않습니다. 이 제한을 모델링하기 위해 실패 가능한 이니셜라이저는 빈 문자열이 발견될 경우 초기화 실패를 트리거합니다.

### *Failable Initializers for Enumerations : 열거형에서 실패할 수 있는 이니셜라이저*

*You can use a failable initializer to select an appropriate enumeration case based on one or more parameters. The initializer can then fail if the provided parameters don’t match an appropriate enumeration case.*

실패 가능한 이니셜라이저 사용하여 하나 이상의 매개 변수를 기준으로 적절한 열거형 케이스를 선택할 수 있습니다. 그런 다음 제공된 매개 변수가 적절한 열거형 케이스와 일치하지 않으면 초기화가 실패할 수 있습니다.

*The example below defines an enumeration called `TemperatureUnit`, with three possible states (`kelvin`, `celsius`, and `fahrenheit`). A failable initializer is used to find an appropriate enumeration case for a `Character` value representing a temperature symbol:*

아래 예제는 세 가지 상태(`kelvin`, `celsius`, 그리고 `fahrenheit`)를 가진 `TemperatureUnit`이라는 열거형을 정의합니다. 실패 가능한 이니셜라이저는 온도 기호를 나타내는 `Character` 값에 대한 적절한 열거형 케이스를 찾는 데 사용됩니다:

```swift
enum TemperatureUnit {
    case kelvin, celsius, fahrenheit
    init?(symbol: Character) {
        switch symbol {
        case "K":
            self = .kelvin
        case "C":
            self = .celsius
        case "F":
            self = .fahrenheit
        default:
            return nil
        }
    }
}
```

*You can use this failable initializer to choose an appropriate enumeration case for the three possible states and to cause initialization to fail if the parameter doesn’t match one of these states:*

이 실패 가능한 이니셜라이저를 사용하여 세 가지 가능한 상태에 대한 적절한 열거 사례를 선택하고 매개 변수가 다음 상태 중 하나와 일치하지 않을 경우 초기화가 실패하도록 할 수 있습니다:

```swift
let fahrenheitUnit = TemperatureUnit(symbol: "F")
if fahrenheitUnit != nil {
    print("This is a defined temperature unit, so initialization succeeded.")
}
// Prints "This is a defined temperature unit, so initialization succeeded."

let unknownUnit = TemperatureUnit(symbol: "X")
if unknownUnit == nil {
    print("This isn't a defined temperature unit, so initialization failed.")
}
// Prints "This isn't a defined temperature unit, so initialization failed."
```

### *Failable Initializers for Enumerations with Raw Values : 원시값을 가지는 열거형에 대한 실패할 수 있는 이니셜라이저*

*Enumerations with raw values automatically receive a failable initializer, `init?(rawValue:)`, that takes a parameter called `rawValue` of the appropriate raw-value type and selects a matching enumeration case if one is found, or triggers an initialization failure if no matching value exists.*

원시 값이 있는 열거형은 적절한 원시 값 타입의 `rawValue`라는 매개 변수를 가져와서 일치하는 열거 사례를 선택하는 실패 가능한 초기화기 'init?(rawValue:)'를 자동으로 수신하거나 일치하는 값이 없으면 초기화 실패를 트리거합니다.

*You can rewrite the `TemperatureUnit` example from above to use raw values of type `Character` and to take advantage of the `init?(rawValue:)` initializer:*

위에서 `TemperatureUnit` 예제를 다시 작성하여 `Character` 타입의 원시 값을 사용하고 `init?(rawValue:)` 이니셜라이저를 활용할 수 있습니다:

```swift
enum TemperatureUnit: Character {
    case kelvin = "K", celsius = "C", fahrenheit = "F"
}

let fahrenheitUnit = TemperatureUnit(rawValue: "F")
if fahrenheitUnit != nil {
    print("This is a defined temperature unit, so initialization succeeded.")
}
// Prints "This is a defined temperature unit, so initialization succeeded."

let unknownUnit = TemperatureUnit(rawValue: "X")
if unknownUnit == nil {
    print("This isn't a defined temperature unit, so initialization failed.")
}
// Prints "This isn't a defined temperature unit, so initialization failed."
```

### *Propagation of Initialization Failure : 초기화 실패 전파*

*A failable initializer of a class, structure, or enumeration can delegate across to another failable initializer from the same class, structure, or enumeration. Similarly, a subclass failable initializer can delegate up to a superclass failable initializer.*

클래스, 구조체 또는 열거형의 실패 가능한 이니셜라이저는 동일한 클래스, 구조체 또는 열거형의 다른 실패 가능한 이니셜라이저에 위임할 수 있습니다. 마찬가지로 하위 클래스의 실패 가능한 이니셜라이저는 최대 슈퍼 클래스 실패 가능한 이니셜라이저까지 위임할 수 있습니다.

*In either case, if you delegate to another initializer that causes initialization to fail, the entire initialization process fails immediately, and no further initialization code is executed.*

어느 경우든 초기화가 실패하는 다른 이니셜라이저에 위임하면 전체 초기화 프로세스가 즉시 실패하고 이후의 초기화 코드는 실행되지 않습니다.

> *NOTE*
> 
> *A failable initializer can also delegate to a nonfailable initializer. Use this approach if you need to add a potential failure state to an existing initialization process that doesn’t otherwise fail.*
> 
> 실패할 수 있는 이니셜라이저도 실패할 수 없는 이니셜라이저로 위임할 수 있습니다. 실패하지 않는 기존 초기화 프로세스에 잠재적인 실패 상태를 추가해야 하는 경우 이 방법을 사용합니다.

*The example below defines a subclass of `Product` called `CartItem`. The `CartItem` class models an item in an online shopping cart. `CartItem` introduces a stored constant property called `quantity` and ensures that this property always has a value of at least `1`:*

아래 예제는 `CartItem`이라는 `Product`의 하위 클래스를 정의합니다. `CartItem` 클래스는 온라인 쇼핑 카트의 항목을 모델링합니다. `CartItem`은 `quantity`라는 상수 저장 프로퍼티를 도입하고 이 프로퍼티가 항상 최소 `1`의 값을 갖도록 합니다:

```swift
class Product {
    let name: String
    init?(name: String) {
        if name.isEmpty { return nil }
        self.name = name
    }
}

class CartItem: Product {
    let quantity: Int
    init?(name: String, quantity: Int) {
        if quantity < 1 { return nil }
        self.quantity = quantity
        super.init(name: name)
    }
}
```

*The failable initializer for `CartItem` starts by validating that it has received a `quantity` value of `1` or more. If the `quantity` is invalid, the entire initialization process fails immediately and no further initialization code is executed. Likewise, the failable initializer for `Product` checks the `name` value, and the initializer process fails immediately if `name` is the empty string.*

`CartItem`에 대한 실패 가능한 이니셜라이저는 `quantity` 값이 `1`이상인지 확인하는 것으로 시작합니다. `quantity`가 올바르지 않으면 전체 초기화 프로세스가 즉시 실패하고 더 이상의 초기화 코드가 실행되지 않습니다. 마찬가지로 `Product`에 대한 실패 가능한 이니셜라이저는 `name` 값을 확인하고, `name`이 빈 문자열이면 이니셜라이저 프로세스는 즉시 실패합니다.

*If you create a `CartItem` instance with a nonempty name and a quantity of `1` or more, initialization succeeds:*

이름이 비어 있지 않고 수량이 `1` 이상인 `CartItem` 인스턴스를 만들면 초기화가 성공합니다:

```swift
if let twoSocks = CartItem(name: "sock", quantity: 2) {
    print("Item: \(twoSocks.name), quantity: \(twoSocks.quantity)")
}
// Prints "Item: sock, quantity: 2"
```

*If you try to create a `CartItem` instance with a `quantity` value of `0`, the `CartItem` initializer causes initialization to fail:*

`quantity` 값이 `0`인 `CartItem` 인스턴스를 생성하려고 하면 `CartItem` 초기화로 인해 초기화가 실패합니다:

```swift
if let zeroShirts = CartItem(name: "shirt", quantity: 0) {
    print("Item: \(zeroShirts.name), quantity: \(zeroShirts.quantity)")
} else {
    print("Unable to initialize zero shirts")
}
// Prints "Unable to initialize zero shirts"
```

*Similarly, if you try to create a `CartItem` instance with an empty `name` value, the superclass `Product` initializer causes initialization to fail:*

이와 마찬가지로 `name` 값이 비어 있는 `CartItem` 인스턴스를 생성하려고 하면 슈퍼클래스 `Product` 초기화로 인해 초기화가 실패합니다:

```swift
if let oneUnnamed = CartItem(name: "", quantity: 1) {
    print("Item: \(oneUnnamed.name), quantity: \(oneUnnamed.quantity)")
} else {
    print("Unable to initialize one unnamed product")
}
// Prints "Unable to initialize one unnamed product"
```

### *Overriding a Failable Initializer : 실패할 수 있는 이니셜라이저 재정의*

*You can override a superclass failable initializer in a subclass, just like any other initializer. Alternatively, you can override a superclass failable initializer with a subclass nonfailable initializer. This enables you to define a subclass for which initialization can’t fail, even though initialization of the superclass is allowed to fail.*

다른 초기화 프로그램과 마찬가지로 하위 클래스에서 슈퍼 클래스의 실패 가능 이니셜라이저를 재정의할 수 있습니다. 또는 슈퍼 클래스의 실패 가능 이니셜라이저를 하위 클래스의 실패 가능 이니셜라이저로 재정의할 수 있습니다. 이렇게 하면 슈퍼 클래스의 초기화가 실패할 수 있지만 초기화가 실패할 수 없는 하위 클래스를 정의할 수 있습니다.

*Note that if you override a failable superclass initializer with a nonfailable subclass initializer, the only way to delegate up to the superclass initializer is to force-unwrap the result of the failable superclass initializer.*

실패 가능한 슈퍼클래스 이니셜라이저를 사용 불가능한 하위클래스 이니셜라이저로 재정의하는 경우 실패 가능한 슈퍼클래스 이니셜라이저에 위임하는 유일한 방법은 실패 가능한 슈퍼클래스 이니셜라이저의결과를 강제로 벗겨내는 것입니다.

> *NOTE*
> 
> *You can override a failable initializer with a nonfailable initializer but not the other way around.*
> 
> 실패 가능한 이니셜라이저를 사용 불가능한 이니셜라이저로 재정의할 수 있지만 그 반대는 아닙니다.

*The example below defines a class called `Document`. This class models a document that can be initialized with a `name` property that’s either a nonempty string value or `nil`, but can’t be an empty string:*

아래 예제에서는 `Document`라는 클래스를 정의합니다. 이 클래스는 빈 문자열 값이나 `nil`인 `name` 프로퍼티로 초기화할 수 있지만 빈 문자열일 수는 없는 문서를 모델링합니다:

```swift
class Document {
    var name: String?
    // this initializer creates a document with a nil name value
    init() {}
    // this initializer creates a document with a nonempty name value
    init?(name: String) {
        if name.isEmpty { return nil }
        self.name = name
    }
}
```

*The next example defines a subclass of `Document` called `AutomaticallyNamedDocument`. The `AutomaticallyNamedDocument` subclass overrides both of the designated initializers introduced by `Document`. These overrides ensure that an `AutomaticallyNamedDocument` instance has an initial `name` value of `"[Untitled]"` if the instance is initialized without a name, or if an empty string is passed to the `init(name:)` initializer:*

다음 예제에서는 `AutomaticallyNamedDocument`라는 문서의 하위 클래스를 정의합니다. `AutomaticallyNamedDocument` 하위 클래스는 `Document`에서 도입한 지정된 이니셜라이저를 모두 재정의합니다. 이러한 재정의는 인스턴스가 이름 없이 초기화되거나 빈 문자열이 `init(name:)` 이니셜라이저에 전달되는 경우 `AutomaticallyNamedDocument` 인스턴스의 초기 `name` 값이 `"[Untitled]"`임을 보장합니다:*

```swift
class AutomaticallyNamedDocument: Document {
    override init() {
        super.init()
        self.name = "[Untitled]"
    }
    override init(name: String) {
        super.init()
        if name.isEmpty {
            self.name = "[Untitled]"
        } else {
            self.name = name
        }
    }
}
```

*The `AutomaticallyNamedDocument` overrides its superclass’s failable `init?(name:)` initializer with a nonfailable `init(name:)` initializer. Because `AutomaticallyNamedDocument` copes with the empty string case in a different way than its superclass, its initializer doesn’t need to fail, and so it provides a nonfailable version of the initializer instead.*

`AutomaticNamedDocument`는 슈퍼클래스의 실패 가능한 `init?(name:)` 이니셜라이저를 실패할  수 없는 `init(name:)` 이니셜라이저로 재정의합니다. `AutomaticallyNamedDocument`는 슈퍼 클래스와 다른 방식으로 빈 문자열 대소문자를 처리하므로 이니셜라이저가 실패할 필요가 없으므로 실패할 수 없는 버전의 이니셜라이저 제공합니다.

*You can use forced unwrapping in an initializer to call a failable initializer from the superclass as part of the implementation of a subclass’s nonfailable initializer. For example, the `UntitledDocument` subclass below is always named `"[Untitled]"`, and it uses the failable `init(name:)` initializer from its superclass during initialization.*

이니셜라이저에서 강제 언래핑을 사용하여 하위 클래스의 실패 불가능한 이니셜라이저 구현의 일부로 슈퍼 클래스에서 실패 가능한 초기화를 호출할 수 있습니다. 예를 들어, 아래의 `UntitledDocument`의 하위 클래스는 항상 `"[Untitled]"`로 명명되며 초기화 중에 슈퍼 클래스의 실패 가능한 `init(name:)` 이니셜라이저를 사용합니다.*

```swift
class UntitledDocument: Document {
    override init() {
        super.init(name: "[Untitled]")!
    }
}
```

*In this case, if the `init(name:)` initializer of the superclass were ever called with an empty string as the name, the forced unwrapping operation would result in a runtime error. However, because it’s called with a string constant, you can see that the initializer won’t fail, so no runtime error can occur in this case.*

이 경우 슈퍼클래스의 `init(name:)` 이니셜라이저가 빈 문자열을 이름으로 사용하여 호출된 경우 강제로 언래핑 작업을 수행하면 런타임 오류가 발생합니다. 그러나 문자열 상수로 호출되기 때문에 초기화가 실패하지 않으므로 이 경우 런타임 오류가 발생할 수 없습니다.

### *The init! Failable Initializer : init! 실패 가능한 이니셜라이저*

*You typically define a failable initializer that creates an optional instance of the appropriate type by placing a question mark after the `init` keyword (`init?`). Alternatively, you can define a failable initializer that creates an implicitly unwrapped optional instance of the appropriate type. Do this by placing an exclamation point after the `init` keyword (`init!`) instead of a question mark.*

일반적으로 `init` 키워드(`init?`) 뒤에 물음표를 붙여 적절한 타입의 옵셔널 인스턴스를 만드는 실패 가능한 이니셜라이저를 정의합니다. 또는 적절한 타입의 암시적으로 언래핑된 선택적 인스턴스를 생성하는 실패 가능한 이니셜라이저를 정의할 수 있습니다. 이 작업은 `init` 키워드 뒤에 물음표 대신 느낌표를 붙여서 수행합니다(`init!`) 

*You can delegate from `init?` to `init!` and vice versa, and you can override `init?` with `init!` and vice versa. You can also delegate from `init` to `init!`, although doing so will trigger an assertion if the `init!` initializer causes initialization to fail.*

init?  에서 init! 으로 위임받을 수 있고, 반대로 init?을 init! 으로 재정의할 수 있으며 반대도 마찬가지입니다.~~init에서 init! 으로 위임될 수도 있지만 init! 이니셜라이저가 초기화를 실패로 이끈다면 assertion이 트리거됩니다.~~


