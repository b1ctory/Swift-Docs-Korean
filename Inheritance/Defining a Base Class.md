## *Defining a Base Class : 기본 클래스 정의*

*Any class that doesn’t inherit from another class is known as a base class.*

다른 클래스에서 상속되지 않는 클래스를 기본 클래스라고 합니다.

> *NOTE*
> 
> *Swift classes don’t inherit from a universal base class. Classes you define without specifying a superclass automatically become base classes for you to build upon.*
> 
> Swift 클래스는 범용 기본 클래스에서 상속되지 않습니다. 슈퍼 클래스를 지정하지 않고 정의한 클래스는 자동으로 작성할 기본 클래스가 됩니다.

*The example below defines a base class called `Vehicle`. This base class defines a stored property called `currentSpeed`, with a default value of `0.0` (inferring a property type of `Double`). The `currentSpeed` property’s value is used by a read-only computed `String` property called `description` to create a description of the vehicle.*

아래 예제에서는 `Vehicle`라는 기본 클래스를 정의합니다. 이 기본 클래스는 `currentSpeed`라는 저장 프로퍼티를 정의하며 기본값은 `0.0`(프로퍼티 타입은 `Double`을 의미)입니다. `currentSpeed` 프로퍼티의 값은 `description`이라는 읽기 전용 연산 `String` 프로퍼티에서 차량에 대한 설명을 만드는 데 사용됩니다.

*The `Vehicle` base class also defines a method called `makeNoise`. This method doesn’t actually do anything for a base `Vehicle` instance, but will be customized by subclasses of `Vehicle` later on:*

`Vehicle` 기본 클래스는 `makeNoise`라는 메서드도 정의합니다. 이 메서드는 기본 `Vehicle` 인스턴스에 대해 실제로 수행되지 않지만 나중에 `Vehicle`의 하위 클래스에 의해 사용자 지정됩니다:

```swift
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    func makeNoise() {
        // do nothing - an arbitrary vehicle doesn't necessarily make a noise
    }
}
```

*You create a new instance of `Vehicle` with initializer syntax, which is written as a type name followed by empty parentheses:*

이니셜라이저 구문을 사용하여 `Vehicle`의 새 인스턴스를 생성합니다. 이 인스턴스는 타입 이름 다음에 빈 괄호로 작성됩니다:

```swift
let someVehicle = Vehicle()
```

*Having created a new `Vehicle` instance, you can access its `description` property to print a human-readable description of the vehicle’s current speed:*

새 `Vehicle` 인스턴스를 만든 후에는 해당 `description` 프로퍼티에 액세스하여 차량의 현재 속도에 대한 사람이 읽을 수 있는 설명을 출력할 수 있습니다:

```swift
print("Vehicle: \(someVehicle.description)")
// Vehicle: traveling at 0.0 miles per hour
```

*The `Vehicle` class defines common characteristics for an arbitrary vehicle, but isn’t much use in itself. To make it more useful, you need to refine it to describe more specific kinds of vehicles.*

`Vehicle` 클래스는 임의의 차량에 대한 공통 특성을 정의하지만 그 자체로는 그다지 유용하지 않습니다. 보다 유용하게 사용하려면 보다 구체적인 타입의 차량을 설명하도록 세부화해야 합니다.
