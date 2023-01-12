## *Subclassing : 서브클래싱*

*Subclassing is the act of basing a new class on an existing class. The subclass inherits characteristics from the existing class, which you can then refine. You can also add new characteristics to the subclass.*

서브클래싱은 기존 클래스를 기반으로 새로운 클래스를 분류하는 행위입니다. 하위 클래스는 기존 클래스에서 프로퍼티를 상속하므로 세분화할 수 있습니다. 하위 클래스에 새 특성을 추가할 수도 있습니다.

*To indicate that a subclass has a superclass, write the subclass name before the superclass name, separated by a colon:*

하위 클래스에 슈퍼 클래스가 있음을 나타내려면 해당 하위 클래스 이름 앞에 콜론으로 구분하여 다음과 같이 입력합니다:

```swift
class SomeSubclass: SomeSuperclass {
    // subclass definition goes here
}
```

*The following example defines a subclass called `Bicycle`, with a superclass of `Vehicle`:*

다음 예제에서는 슈퍼 클래스가 `Vehicle`인 `Bicycle`이라는 하위 클래스를 정의합니다:

```swift
class Bicycle: Vehicle {
    var hasBasket = false
}
```

*The new `Bicycle` class automatically gains all of the characteristics of `Vehicle`, such as its `currentSpeed` and `description` properties and its `makeNoise()` method.*

새 `Bicycle` 클래스는 `currentSpeed` 및 `description` 프로퍼티와 `makeNoise()`메서드 등 차량의 모든 특성을 자동으로 가져옵니다.

*In addition to the characteristics it inherits, the `Bicycle` class defines a new stored property, `hasBasket`, with a default value of `false` (inferring a type of `Bool` for the property).*

상속되는 특성 외에도 `Bicycle` 클래스는 새 저장 프로퍼티 `hasBasket`을 기본값 `false`(프로퍼티의 `Bool` 타입을 유추)로 정의합니다.

*By default, any new `Bicycle` instance you create will not have a basket. You can set the `hasBasket` property to `true` for a particular `Bicycle` instance after that instance is created:*

기본적으로 생성하는 새 `Bicycle` 인스턴스에는 바스켓이 없습니다. 특정 `Bicycle` 인스턴스가 생성된 후 해당 인스턴스에 대해 `hasBasket` 프로퍼티를 `true`로 설정할 수 있습니다:

```swift
let bicycle = Bicycle()
bicycle.hasBasket = true
```

*You can also modify the inherited `currentSpeed` property of a `Bicycle` instance, and query the instance’s inherited `description` property:*

또한 `Bicycle` 인스턴스의 상속된 `currentSpeed` 프로퍼티를 수정하고 인스턴스의 상속된 `description` 프로퍼티를 쿼리할 수 있습니다:

```swift
bicycle.currentSpeed = 15.0
print("Bicycle: \(bicycle.description)")
// Bicycle: traveling at 15.0 miles per hour
```

*Subclasses can themselves be subclassed. The next example creates a subclass of `Bicycle` for a two-seater bicycle known as a “tandem”:*

하위 클래스 자체는 하위 클래스로 분류될 수 있습니다. 다음 예에서는 "tandem"으로 알려진 2인승 자전거에 대해 `Bicycle`의 하위 클래스를 만듭니다:

```swift
class Tandem: Bicycle {
    var currentNumberOfPassengers = 0
}
```

*`Tandem` inherits all of the properties and methods from `Bicycle`, which in turn inherits all of the properties and methods from `Vehicle`. The `Tandem` subclass also adds a new stored property called `currentNumberOfPassengers`, with a default value of `0`.*

`Tandem`은 `Bicycle`의 모든 프로퍼티와 메서드를 상속하고, `Vehicle`의 모든 프로퍼티와 메서드를 상속합니다. `Tandem` 하위 클래스는 또한 기본값이 `0`인 `currentNumberOfPasseners`라는 새 저장 프로퍼티를 추가합니다.

*If you create an instance of `Tandem`, you can work with any of its new and inherited properties, and query the read-only `description` property it inherits from `Vehicle`:*

`Tandem`의 인스턴스를 생성하면 해당 인스턴스의 새 프로퍼티와 상속된 프로퍼티 중 하나를 사용하여 작업할 수 있으며 `Vehicle`에서 상속되는 읽기 전용 `description` 프로퍼티를 쿼리할 수 있습니다:

```swift
let tandem = Tandem()
tandem.hasBasket = true
tandem.currentNumberOfPassengers = 2
tandem.currentSpeed = 22.0
print("Tandem: \(tandem.description)")
// Tandem: traveling at 22.0 miles per hour
```
