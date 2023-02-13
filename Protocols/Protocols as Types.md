## *Protocols as Types : 타입으로서의 프로토콜*

*Protocols don’t actually implement any functionality themselves. Nonetheless, you can use protocols as a fully fledged types in your code. Using a protocol as a type is sometimes called an existential type, which comes from the phrase “there exists a type T such that T conforms to the protocol”.*

프로토콜 자체는 실제로 어떤 기능도 구현하지 않습니다. 그럼에도 불구하고 코드에서 프로토콜을 완전한 타입으로 사용할 수 있습니다. 프로토콜을 타입으로 사용하는 것을 실존적 타입이라고도 하는데, 이는 "T가 프로토콜을 준수하도록 T형이 존재한다"는 문구에서 유래합니다.

*You can use a protocol in many places where other types are allowed, including:*

다음을 포함하여 다른 타입 허용되는 많은 곳에서 프로토콜을 사용할 수 있습니다:

- *As a parameter type or return type in a function, method, or initializer*
  
  함수, 메서드 또는 이니셜라이저의 매개 변수 타입 또는 반환 타입으로 사용됩니다.

- *As the type of a constant, variable, or property*
  
  정수, 변수 또는 프로퍼티의 타입입니다.

- *As the type of items in an array, dictionary, or other container*
  
  배열, 딕셔너리 또는 기타 컨테이너의 항목 타입입니다.

> *NOTE*
> 
> *Because protocols are types, begin their names with a capital letter (such as `FullyNamed` and `RandomNumberGenerator`) to match the names of other types in Swift (such as `Int`, `String`, and `Double`).*
> 
> 프로토콜은 타입이므로 이름을 대문자 (`FullyNamed` 및 `RandomNumberGenerator` 같은)로 시작하여 Swift의 다른 타입(예: `Int`, `String` 및 `Double`)과 일치시킵니다.

*Here’s an example of a protocol used as a type:*

다음은 타입으로 사용되는 프로토콜의 예입니다:

```swift
class Dice {
    let sides: Int
    let generator: RandomNumberGenerator
    init(sides: Int, generator: RandomNumberGenerator) {
        self.sides = sides
        self.generator = generator
    }
    func roll() -> Int {
        return Int(generator.random() * Double(sides)) + 1
    }
}
```

*This example defines a new class called `Dice`, which represents an n-sided dice for use in a board game. `Dice` instances have an integer property called `sides`, which represents how many sides they have, and a property called `generator`, which provides a random number generator from which to create dice roll values.*

이 예에서는 보드 게임에서 사용할 n면 주사위를 나타내는 `Dice`라는 새로운 클래스를 정의합니다. `Dice` 인스턴스에는 몇 개의 변을 가지고 있는지를 나타내는 `sides`라는 정수 프로퍼티와 주사위 롤 값을 만드는 난수 생성기를 제공하는 `generator`라는 프로퍼티가 있습니다.

*The `generator` property is of type `RandomNumberGenerator`. Therefore, you can set it to an instance of any type that adopts the `RandomNumberGenerator` protocol. Nothing else is required of the instance you assign to this property, except that the instance must adopt the `RandomNumberGenerator` protocol. Because its type is `RandomNumberGenerator`, code inside the `Dice` class can only interact with `generator` in ways that apply to all generators that conform to this protocol. That means it can’t use any methods or properties that are defined by the underlying type of the generator. However, you can downcast from a protocol type to an underlying type in the same way you can downcast from a superclass to a subclass, as discussed in [Downcasting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html#ID341).*

`generator` 프로퍼티는 `RandomNumberGenerator` 타입입니다. 따라서 난수 생성기 프로토콜을 사용하는 모든 타입의 인스턴스로 설정할 수 있습니다. 이 프로퍼티에 할당하는 인스턴스에는 `RandomNumberGenerator` 프로토콜을 적용해야 한다는 점을 제외하고는 필요한 것이 없습니다. 타입이 `RandomNumberGenerator`이기 때문에 `Dice`클래스 내의 코드는 이 프로토콜을 준수하는 모든 생성자에 적용되는 방식으로만 `generator`와 상호 작용할 수 있습니다. 즉, 생성자의 기본 타입으로 정의된 메서드나 프로퍼티를 사용할 수 없습니다. 그러나 [링크]에서 설명한 것처럼 슈퍼 클래스에서 하위 클래스로 다운캐스트할 수 있는 것과 동일한 방식으로 프로토콜 타입에서 기본 타입으로 다운캐스트할 수 있습니다.

*`Dice` also has an initializer, to set up its initial state. This initializer has a parameter called `generator`, which is also of type `RandomNumberGenerator`. You can pass a value of any conforming type in to this parameter when initializing a new `Dice` instance.*

`Dice`에는 초기 상태를 설정하기 위한 이니셜라이저도 있습니다. 이 이니셜라이저에는 `generator`라는 매개 변수가 있으며, 이 매개 변수도 `RandomNumberGenerator` 타입입니다. 새 `Dice` 인스턴스를 초기화할 때 적합한 타입의 값을 이 매개 변수에 전달할 수 있습니다.

*`Dice` provides one instance method, `roll`, which returns an integer value between 1 and the number of sides on the dice. This method calls the generator’s `random()` method to create a new random number between `0.0` and `1.0`, and uses this random number to create a dice roll value within the correct range. Because `generator` is known to adopt `RandomNumberGenerator`, it’s guaranteed to have a `random()` method to call.*

`Dice`는 1에서 주사위의 면의 수 사이의 정수 값을 반환하는 하나의 인스턴스 메서드인 `roll`을 제공합니다. 이 메서드는 생성자의 `random()` 메서드를 호출하여 `0.0`과 `1.0` 사이의 새로운 난수를 생성하고, 이 난수를 사용하여 정확한 범위 내에서 주사위 굴림 값을 생성합니다. 생성자는 난수 생성기를 채택하는 것으로 알려져 있기 때문에  `random()` 메서드를 호출하는 것이 보장됩니다.

*Here’s how the `Dice` class can be used to create a six-sided dice with a `LinearCongruentialGenerator` instance as its random number generator:*

다음은 `Dice` 클래스를 사용하여 `LinearCongruentialGenerator`인스턴스를 난수 생성기로 사용하여 6면 주사위를 만드는 방법입니다:

```swift
var d6 = Dice(sides: 6, generator: LinearCongruentialGenerator())
for _ in 1...5 {
    print("Random dice roll is \(d6.roll())")
}
// Random dice roll is 3
// Random dice roll is 5
// Random dice roll is 4
// Random dice roll is 5
// Random dice roll is 4
```
