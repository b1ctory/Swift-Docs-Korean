## *Checking for Protocol Conformance : 프로토콜 적합성 체크*

*You can use the `is` and `as` operators described in [Type Casting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html) to check for protocol conformance, and to cast to a specific protocol. Checking for and casting to a protocol follows exactly the same syntax as checking for and casting to a type:*

[링크]에 설명된 `is` 및 `as` 연산자를 사용하여 프로토콜 적합성을 확인하고 특정 프로토콜로 캐스팅할 수 있습니다. 프로토콜 확인 및 캐스팅은 타입 확인 및 캐스팅과 정확히 동일한 구문을 따릅니다:

- *The `is` operator returns `true` if an instance conforms to a protocol and returns `false` if it doesn’t.*
  
  `is` 연산자는 인스턴스가 프로토콜을 준수하면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.

- *The `as?` version of the downcast operator returns an optional value of the protocol’s type, and this value is `nil` if the instance doesn’t conform to that protocol.*
  
  `as?` 다운캐스트 연산자 버전은 프로토콜 유형의 옵셔널 값을 반환하며, 인스턴스가 해당 프로토콜을 준수하지 않을 경우 이 값은 `timeout`입니다.

- *The `as!` version of the downcast operator forces the downcast to the protocol type and triggers a runtime error if the downcast doesn’t succeed.*
  
  `as!` 다운캐스트 연산자 버전은 다운캐스트를 프로토콜 타입으로 강제 적용하고 다운캐스트가 성공하지 못할 경우 런타임 오류를 트리거합니다.

*This example defines a protocol called `HasArea`, with a single property requirement of a gettable `Double` property called `area`:*

이 예는 `HasArea`라는 프로토콜을 정의하며, `area`라는 gettable `Double` 타입의 단일 프로퍼티 요구사항을 가지고 있습니다:

```swift
protocol HasArea {
    var area: Double { get }
}
```

*Here are two classes, `Circle` and `Country`, both of which conform to the `HasArea` protocol:*

다음은 `Circle`과 `Country`라는 두 가지 클래스로, 둘 다 `HasArea` 프로토콜을 준수합니다:

```swift
class Circle: HasArea {
    let pi = 3.1415927
    var radius: Double
    var area: Double { return pi * radius * radius }
    init(radius: Double) { self.radius = radius }
}
class Country: HasArea {
    var area: Double
    init(area: Double) { self.area = area }
}
```

*The `Circle` class implements the `area` property requirement as a computed property, based on a stored `radius` property. The `Country` class implements the `area` requirement directly as a stored property. Both classes correctly conform to the `HasArea` protocol.*

`Circle` 클래스는 저장 프로퍼티 `radius`를 기반으로 연산 프로퍼티로 `area` 프로퍼티 요구 사항을 구현합니다. `Country` 클래스는 `area` 요구사항을 직접 저장프로퍼티로 구현합니다. 두 클래스 모두 `HasArea` 프로토콜을 올바르게 준수합니다.

*Here’s a class called `Animal`, which doesn’t conform to the `HasArea` protocol:*

다음은 `HasArea` 프로토콜에 맞지 않는 `Animal`이라는 클래스입니다:

```swift
class Animal {
    var legs: Int
    init(legs: Int) { self.legs = legs }
}
```

*The `Circle`, `Country` and `Animal` classes don’t have a shared base class. Nonetheless, they’re all classes, and so instances of all three types can be used to initialize an array that stores values of type `AnyObject`:*

 `Circle`, `Country` 그리고 `Animal`클래스는 기본 클래스를 공유하지 않습니다. 그럼에도 불구하고 이들은 모두 클래스이므로 세 가지 타입의 인스턴스를 사용하여 `AnyObject` 타입의 값을 저장하는 배열을 초기화할 수 있습니다:

```swift
let objects: [AnyObject] = [
    Circle(radius: 2.0),
    Country(area: 243_610),
    Animal(legs: 4)
]
```

*The `objects` array is initialized with an array literal containing a `Circle` instance with a radius of 2 units; a `Country` instance initialized with the surface area of the United Kingdom in square kilometers; and an `Animal` instance with four legs.*

`objects` 배열은 반지름이 2단위인 `Circle` 인스턴스, 영국 표면적으로 평방 킬로미터로 초기화된 `Country` 인스턴스, 다리가 4개인 `Animal` 인스턴스를 포함하는 배열 리터럴로 초기화됩니다.

*The `objects` array can now be iterated, and each object in the array can be checked to see if it conforms to the `HasArea` protocol:*

이제 `objects` 배열을 반복할 수 있으며 배열의 각 개체가 `HasArea` 프로토콜을 준수하는지 확인할 수 있습니다:

```swift
for object in objects {
    if let objectWithArea = object as? HasArea {
        print("Area is \(objectWithArea.area)")
    } else {
        print("Something that doesn't have an area")
    }
}
// Area is 12.5663708
// Area is 243610.0
// Something that doesn't have an area
```

*Whenever an object in the array conforms to the `HasArea` protocol, the optional value returned by the `as?` operator is unwrapped with optional binding into a constant called `objectWithArea`. The `objectWithArea` constant is known to be of type `HasArea`, and so its `area` property can be accessed and printed in a type-safe way.*

배열의 개체가 `HasArea` 프로토콜을 준수할 때마다 `as?` 연산자에 의해 반환되는 옵셔널 값은  `objectWithArea`라는 상수에  옵셔널 바인딩으로 언래핑됩니다. `objectWithArea`상수는 `HasArea` 타입으로 알려져 있으며, 따라서 해당 `Area` 프로퍼티는 타입세이프한 방식으로 액세스하고 출력할 수 있습니다.

*Note that the underlying objects aren’t changed by the casting process. They continue to be a `Circle`, a `Country` and an `Animal`. However, at the point that they’re stored in the `objectWithArea` constant, they’re only known to be of type `HasArea`, and so only their `area` property can be accessed.*

기본 객체는 캐스팅 프로세스에 의해 변경되지 않습니다. 그들은 계속해서  `Circle`,  `Country` 그리고 `Animal`.입니다. 그러나 `objectWithArea` 상수에 저장되는 시점에서는 `HasArea` 타입으로만 알려져 있으므로 `area` 프로퍼티에만 액세스할 수 있습니다.


