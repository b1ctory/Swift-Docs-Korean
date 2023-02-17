## *Optional Protocol Requirements : 옵셔널 프로토콜요구사항*

*You can define optional requirements for protocols. These requirements don’t have to be implemented by types that conform to the protocol. Optional requirements are prefixed by the `optional` modifier as part of the protocol’s definition. Optional requirements are available so that you can write code that interoperates with Objective-C. Both the protocol and the optional requirement must be marked with the `@objc` attribute. Note that `@objc` protocols can be adopted only by classes that inherit from Objective-C classes or other `@objc` classes. They can’t be adopted by structures or enumerations.*

프로토콜에 대한 옵셔널 요구사항을 정의할 수 있습니다. 이러한 요구 사항은 프로토콜을 준수하는 타입에 의해 구현될 필요가 없습니다. 옵셔널 요구 사항은 프로토콜 정의의 일부로 `optional` 수정자가 붙습니다. Objective-C와 상호 운용되는 코드를 작성할 수 있도록 옵셔널 요구 사항을 사용할 수 있습니다. 프로토콜과 옵셔널 요구 사항은 모두 `@objc` 속성으로 표시되어야 합니다. `@objc` 프로토콜은 Objective-C 클래스 또는 기타 `@objc` 클래스에서 상속된 클래스에서만 채택할 수 있습니다. 구조체나 열거형에 의해 채택될 수 없습니다.

*When you use a method or property in an optional requirement, its type automatically becomes an optional. For example, a method of type `(Int) -> String` becomes `((Int) -> String)?`. Note that the entire function type is wrapped in the optional, not the method’s return value.*

옵셔널 요구 사항에서 메서드 또는 프로퍼티를 사용하면 해당 타입이 자동으로 옵셔널이 됩니다. 예를 들어 `(Int) -> String` 타입의 메서드는 `((Int) -> String)?`이 됩니다. 전체 함수 타입은 메서드의 리턴 값이 아니라 옵셔널로 래핑됩니다.

*An optional protocol requirement can be called with optional chaining, to account for the possibility that the requirement was not implemented by a type that conforms to the protocol. You check for an implementation of an optional method by writing a question mark after the name of the method when it’s called, such as `someOptionalMethod?(someArgument)`. For information on optional chaining, see [Optional Chaining](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html).*

프로토콜을 준수하는 타입에 의해 요구 사항이 구현되지 않았을 가능성을 설명하기 위해 옵셔널 프로토콜 요구 사항을 옵셔널 체이닝과 함께 호출할 수 있습니다. `someOptionalMethod?(someArgument)`와 같이 호출될 때 메소드 이름 뒤에 물음표를 작성하여 옵셔널 메서드의 구현을 확인합니다. 옵셔널 체이닝에 대한 자세한 내용은 [링크]를 참조하세요.

*The following example defines an integer-counting class called `Counter`, which uses an external data source to provide its increment amount. This data source is defined by the `CounterDataSource` protocol, which has two optional requirements:*

다음 예는 외부 데이터 소스를 사용하여 증가량을 제공하는 `Counter`라는 정수 계산 클래스를 정의합니다. 이 데이터 소스는 두 가지 옵셔널 요구 사항이 있는 `CounterDataSource` 프로토콜에 의해 정의됩니다.

```swift
@objc protocol CounterDataSource {
    @objc optional func increment(forCount count: Int) -> Int
    @objc optional var fixedIncrement: Int { get }
}
```

*The `CounterDataSource` protocol defines an optional method requirement called `increment(forCount:)` and an optional property requirement called `fixedIncrement`. These requirements define two different ways for data sources to provide an appropriate increment amount for a `Counter` instance.*

`CounterDataSource` 프로토콜은 `increment(forCount:)`라는 옵셔널 메서드 요구 사항과 `fixed`라는 옵셔널 프로퍼티 요구 사항을 정의합니다. 이러한 요구사항은 데이터 소스가 `Counter` 인스턴스에 대해 적절한 증가량을 제공하는 두 가지 다른 방법을 정의합니다.

> *NOTE*
> 
> *Strictly speaking, you can write a custom class that conforms to `CounterDataSource` without implementing either protocol requirement. They’re both optional, after all. Although technically allowed, this wouldn’t make for a very good data source.*
> 
> 엄밀하게 말하면, 두 프로토콜 요구 사항을 구현하지 않고도 `CounterDataSource`를 준수하는 사용자 정의 클래스를 작성할 수 있습니다. 결국 둘 다 옵셔널입니다. 기술적으로 허용되기는 하지만, 이것은 그다지 좋은 데이터 소스가 되지는 않을 것입니다.

*The `Counter` class, defined below, has an optional `dataSource` property of type `CounterDataSource?`:*

아래 정의된 `Counter` 클래스는 `CounterDataSource?` 타입의 옵셔널 `dataSource` 프로퍼티를 가지고 있습니다:

```swift
class Counter {
    var count = 0
    var dataSource: CounterDataSource?
    func increment() {
        if let amount = dataSource?.increment?(forCount: count) {
            count += amount
        } else if let amount = dataSource?.fixedIncrement {
            count += amount
        }
    }
}
```

*The `Counter` class stores its current value in a variable property called `count`. The `Counter` class also defines a method called `increment`, which increments the `count` property every time the method is called.*

`Counter` 클래스는 현재 값을 `count`라는 변수 프로퍼티에 저장합니다. `Counter` 클래스는 또한 메서드를 호출할 때마다 `count` 프로퍼티를 증가시키는 `increment`라는 메서드를 정의합니다.

*The `increment()` method first tries to retrieve an increment amount by looking for an implementation of the `increment(forCount:)` method on its data source. The `increment()` method uses optional chaining to try to call `increment(forCount:)`, and passes the current `count` value as the method’s single argument.*

`increment()` 메서드는 먼저 데이터 소스에서 `increment(forCount:)` 메서드의 구현을 찾아 증가량을 검색하려고 합니다. `increment()` 메서드는 옵셔널 체인을 사용하여 `increment(forCount:)`를 호출하고 현재 `count` 값을 메서드의 단일 인수로 전달합니다.

*Note that two levels of optional chaining are at play here. First, it’s possible that `dataSource` may be `nil`, and so `dataSource` has a question mark after its name to indicate that `increment(forCount:)` should be called only if `dataSource` isn’t `nil`. Second, even if `dataSource` does exist, there’s no guarantee that it implements `increment(forCount:)`, because it’s an optional requirement. Here, the possibility that `increment(forCount:)` might not be implemented is also handled by optional chaining. The call to `increment(forCount:)` happens only if `increment(forCount:)` exists—that is, if it isn’t `nil`. This is why `increment(forCount:)` is also written with a question mark after its name.*

여기에는 두 가지 수준의 옵셔널 체인이 적용됩니다. 첫째, `dataSource`가 `nil`일 수 있으므로, `dataSource`는 이름 뒤에 물음표를 붙여 `dataSource`가 `nil`이 아닌 경우에만 `increment(forCount:)`를 호출해야 함을 나타낼 수 있습니다. 둘째로, `dataSource`가 존재한다고 해도 옵셔널 요구사항이기 때문에 `increment(forCount:)`를 구현한다는 보장이 없습니다. 여기서 `increment(forCount:)`가 구현되지 않을 가능성도 옵셔널 체인에 의해 처리됩니다. `increment(forCount:)` 호출은 `increment(forCount:)`가 존재하는 경우 즉, `nil`이 아닌 경우에만 발생합니다. 그래서 `increment(forCount:)`도 이름 뒤에 물음표가 붙습니다.

*Because the call to `increment(forCount:)` can fail for either of these two reasons, the call returns an optional `Int` value. This is true even though `increment(forCount:)` is defined as returning a non-optional `Int` value in the definition of `CounterDataSource`. Even though there are two optional chaining operations, one after another, the result is still wrapped in a single optional. For more information about using multiple optional chaining operations, see [Linking Multiple Levels of Chaining](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html#ID252).*

`increment(forCount:)`에 대한 호출이 다음 두 가지 이유 중 하나로 실패할 수 있으므로 호출은 옵셔널 `Int` 값을 반환합니다. 이는 `increment(forCount:)`가 `CounterDataSource`의 정의에서 비옵셔널 `Int` 값을 반환하는 것으로 정의되지만 사실입니다. 옵셔널 체인 작업이 두 개씩 있지만 결과는 하나의 옵셔널 작업으로 마무리됩니다. 다중 옵셔널 체인 작업 사용에 대한 자세한 내용은 [링크]를 참조하세요.

*After calling `increment(forCount:)`, the optional `Int` that it returns is unwrapped into a constant called `amount`, using optional binding. If the optional `Int` does contain a value—that is, if the delegate and method both exist, and the method returned a value—the unwrapped `amount` is added onto the stored `count` property, and incrementation is complete.*

`increment(forCount:)`를 호출한 후 반환되는 옵셔널 `Int`는 옵셔널 바인딩을 사용하여 `amount`라는 상수로 언래핑됩니다. 옵셔널 `Int`에 값이 포함되어 있으면(즉, 델리게이트와 메서드가 모두 존재하고 메서드가 값을 반환한 경우), 언래핑된 `amount`가 저장프로퍼티 `count` 에 추가되고 증가가 완료됩니다.

*If it’s not possible to retrieve a value from the `increment(forCount:)` method—either because `dataSource` is nil, or because the data source doesn’t implement `increment(forCount:)`—then the `increment()` method tries to retrieve a value from the data source’s `fixedIncrement` property instead. The `fixedIncrement` property is also an optional requirement, so its value is an optional `Int` value, even though `fixedIncrement` is defined as a non-optional `Int` property as part of the `CounterDataSource` protocol definition.*

`increment(forCount:)` 메서드에서 값을 검색할 수 없는 경우(`dataSource`가 nil이거나 데이터 소스가 `increment(forCount:)`를 구현하지 않기 때문에) `increment( )` 메서드는 대신 데이터 소스의 `fixedIncrement` 프로퍼티에서 값을 검색하려고 시도합니다. `fixedIncrement` 속성도 선택적 요구 사항이므로 `fixedIncrement`가 `CounterDataSource` 프로토콜 정의의 일부로 옵셔널이 아닌 `Int` 프로퍼티로 정의되더라도 해당 값은 옵셔널 `Int` 값입니다.

*Here’s a simple `CounterDataSource` implementation where the data source returns a constant value of `3` every time it’s queried. It does this by implementing the optional `fixedIncrement` property requirement:*

다음은 데이터 소스가 쿼리될 때마다 상수 값 `3`을 반환하는 간단한 `CounterDataSource` 구현입니다. 옵셔널 `fixedIncrement` 프로퍼티 요구 사항을 구현하여 이를 수행합니다.

```swift
class ThreeSource: NSObject, CounterDataSource {
    let fixedIncrement = 3
}
```

*You can use an instance of `ThreeSource` as the data source for a new `Counter` instance:*

`ThreeSource` 인스턴스를 새 `Counter` 인스턴스의 데이터 소스로 사용할 수 있습니다.

```swift
var counter = Counter()
counter.dataSource = ThreeSource()
for _ in 1...4 {
    counter.increment()
    print(counter.count)
}
// 3
// 6
// 9
// 12
```

*The code above creates a new `Counter` instance; sets its data source to be a new `ThreeSource` instance; and calls the counter’s `increment()` method four times. As expected, the counter’s `count` property increases by three each time `increment()` is called.*

위의 코드는 새로운 `Counter` 인스턴스를 생성합니다. 데이터 소스를 새로운 `ThreeSource` 인스턴스로 설정합니다. 카운터의 `increment()` 메서드를 네 번 호출합니다. 예상대로 카운터의 `count` 프로퍼티는 `increment()`가 호출될 때마다 3씩 증가합니다.

*Here’s a more complex data source called `TowardsZeroSource`, which makes a `Counter` instance count up or down towards zero from its current `count` value:*

다음은 `TowardsZeroSource`라는 더 복잡한 데이터 소스로, `Counter` 인스턴스가 현재 `count` 값에서 0을 향해 올라가거나 내려가도록 합니다.

```swift
class TowardsZeroSource: NSObject, CounterDataSource {
    func increment(forCount count: Int) -> Int {
        if count == 0 {
            return 0
        } else if count < 0 {
            return 1
        } else {
            return -1
        }
    }
}
```

*The `TowardsZeroSource` class implements the optional `increment(forCount:)` method from the `CounterDataSource` protocol and uses the `count` argument value to work out which direction to count in. If `count` is already zero, the method returns `0` to indicate that no further counting should take place.*

`TowardsZeroSource` 클래스는 `CounterDataSource` 프로토콜의 옵셔널 `increment(forCount:)` 메서드를 구현하고 `count` 인수 값을 사용하여 계산할 방향을 알아냅니다. `count`가 이미 0인 경우 메서드는 더 이상 세지 ​​않아야 함을 나타내기 위해 `0`을 반환합니다.

*You can use an instance of `TowardsZeroSource` with the existing `Counter` instance to count from `-4` to zero. Once the counter reaches zero, no more counting takes place:*

`TowardsZeroSource` 인스턴스를 기존 `Counter` 인스턴스와 함께 사용하여 `-4`에서 0까지 셀 수 있습니다. 카운터가 0에 도달하면 더 이상 계산이 수행되지 않습니다.

```swift
counter.count = -4
counter.dataSource = TowardsZeroSource()
for _ in 1...5 {
    counter.increment()
    print(counter.count)
}
// -3
// -2
// -1
// 0
// 0
```
