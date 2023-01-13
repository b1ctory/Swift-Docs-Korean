## *Overriding : 재정의*

*A subclass can provide its own custom implementation of an instance method, type method, instance property, type property, or subscript that it would otherwise inherit from a superclass. This is known as overriding.*

하위 클래스는 슈퍼 클래스에서 상속하는 인스턴스 메서드, 타입 메서드, 인스턴스 프로퍼티, 타입 프로퍼티 또는 서브스크립트의 사용자 지정 구현을 제공할 수 있습니다. 이를 재정의라고 합니다.

*To override a characteristic that would otherwise be inherited, you prefix your overriding definition with the `override` keyword. Doing so clarifies that you intend to provide an override and haven’t provided a matching definition by mistake. Overriding by accident can cause unexpected behavior, and any overrides without the `override` keyword are diagnosed as an error when your code is compiled.*

다른 방식으로 상속될 특성을 재정의하려면 재정의하는 정의에 `override` 키워드를 접두사로 붙이면 됩니다. 이렇게 하면 재정의를 제공할 의도가 있으며 실수로 일치하는 정의를 제공하지 않았음을 알 수 있습니다. 실수로 재정의하면 예기치 않은 동작이 발생할 수 있으며, `override` 키워드가 없는 재정의는 코드가 컴파일될 때 에러로 진단됩니다.

*The `override` keyword also prompts the Swift compiler to check that your overriding class’s superclass (or one of its parents) has a declaration that matches the one you provided for the override. This check ensures that your overriding definition is correct.*

또한 `override` 키워드를 사용하면 Swift 컴파일러가 재정의하는 클래스의 슈퍼 클래스(또는 상위 클래스 중 하나)에 재정의에 대해 제공한 것과 일치하는 선언이 있는지 확인할 수 있습니다. 이 검사는 재정의하는 정의가 올바른지 확인합니다.

### *Accessing Superclass Methods, Properties, and Subscripts : 슈퍼클래스 메서드, 프로퍼티 및 서브스크립트에 접근*

*When you provide a method, property, or subscript override for a subclass, it’s sometimes useful to use the existing superclass implementation as part of your override. For example, you can refine the behavior of that existing implementation, or store a modified value in an existing inherited variable.*

하위 클래스에 메서드, 프로퍼티 또는 서브스크립트 재정의를 제공할 때 재정의의 일부로 기존 슈퍼클래스 구현을 사용하는 것이 유용할 수 있습니다. 예를 들어 기존 구현의 동작을 세분화하거나 수정된 값을 기존 상속된 변수에 저장할 수 있습니다.

*Where this is appropriate, you access the superclass version of a method, property, or subscript by using the `super` prefix:*

적절한 경우 `super` 접두사를 사용하여 메서드, 프로퍼티 또는 서브스크립트의 슈퍼클래스 버전에 액세스합니다:

- *An overridden method named `someMethod()` can call the superclass version of `someMethod()` by calling `super.someMethod()` within the overriding method implementation.*
  
  재정의된 메서드 `someMethod()`는 재정의된 메서드 구현 내에서`super.someMethod()` 를 호출함으로써 `someMethod()`의 슈퍼클래스 버전을 호출할 수 있습니다.

- *An overridden property called `someProperty` can access the superclass version of `someProperty` as `super.someProperty` within the overriding getter or setter implementation.*
  
  `someProperty`라는 재정의된 프로퍼티는 재정의된 게터 또는 세터 구현 내에서 `someProperty`의 슈퍼클래스 버전에 `super`로 액세스할 수 있습니다.

- *An overridden subscript for `someIndex` can access the superclass version of the same subscript as `super[someIndex]` from within the overriding subscript implementation.*
  
  `someIndex`에 대해 재정의된 서브스크립트는 재정의 서브스크립트 구현 내에서 `super[someIndex]`와 동일한 서브스크립트의 슈퍼클래스 버전에 액세스할 수 있습니다.

### *Overriding Methods : 재정의 메서드*

*You can override an inherited instance or type method to provide a tailored or alternative implementation of the method within your subclass.*

상속된 인스턴스 또는 타입 메서드를 재정의하여 하위 클래스 내에서 메서드의 맞춤형 또는 대체 구현을 제공할 수 있습니다.

*The following example defines a new subclass of `Vehicle` called `Train`, which overrides the `makeNoise()` method that `Train` inherits from `Vehicle`:*

다음 예제에서는 `Train`이 `Vehicle`에서 상속하는 `makeNoise()`메서드를 재정의하는 `Vehicle`의 새로운 하위 클래스인 `Train`을 정의합니다:

```swift
class Train: Vehicle {
    override func makeNoise() {
        print("Choo Choo")
    }
}
```

*If you create a new instance of `Train` and call its `makeNoise()` method, you can see that the `Train` subclass version of the method is called:*

`Train`의 새 인스턴스를 만들고 해당 인스턴스의 `makeNoise()` 메서드를 호출하면 해당 메서드의 `Train` 하위 클래스 버전이 다음과 같이 호출됨을 알 수 있습니다:

```swift
let train = Train()
train.makeNoise()
// Prints "Choo Choo"
```

### *Overriding Properties : 프로퍼티 재정의*

*You can override an inherited instance or type property to provide your own custom getter and setter for that property, or to add property observers to enable the overriding property to observe when the underlying property value changes.*

상속된 인스턴스 또는 타입 프로퍼티를 재정의하여 해당 프로퍼티에 대한 고유한 사용자 지정 게터 및 세터를 제공하거나 재정의 프로퍼티의 기본 프로퍼티 값이 변경될 때 관찰할 수 있도록 프로퍼티 옵저버를 추가할 수 있습니다

#### *Overriding Property Getters and Setters : 프로퍼티 정의 게터 및 세터*

*You can provide a custom getter (and setter, if appropriate) to override any inherited property, regardless of whether the inherited property is implemented as a stored or computed property at source. The stored or computed nature of an inherited property isn’t known by a subclass—it only knows that the inherited property has a certain name and type. You must always state both the name and the type of the property you are overriding, to enable the compiler to check that your override matches a superclass property with the same name and type.*

상속된 프로퍼티가 원본에서 저장 프로퍼티로 구현되는지 연산 프로퍼티로 구현되는지 여부에 관계없이 상속된 프로퍼티를 재정의하는 사용자 지정 게터(및 해당하는 경우 세터)를 제공할 수 있습니다. 상속된 프로퍼티의 저장 또는 연산 프로퍼티는 하위 클래스에서 알 수 없으며 상속된 프로퍼티에 특정 이름과 타입이 있다는 것만 알고 있습니다. 컴파일러가 재정의가 동일한 이름과 타입의 슈퍼클래스 프로퍼티와 일치하는지 확인하려면 재정의할 프로퍼티의 이름과 타입을 항상 명시해야 합니다.

*You can present an inherited read-only property as a read-write property by providing both a getter and a setter in your subclass property override. You can’t, however, present an inherited read-write property as a read-only property.*

하위 클래스 프로퍼티 재정의에 게터와 세터를 모두 제공하여 상속된 읽기 전용 속성을 읽기-쓰기 프로퍼티로 표시할 수 있습니다. 그러나 상속된 읽기-쓰기 프로퍼티를 읽기 전용 프로퍼티로 표시할 수는 없습니다.

> *NOTE*
> 
> *If you provide a setter as part of a property override, you must also provide a getter for that override. If you don’t want to modify the inherited property’s value within the overriding getter, you can simply pass through the inherited value by returning `super.someProperty` from the getter, where `someProperty` is the name of the property you are overriding.*
> 
> 프로퍼티 재정의의 일부로 세터를 제공하는 경우 해당 재정의에 대한 게터도 제공해야 합니다. 상속된 프로퍼티의 값을 재정의하는 게터 내에서 수정하지 않으려면 게터에서 `super.someProperty`를 반환하여 상속된 값을 전달할 수 있습니다. 여기서 `someProperty`는 재정의하는 프로퍼티의 이름입니다.

*The following example defines a new class called `Car`, which is a subclass of `Vehicle`. The `Car` class introduces a new stored property called `gear`, with a default integer value of `1`. The `Car` class also overrides the `description` property it inherits from `Vehicle`, to provide a custom description that includes the current gear:*

다음 예제에서는 `Vehicle`의 하위 클래스인 `Car`라는 새 클래스를 정의합니다. `Car` 클래스는 기본 정수 값이 `1`인 `gear`라는 새로운 저장 프로퍼티를 도입합니다. 또한 `Car` 클래스는 `Vehicle`에서 상속하는 `description` 프로퍼티를 재정의하여 현재 기어를 포함하는 사용자 지정 설명을 제공합니다:

```swift
class Car: Vehicle {
    var gear = 1
    override var description: String {
        return super.description + " in gear \(gear)"
    }
}
```

*The override of the `description` property starts by calling `super.description`, which returns the `Vehicle` class’s `description` property. The `Car` class’s version of `description` then adds some extra text onto the end of this description to provide information about the current gear.*

`description` 속성의 재정의는 `Vehicle` 클래스의 `description` 프로퍼티를 반환하는 `super.description`을 호출하는 것으로 시작합니다. 그런 다음 `Car` 클래스의 `description` 버전은 이 설명의 끝에 텍스트를 추가하여 현재 기어에 대한 정보를 제공합니다.

*If you create an instance of the `Car` class and set its `gear` and `currentSpeed` properties, you can see that its `description` property returns the tailored description defined within the `Car` class:*

`Car` 클래스의 인스턴스를 만들고 해당 `gear` 및 `currentSpeed` 프로퍼티를 설정하면 해당 `description` 프로퍼티가 `Car` 클래스 내에서 정의된 맞춤형 설명을 반환한다는 것을 알 수 있습니다:

```swift
let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("Car: \(car.description)")
// Car: traveling at 25.0 miles per hour in gear 3
```

#### *Overriding Property Observers : 프로퍼티 옵저버 재정의*

*You can use property overriding to add property observers to an inherited property. This enables you to be notified when the value of an inherited property changes, regardless of how that property was originally implemented. For more information on property observers, see [Property Observers](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID262).*

프로퍼티 재정의를 사용하여 상속된 프로퍼티에 프로퍼티 옵저버를 추가할 수 있습니다. 이렇게 하면 상속된 프로퍼티 값이 변경될 때 해당 프로퍼티가 처음 구현된 방식에 관계없이 알림을 받을 수 있습니다. 속성 관찰자에 대한 자세한 내용은 [링크]를 참조하세요.

> *NOTE*
> 
> *You can’t add property observers to inherited constant stored properties or inherited read-only computed properties. The value of these properties can’t be set, and so it isn’t appropriate to provide a `willSet` or `didSet` implementation as part of an override.*
> 
> 상속된 상수 저장 프로퍼티 또는 상속된 읽기 전용 연산 프로퍼티에는 프로퍼티 옵저버를 추가할 수 없습니다. 이러한 프로퍼티의 값을 설정할 수 없으므로 재정의의 일부로 `willSet` 또는 `didSet` 구현을 제공하는 것은 적절하지 않습니다.
> 
> *Note also that you can’t provide both an overriding setter and an overriding property observer for the same property. If you want to observe changes to a property’s value, and you are already providing a custom setter for that property, you can simply observe any value changes from within the custom setter.*
> 
> 또한 동일한 프로퍼티에 대해 재정의 세터와 재정의 프로퍼티 옵저버를 모두 제공할 수 없습니다. 프로퍼티 값의 변경을 관찰하려는 경우 이미 해당 프로퍼티에 대한 사용자 지정 세터를 제공하고 있는 경우 사용자 지정 세터 내에서 모든 값 변경을 관찰할 수 있습니다.

*The following example defines a new class called `AutomaticCar`, which is a subclass of `Car`. The `AutomaticCar` class represents a car with an automatic gearbox, which automatically selects an appropriate gear to use based on the current speed:*

다음 예에서는 `AutomaticCar`라는 새로운 클래스를 정의합니다. `AutomaticCar` 클래스는 현재 속도에 따라 사용할 적절한 기어를 자동으로 선택하는 자동 변속 장치가 장착된 자동차를 나타냅니다:

```swift
class AutomaticCar: Car {
    override var currentSpeed: Double {
        didSet {
            gear = Int(currentSpeed / 10.0) + 1
        }
    }
}
```

*Whenever you set the `currentSpeed` property of an `AutomaticCar` instance, the property’s `didSet` observer sets the instance’s `gear` property to an appropriate choice of gear for the new speed. Specifically, the property observer chooses a gear that’s the new `currentSpeed` value divided by `10`, rounded down to the nearest integer, plus `1`. A speed of `35.0` produces a gear of `4`:*

`AutomaticCar` 인스턴스의 `currentSpeed` 프로퍼티를 설정할 때마다 프로퍼티의 `didSet` 옵저버는 인스턴스의 기어 프로퍼티를 새로운 속도에 적합한 기어 선택으로 설정합니다. 구체적으로, 속성 관찰자는 새로운 'current Speed' 값을 '10'으로 나누고 가장 가까운 정수에 `1`을 더한 기어를 선택합니다. 속도가 `35.0`이면 기어가 `4`가 됩니다.

```swift
let automatic = AutomaticCar()
automatic.currentSpeed = 35.0
print("AutomaticCar: \(automatic.description)")
// AutomaticCar: traveling at 35.0 miles per hour in gear 4
```
