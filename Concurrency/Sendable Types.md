## *Sendable Types : 전송 가능 타입*

*Tasks and actors let you divide a program into pieces that can safely run concurrently. Inside of a task or an instance of an actor, the part of a program that contains mutable state, like variables and properties, is called a concurrency domain. Some kinds of data can’t be shared between concurrency domains, because that data contains mutable state, but it doesn’t protect against overlapping access.*

작업 및 액터를 통해 프로그램을 안전하게 동시에 실행할 수 있는 부분으로 나눌 수 있습니다. 작업 또는 액터의 인스턴스 내부에서 변수 및 프로퍼티와 같이 가변 상태를 포함하는 프로그램 부분을 동시성 도메인이라고 합니다. 일부 타입의 데이터는 변경 가능한 상태를 포함하지만 중복 액세스로부터 보호되지 않기 때문에 동시성 도메인 간에 공유할 수 없습니다.

*A type that can be shared from one concurrency domain to another is known as a sendable type. For example, it can be passed as an argument when calling an actor method or be returned as the result of a task. The examples earlier in this chapter didn’t discuss sendability because those examples use simple value types that are always safe to share for the data being passed between concurrency domains. In contrast, some types aren’t safe to pass across concurrency domains. For example, a class that contains mutable properties and doesn’t serialize access to those properties can produce unpredictable and incorrect results when you pass instances of that class between different tasks.*

한 동시성 도메인에서 다른 도메인으로 공유할 수 있는 타입을 전송 가능 타입이라고 합니다. 예를 들어, 액터 메서드를 호출할 때 인수로 전달되거나 작업의 결과로 반환될 수 있습니다. 이 장의 앞부분에 있는 예제에서는 동시성 도메인 간에 전달되는 데이터에 대해 항상 안전하게 공유할 수 있는 단순한 값 타입을 사용하기 때문에 전송 가능성에 대해 설명하지 않았습니다. 반대로, 일부 타입은 동시성 도메인을 통과하는 것이 안전하지 않습니다. 예를 들어, 변경 가능한 프로퍼티를 포함하고 이러한 프로퍼티에 대한 액세스를 직렬화하지 않는 클래스는 다른 작업 간에 해당 클래스의 인스턴스를 전달할 때 예측할 수 없고 잘못된 결과를 생성할 수 있습니다.

*You mark a type as being sendable by declaring conformance to the `Sendable` protocol. That protocol doesn’t have any code requirements, but it does have semantic requirements that Swift enforces. In general, there are three ways for a type to be sendable:*

`Sendable` 프로토콜에 대한 적합성을 선언하여 타입을 전송 가능으로 표시합니다. 그 프로토콜에는 코드 요구 사항이 없지만 Swift가 적용하는 의미론적 요구 사항이 있습니다. 일반적으로 타입을 전송할 수 있는 세 가지 방법이 있습니다:

- *The type is a value type, and its mutable state is made up of other sendable data—for example, a structure with stored properties that are sendable or an enumeration with associated values that are sendable.*
  
  타입은 값 타입이며 변경 가능한 상태는 다른 전송 가능한 데이터(예: 전송 가능한 저장 프로퍼티가 있는 구조체 또는 전송 가능한 값이 연결된 열거형)로 구성됩니다.

- *The type doesn’t have any mutable state, and its immutable state is made up of other sendable data—for example, a structure or class that has only read-only properties.*
  
  타입에는 변경 가능한 상태가 없으며 변경 불가능한 상태는 다른 전송 가능한 데이터(예: 읽기 전용 프로퍼티만 있는 구조체 또는 클래스)로 구성됩니다.

- *The type has code that ensures the safety of its mutable state, like a class that’s marked `@MainActor` or a class that serializes access to its properties on a particular thread or queue.*
  
  `@MainActor`로 표시된 클래스나 특정 스레드 또는 대기열에서 프로퍼티에 대한 액세스를 직렬화하는 클래스와 같이 이 타입은 가변 상태의 안전을 보장하는 코드를 가지고 있습니다.

*For a detailed list of the semantic requirements, see the [`Sendable`](https://developer.apple.com/documentation/swift/sendable) protocol reference.*

의미론적 요구사항에 대한 자세한 리스트는 [링크]를 참조하세요.

*Some types are always sendable, like structures that have only sendable properties and enumerations that have only sendable associated values. For example:*

보낼 수 있는 프로퍼티만 있는 구조체와 보낼 수 있는 관련 값만 있는 열거형과 같은 일부 타입은 항상 보낼 수 있습니다. 예를 들어 다음과 같습니다:

```swift
struct TemperatureReading: Sendable {
    var measurement: Int
}

extension TemperatureLogger {
    func addReading(from reading: TemperatureReading) {
        measurements.append(reading.measurement)
    }
}

let logger = TemperatureLogger(label: "Tea kettle", measurement: 85)
let reading = TemperatureReading(measurement: 45)
await logger.addReading(from: reading)
```

*Because `TemperatureReading` is a structure that has only sendable properties, and the structure isn’t marked `public` or `@usableFromInline`, it’s implicitly sendable. Here’s a version of the structure where conformance to the `Sendable` protocol is implied:*

`TemperatureReading`은 전송 가능한 프로퍼티만 있는 구조체이고, `public`이나 `@useableFromInline`으로 표시되지 않기 때문에 암묵적으로 전송 가능합니다. 다음은 `Sendable` 프로토콜의 준수를 암시하는 구조체의 버전입니다:

```swift
struct TemperatureReading {
    var measurement: Int
}
```
