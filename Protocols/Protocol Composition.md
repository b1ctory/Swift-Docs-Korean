## *Protocol Composition : 프로토콜 구성*

*It can be useful to require a type to conform to multiple protocols at the same time. You can combine multiple protocols into a single requirement with a protocol composition. Protocol compositions behave as if you defined a temporary local protocol that has the combined requirements of all protocols in the composition. Protocol compositions don’t define any new protocol types.*

한 타입이 동시에 여러 프로토콜을 준수하도록 요구하는 것이 유용할 수 있습니다. 프로토콜 구성을 사용하여 여러 프로토콜을 단일 요구사항으로 결합할 수 있습니다. 프로토콜 구성은 구성에 있는 모든 프로토콜의 결합된 요구사항을 가진 임시 로컬 프로토콜을 정의한 것처럼 작동합니다. 프로토콜 구성은 새 프로토콜 타입을 정의하지 않습니다.

*Protocol compositions have the form `SomeProtocol & AnotherProtocol`. You can list as many protocols as you need, separating them with ampersands (`&`). In addition to its list of protocols, a protocol composition can also contain one class type, which you can use to specify a required superclass.*

프로토콜 구성은 `Some Protocol & Another Protocol` 형식입니다. 앰퍼샌드(`&`)로 구분하여 필요한 만큼의 프로토콜을 나열할 수 있습니다. 프로토콜 목록 외에도 프로토콜 구성에는 필요한 슈퍼클래스를 지정하는 데 사용할 수 있는 클래스 타입이 하나 포함될 수 있습니다.

*Here’s an example that combines two protocols called `Named` and `Aged` into a single protocol composition requirement on a function parameter:*

다음은 함수 매개 변수에 대한 단일 프로토콜 구성 요구 사항으로 `Named`와  `Aged`라는 두 프로토콜을 결합하는 예입니다:

```swift
protocol Named {
    var name: String { get }
}
protocol Aged {
    var age: Int { get }
}
struct Person: Named, Aged {
    var name: String
    var age: Int
}
func wishHappyBirthday(to celebrator: Named & Aged) {
    print("Happy birthday, \(celebrator.name), you're \(celebrator.age)!")
}
let birthdayPerson = Person(name: "Malcolm", age: 21)
wishHappyBirthday(to: birthdayPerson)
// Prints "Happy birthday, Malcolm, you're 21!"
```

*In this example, the `Named` protocol has a single requirement for a gettable `String` property called `name`. The `Aged` protocol has a single requirement for a gettable `Int` property called `age`. Both protocols are adopted by a structure called `Person`.*

이 예에서 `Named` 프로토콜에는 `name`이라는 gettable `String` 프로퍼티에 대한 단일 요구 사항이 있습니다. `Aged` 프로토콜에는 `age`라는 gettable `Int` 프로퍼티에 대한 단일 요구 사항이 있습니다. 두 프로토콜 모두 `Person`이라는 구조로 채택됩니다.

*The example also defines a `wishHappyBirthday(to:)` function. The type of the `celebrator` parameter is `Named & Aged`, which means “any type that conforms to both the `Named` and `Aged` protocols.” It doesn’t matter which specific type is passed to the function, as long as it conforms to both of the required protocols.*

이 예에서는 `wishHappyBirthday(to:)` 함수도 정의합니다. `celebrator` 매개 변수의 타입은 `Named & aged`로 "`Named` 프로토콜과 `Aged` 프로토콜을 모두 준수하는 모든 타입"을 의미합니다 함수에 전달되는 특정 타입은 필요한 프로토콜을 모두 준수하는 한 중요하지 않습니다.

*The example then creates a new `Person` instance called `birthdayPerson` and passes this new instance to the `wishHappyBirthday(to:)` function. Because `Person` conforms to both protocols, this call is valid, and the `wishHappyBirthday(to:)` function can print its birthday greeting.*

이 예에서는 `birthdayPerson`이라는 새 `Person` 인스턴스를 만들고 이 새 인스턴스를 `wishHappyBirthday(to:)` 함수에 전달합니다. `Person`은 두 프로토콜을 모두 준수하므로 이 호출은 유효하며 `wishHappyBirthday(to:)` 함수는 생일 인사말을 출력할 수 있습니다.

*Here’s an example that combines the `Named` protocol from the previous example with a `Location` class:*

다음은 이전 예의 `Named` 프로토콜을 `Location` 클래스와 결합한 예입니다.

```swift
class Location {
    var latitude: Double
    var longitude: Double
    init(latitude: Double, longitude: Double) {
        self.latitude = latitude
        self.longitude = longitude
    }
}
class City: Location, Named {
    var name: String
    init(name: String, latitude: Double, longitude: Double) {
        self.name = name
        super.init(latitude: latitude, longitude: longitude)
    }
}
func beginConcert(in location: Location & Named) {
    print("Hello, \(location.name)!")
}

let seattle = City(name: "Seattle", latitude: 47.6, longitude: -122.3)
beginConcert(in: seattle)
// Prints "Hello, Seattle!"
```

*The `beginConcert(in:)` function takes a parameter of type `Location & Named`, which means “any type that’s a subclass of `Location` and that conforms to the `Named` protocol.” In this case, `City` satisfies both requirements.*

`beginConcert(in:)` 함수는 `Location & Named` 타입의 매개변수를 사용합니다. 이는 "`Location`의 하위 클래스이고 `Named` 프로토콜을 준수하는 모든 타입"을 의미합니다. 이 경우 `City`는 두 가지 요구사항을 모두 충족합니다.

*Passing `birthdayPerson` to the `beginConcert(in:)` function is invalid because `Person` isn’t a subclass of `Location`. Likewise, if you made a subclass of `Location` that didn’t conform to the `Named` protocol, calling `beginConcert(in:)` with an instance of that type is also invalid.*

`Person`은 `Location`의 하위 클래스가 아니기 때문에 `birthdayPerson`을 `beginConcert(in:)` 함수에 전달하는 것은 유효하지 않습니다. 마찬가지로 `Named` 프로토콜을 준수하지 않는 `Location`의 하위 클래스를 만든 경우 해당 타입의 인스턴스로 `beginConcert(in:)`를 호출하는 것도 유효하지 않습니다.


