### *Unowned References and Implicitly Unwrapped Optional Properties : 미소유 참조 및 암묵적 언래핑된 옵셔널 프로퍼티*

*The examples for weak and unowned references above cover two of the more common scenarios in which it’s necessary to break a strong reference cycle.*

위의 약한 참조 및 미소유 참조에 대한 예는 강력한 순환 참조를 중단해야 하는 두 가지 공통 시나리오를 다룹니다.

*The `Person` and `Apartment` example shows a situation where two properties, both of which are allowed to be `nil`, have the potential to cause a strong reference cycle. This scenario is best resolved with a weak reference.*

`Person` 및 `Apartment` 예시는 둘 다 `nil`로 허용되는 두 프로퍼티가 강한 순환 참조를 유발할 가능성이 있는 상황을 보여줍니다. 이 시나리오는 약한 참조로 가장 잘 해결됩니다.

*The `Customer` and `CreditCard` example shows a situation where one property that’s allowed to be `nil` and another property that can’t be `nil` have the potential to cause a strong reference cycle. This scenario is best resolved with an unowned reference.*

`Customer` 및 `CreditCard` 예시는 `nil`이 허용되는 프로퍼티 하나와 `nil`이 될 수 없는 다른 프로퍼티가 강력한 순환 참조를 유발할 가능성이 있는 상황을 보여줍니다. 이 시나리오는 미소유 참조로 가장 잘 해결됩니다.

*However, there’s a third scenario, in which both properties should always have a value, and neither property should ever be `nil` once initialization is complete. In this scenario, it’s useful to combine an unowned property on one class with an implicitly unwrapped optional property on the other class.*

그러나 세 번째 시나리오는 두 프로퍼티 모두 항상 값을 가져야 하며 초기화가 완료되면 어느 프로퍼티도 `nil`이 되어서는 안 됩니다. 이 시나리오에서는 한 클래스의 소유되지 않은 프로퍼티를 다른 클래스의 암시적으로 언래핑된 옵셔널 프로퍼티와 결합하는 것이 유용합니다.

*This enables both properties to be accessed directly (without optional unwrapping) once initialization is complete, while still avoiding a reference cycle. This section shows you how to set up such a relationship.*

이렇게 초기화가 완료되면 순환 참조를 피하면서 두 프로퍼티에 직접 액세스할 수 있습니다(옵셔널 언래핑 없이). 이 섹션에서는 이러한 관계를 설정하는 방법을 보여줍니다.

*The example below defines two classes, `Country` and `City`, each of which stores an instance of the other class as a property. In this data model, every country must always have a capital city, and every city must always belong to a country. To represent this, the `Country` class has a `capitalCity` property, and the `City` class has a `country` property:*

아래 예에서는 각각 다른 클래스의 인스턴스를 프로퍼티로 저장하는 두 개의 클래스인 `Country`와 `City`를 정의합니다. 이 데이터 모델에서 모든 국가에는 항상 수도가 있어야 하며 모든 도시는 항상 국가에 속해야 합니다. 이를 나타내기 위해 `Country` 클래스에는 `capitalCity` 프로퍼티가 있고 `City` 클래스에는 `country` 프로퍼티가 있습니다.

```swift
class Country {
    let name: String
    var capitalCity: City!
    init(name: String, capitalName: String) {
        self.name = name
        self.capitalCity = City(name: capitalName, country: self)
    }
}

class City {
    let name: String
    unowned let country: Country
    init(name: String, country: Country) {
        self.name = name
        self.country = country
    }
}
```

*To set up the interdependency between the two classes, the initializer for `City` takes a `Country` instance, and stores this instance in its `country` property.*

두 클래스 간의 상호 의존성을 설정하기 위해 `City`의 이니셜라이저는 `Country` 인스턴스를 가져오고 이 인스턴스를 `country` 프로퍼티에 저장합니다.

*The initializer for `City` is called from within the initializer for `Country`. However, the initializer for `Country` can’t pass `self` to the `City` initializer until a new `Country` instance is fully initialized, as described in [Two-Phase Initialization](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization#Two-Phase-Initialization).*

`City`의 이니셜라이저는 `Country`의 이니셜라이저 내에서 호출됩니다. 그러나 [링크]에 설명된 바와 같이 새로운 `Country` 인스턴스가 완전히 초기화될 때까지 `Country`의 초기화는 `City` 초기화에 `self`을 전달할 수 없습니다.

*To cope with this requirement, you declare the `capitalCity` property of `Country` as an implicitly unwrapped optional property, indicated by the exclamation point at the end of its type annotation (`City!`). This means that the `capitalCity` property has a default value of `nil`, like any other optional, but can be accessed without the need to unwrap its value as described in [Implicitly Unwrapped Optionals](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Implicitly-Unwrapped-Optionals).*

이 요구 사항에 대처하기 위해 타입 주석 끝에 느낌표(`City!`)로 표시된 `Country`의 `capitalCity` 프로퍼티를 암묵적으로 포장 해제된 옵션 속성으로 선언합니다. 즉, `capitalCity` 프로퍼티는 다른 옵셔널과 마찬가지로 기본값인 `capitalcity`를 갖지만 [링크]에 설명된 대로 값을 언래핑할 필요 없이 액세스할 수 있습니다.

*Because `capitalCity` has a default `nil` value, a new `Country` instance is considered fully initialized as soon as the `Country` instance sets its `name` property within its initializer. This means that the `Country` initializer can start to reference and pass around the implicit `self` property as soon as the `name` property is set. The `Country` initializer can therefore pass `self` as one of the parameters for the `City` initializer when the `Country` initializer is setting its own `capitalCity` property.*

`capitalCity`는 기본값인 `nil`을 가지고 있기 때문에 `Country` 인스턴스가 이니셜라이저 내에서 `name` 프로퍼티를 설정하는 즉시 새로운 `Country` 인스턴스가 완전히 초기화된 것으로 간주됩니다. 즉, `name` 프로퍼티가 설정되는 즉시 `Country` 이니셜라이저가 참조를 시작하고 암시적 `self` 프로퍼티를 우회할 수 있습니다. 따라서 `Country` 이니셜라이저가 자체 `capitalCity` 프로퍼티를 설정할 때 `Country` 이니셜라이저는 `self`를 `City`이니셜라이저의 매개 변수 중 하나로 전달할 수 있습니다.

*All of this means that you can create the `Country` and `City` instances in a single statement, without creating a strong reference cycle, and the `capitalCity` property can be accessed directly, without needing to use an exclamation point to unwrap its optional value:*

이 모든 것은 강력한 참조 주기를 생성하지 않고 단일 문에서 `Country` 및 `City` 인스턴스를 생성할 수 있으며 옵셔널 값을 풀기 위해 느낌표를 사용하지 않고도 `capitalCity` 프로퍼티에 직접 액세스할 수 있다는 것을 의미합니다:

```swift
var country = Country(name: "Canada", capitalName: "Ottawa")
print("\(country.name)'s capital city is called \(country.capitalCity.name)")
// Prints "Canada's capital city is called Ottawa"
```

*In the example above, the use of an implicitly unwrapped optional means that all of the two-phase class initializer requirements are satisfied. The `capitalCity` property can be used and accessed like a non-optional value once initialization is complete, while still avoiding a strong reference cycle.*

위의 예에서 암시적으로 언래핑된 옵셔널을 사용한다는 것은 모든 2단계 클래스 이니셜라이저 요구 사항이 충족됨을 의미합니다. `capitalCity` 프로퍼티는 초기화가 완료되면 옵셔널이 아닌 값처럼 사용하고 액세스할 수 있지만 여전히 강력한 순환 참조를 피합니다.





