## *Raw Values : 원시값*

*The barcode example in [Associated Values](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html#ID148) shows how cases of an enumeration can declare that they store associated values of different types. As an alternative to associated values, enumeration cases can come prepopulated with default values (called raw values), which are all of the same type.*

[링크]의 바코드 예제는 열거형의 케이스가 서로 다른 타입의 관련 값을 저장한다고 선언하는 방법을 보여줍니다. 연결된 값 대신 열거 케이스가 기본값 (원시값이라고 함)으로 미리 채워질 수 있으며, 이 값은 모두 동일한 타입입니다.

*Here’s an example that stores raw ASCII values alongside named enumeration cases:*

다음은 명명된 열거형 케이스와 함께 원시 ASCII 값을 저장하는 예시입니다.

```swift
enum ASCIIControlCharacter: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}
```

*Here, the raw values for an enumeration called `ASCIIControlCharacter` are defined to be of type `Character`, and are set to some of the more common ASCII control characters. `Character` values are described in [Strings and Characters](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html).*

여기서 `ASCIIControlCharacter`라는 열거형의 원시 값은 Character 타입으로 정의되며, 보다 일반적인 ASCII 제어 문자 중 일부로 설정됩니다. Character 값은 [링크]에 설명되어 있습니다.

*Raw values can be strings, characters, or any of the integer or floating-point number types. Each raw value must be unique within its enumeration declaration.*

원시값은 문자열, 문자 혹은 정수 혹은 부동 소수점 숫자 타입일 수 있습니다. 각 원시 값은 열거형 선언 내에서 고유해야 합니다.

> *NOTE*
> 
> *Raw values are not the same as associated values. Raw values are set to prepopulated values when you first define the enumeration in your code, like the three ASCII codes above. The raw value for a particular enumeration case is always the same. Associated values are set when you create a new constant or variable based on one of the enumeration’s cases, and can be different each time you do so.*
> 
> 원시값은 연관된 값과 같지 않습니다. 원시 값은 위의 세가지 ASCII 코드와 같이 콛에 열거형을 처음 정의할 때 미리 채워진 값으로 설정됩니다. 특정 열거형 케이스의 원시값은 항상 동일합니다. 연결된 값은 열거형의 경우 중 하나를 기준으로 새 상수 혹은 변수를 생성할 때 설정되며, 생성할 때마다 달라질 수 있습니다.

### *Implicitly Assigned Raw Values : 원시값을 암시적으로 할당*

*When you’re working with enumerations that store integer or string raw values, you don’t have to explicitly assign a raw value for each case. When you don’t, Swift automatically assigns the values for you.*

정수 혹은 문자열 원시값을 저장하는 열거형으로 작업할 때 각 경우에 원시값을 명시적으로 할당할 필요가 없습니다. 그렇지 않으면 Swift가 자동으로 값을 할당합니다.

*For example, when integers are used for raw values, the implicit value for each case is one more than the previous case. If the first case doesn’t have a value set, its value is `0`.*

예를 들어, 원시 값에 정수를 사용하는 경우 각 경우의 암시적 값은 이전 케이스보다 1개 더 많습니다. 첫번째 사레에 값이 설정되지 않은 경우 값은 0입니다.

*The enumeration below is a refinement of the earlier `Planet` enumeration, with integer raw values to represent each planet’s order from the sun:*

아래의 열거형은 이전의 Planet 열거를 개선한 것으로, 태양으로부터의 각 행성의 순서르 나타내는 정수 원시 값을 사용합니다.

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

*In the example above, `Planet.mercury` has an explicit raw value of `1`, `Planet.venus` has an implicit raw value of `2`, and so on.*

위의 예에서, Planet.mercury는 명시적인 원시 값인 `1`, `Planet.venus` 를 가지고, 암시적인 원시 값이 `2` 등등 입니다.

*When strings are used for raw values, the implicit value for each case is the text of that case’s name.*

원시값에 문자열을 사용하는 경우 각 케이스의 암시적인 값은 해당 케이스 이름의 텍스트입니다. 

*The enumeration below is a refinement of the earlier `CompassPoint` enumeration, with string raw values to represent each direction’s name:*

아래 열거형은 각 방향의 이름을 나타내는 문자열 원시값을 사용해서 이전의 `CompassPoint` 열거형을 개선한 것입니다.

```swift
enum CompassPoint: String {
    case north, south, east, west
}
```

*In the example above, `CompassPoint.south` has an implicit raw value of `"south"`, and so on.*

위의 예에서 CompassPoint.south는 암묵적인 원시값 `"south"`을 가집니다.

*You access the raw value of an enumeration case with its `rawValue` property:*

`rawValue` 속성을 사용해서 열거형 케이스의 원시 값에 엑세스할 수 있습니다.

```swift
let earthsOrder = Planet.earth.rawValue
// earthsOrder is 3

let sunsetDirection = CompassPoint.west.rawValue
// sunsetDirection is "west"
```

### *Initializing from a Raw Value : 원시값에서 초기화*

*If you define an enumeration with a raw-value type, the enumeration automatically receives an initializer that takes a value of the raw value’s type (as a parameter called `rawValue`) and returns either an enumeration case or `nil`. You can use this initializer to try to create a new instance of the enumeration.*

원시값 타입으로 열거를 정의하는 경우 열거는 자동으로 원시값 타입의 값 (`rawValue`라고 불리는 매개변수)을 가져와서 열거형 케이스 혹은 `nil`을 반환하는 이니셜라이저를 수신합니다. 이 이니셜라이즈를 사용해서 열거형의 새 인스턴스를 만들 수 있습니다.

*This example identifies Uranus from its raw value of `7`:*

이 예시는 원시값 `7`에서 천왕성을 식별합니다 :

```swift
let possiblePlanet = Planet(rawValue: 7)
// possiblePlanet is of type Planet? and equals Planet.uranus
```

*Not all possible `Int` values will find a matching planet, however. Because of this, the raw value initializer always returns an optional enumeration case. In the example above, `possiblePlanet` is of type `Planet?`, or “optional `Planet`.”*

그러나 모든 가능한 `Int` 값이 일치하는 행성을 찾는 것은 아닙니다. 따라서 원시값 이니셜라이저는 항상 옵셔널 열거형 케이스를 반환합니다.

> *NOTE*
> 
> *The raw value initializer is a failable initializer, because not every raw value will return an enumeration case. For more information, see [Failable Initializers](https://docs.swift.org/swift-book/ReferenceManual/Declarations.html#ID376).*
> 
> 모든 원시 값이 열거형 케이스를 반환하지 않기 때문에 원시값 이니셜라이저는 실패 가능한 이니셜라이저 입니다.자세한 내용은 [링크]를 참조하세요.

*If you try to find a planet with a position of `11`, the optional `Planet` value returned by the raw value initializer will be `nil`:*

위치가 11인 행성을 찾으려는 경우 원시값 이니셜라이저에서 반환되는 옵셔널 `Planet` 값은 `nil` 이 됩니다.

```swift
let positionToFind = 11
if let somePlanet = Planet(rawValue: positionToFind) {
    switch somePlanet {
    case .earth:
        print("Mostly harmless")
    default:
        print("Not a safe place for humans")
    }
} else {
    print("There isn't a planet at position \(positionToFind)")
}
// Prints "There isn't a planet at position 11"
```

*This example uses optional binding to try to access a planet with a raw value of `11`. The statement `if let somePlanet = Planet(rawValue: 11)` creates an optional `Planet`, and sets `somePlanet` to the value of that optional `Planet` if it can be retrieved. In this case, it isn’t possible to retrieve a planet with a position of `11`, and so the `else` branch is executed instead.*

이 예시에서는 원시값이 `11`인 행성에 엑세스하기 위해 옵셔널 바인딩을 사용합니다.  `if let somePlanet = Planet(rawValue: 11)` 이라는 문장은 옵셔널인 Planet 을 생성하고, 검색할 수 있는 경우 `somePlanet`을 옵셔널인 `Planet` 값으로 설정합니다. 이 경우 위치가 `11`인 행성은 회수할 수 없으므로 다른 분기가 대신 실행됩니다.


