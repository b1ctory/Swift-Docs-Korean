## *Method Requirements : 메서드 요구사항*

*Protocols can require specific instance methods and type methods to be implemented by conforming types. These methods are written as part of the protocol’s definition in exactly the same way as for normal instance and type methods, but without curly braces or a method body. Variadic parameters are allowed, subject to the same rules as for normal methods. Default values, however, can’t be specified for method parameters within a protocol’s definition.*

프로토콜은 타입을 준수하여 특정 인스턴스 메서드 및 타입 메서드를 구현하도록 요구할 수 있습니다. 이러한 메소드는 일반 인스턴스 및 타입 메서드와 정확히 동일한 방식으로 프로토콜 정의의 일부로 작성되지만 중괄호나 메서드의 본문이 없습니다. 일반 메서드와 동일한 규칙에 따라 가변 매개변수가 허용됩니다. 그러나 프로토콜 정의 내에서 메서드 매개변수에 대해 기본값을 지정할 수 없습니다.

*As with type property requirements, you always prefix type method requirements with the `static` keyword when they’re defined in a protocol. This is true even though type method requirements are prefixed with the `class` or `static` keyword when implemented by a class:*

타입 프로퍼티 요구 사항과 마찬가지로 프로토콜에서 정의될 때 타입 메서드 요구 사항에 항상 `static` 키워드 접두사를 붙입니다. 이는 클래스에 의해 구현될 때 타입 메서드 요구사항에 `class` 또는 `static` 키워드가 접두사로 붙는 경우에도 마찬가지입니다.

```swift
protocol SomeProtocol {
    static func someTypeMethod()
}
```

*The following example defines a protocol with a single instance method requirement:*

다음 예제는 단일 인스턴스 메서드 요구 사항이 있는 프로토콜을 정의합니다.

```swift
protocol RandomNumberGenerator {
    func random() -> Double
}
```

*This protocol, `RandomNumberGenerator`, requires any conforming type to have an instance method called `random`, which returns a `Double` value whenever it’s called. Although it’s not specified as part of the protocol, it’s assumed that this value will be a number from `0.0` up to (but not including) `1.0`.*

이 프로토콜인 `RandomNumberGenerator`는 호출될 때마다 `Double` 값을 반환하는 인스턴스 메서드인 `random`을 갖는 준수 타입을 요구합니다. 프로토콜의 일부로 지정되지는 않았지만 이 값은 `0.0`에서 `1.0`(포함되지 않음)까지의 숫자라고 가정합니다.

*The `RandomNumberGenerator` protocol doesn’t make any assumptions about how each random number will be generated—it simply requires the generator to provide a standard way to generate a new random number.*

`RandomNumberGenerator` 프로토콜은 각 난수가 생성되는 방식에 대해 어떠한 가정도 하지 않습니다. 생성기가 새로운 난수를 생성하는 표준 방법을 제공하기만 하면 됩니다.

*Here’s an implementation of a class that adopts and conforms to the `RandomNumberGenerator` protocol. This class implements a pseudorandom number generator algorithm known as a linear congruential generator:*

다음은 `RandomNumberGenerator` 프로토콜을 채택하고 준수하는 클래스 구현입니다. 이 클래스는 선형 합동 생성기로 알려진 의사난수 생성기 알고리즘을 구현합니다.

```swift
class LinearCongruentialGenerator: RandomNumberGenerator {
    var lastRandom = 42.0
    let m = 139968.0
    let a = 3877.0
    let c = 29573.0
    func random() -> Double {
        lastRandom = ((lastRandom * a + c)
            .truncatingRemainder(dividingBy:m))
        return lastRandom / m
    }
}
let generator = LinearCongruentialGenerator()
print("Here's a random number: \(generator.random())")
// Prints "Here's a random number: 0.3746499199817101"
print("And another one: \(generator.random())")
// Prints "And another one: 0.729023776863283"
```
