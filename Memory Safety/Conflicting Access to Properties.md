## *Conflicting Access to Properties : 프로퍼티에 대한 엑세스 충돌*

*Types like structures, tuples, and enumerations are made up of individual constituent values, such as the properties of a structure or the elements of a tuple. Because these are value types, mutating any piece of the value mutates the whole value, meaning read or write access to one of the properties requires read or write access to the whole value. For example, overlapping write accesses to the elements of a tuple produces a conflict:*

구조체, 튜플 및 열거형과 같은 타입은 구조체의 프로퍼티 또는 튜플의 요소와 같은 개별 구성 값으로 구성됩니다. 이들은 값 타입이기 때문에 값의 일부를 변경하면 전체 값이 변경됩니다. 즉, 프로퍼티 중 하나에 대한 읽기 또는 쓰기 액세스에는 전체 값에 대한 읽기 또는 쓰기 액세스가 필요합니다. 예를 들어 튜플의 요소에 대한 쓰기 액세스가 중복되면 충돌이 발생합니다.

```swift
var playerInformation = (health: 10, energy: 20)
balance(&playerInformation.health, &playerInformation.energy)
// Error: conflicting access to properties of playerInformation
```

*In the example above, calling `balance(_:_:)` on the elements of a tuple produces a conflict because there are overlapping write accesses to `playerInformation`. Both `playerInformation.health` and `playerInformation.energy` are passed as in-out parameters, which means `balance(_:_:)` needs write access to them for the duration of the function call. In both cases, a write access to the tuple element requires a write access to the entire tuple. This means there are two write accesses to `playerInformation` with durations that overlap, causing a conflict.*

위의 예에서 튜플의 요소에서 `balance(_:_:)`를 호출하면 `playerInformation`에 대한 중복 쓰기 액세스가 있기 때문에 충돌이 발생합니다. `playerInformation.health` 및 `playerInformation.energy`는 모두 in-out 매개변수로 전달되며, 이는 `balance(_:_:)`가 함수 호출 기간 동안 쓰기 액세스 권한이 필요함을 의미합니다. 두 경우 모두 튜플 요소에 대한 쓰기 액세스에는 전체 튜플에 대한 쓰기 액세스가 필요합니다. 즉, 기간이 겹치는 `playerInformation`에 대한 두 가지 쓰기 액세스가 있어 충돌이 발생합니다.

*The code below shows that the same error appears for overlapping write accesses to the properties of a structure that’s stored in a global variable.*

아래 코드는 전역 변수에 저장된 구조체의 프로퍼티에 대한 중복 쓰기 액세스에 대해 동일한 오류가 나타나는 것을 보여줍니다.

```swift
var holly = Player(name: "Holly", health: 10, energy: 10)
balance(&holly.health, &holly.energy)  // Error
```

*In practice, most access to the properties of a structure can overlap safely. For example, if the variable `holly` in the example above is changed to a local variable instead of a global variable, the compiler can prove that overlapping access to stored properties of the structure is safe:*

실제로 구조체의 프로퍼티에 대한 대부분의 액세스는 안전하게 중첩될 수 있습니다. 예를 들어 위의 예에서 변수 `holly`가 전역 변수 대신 로컬 변수로 변경되면 컴파일러는 구조체의 저장 프로퍼티에 대한 중첩 액세스가 안전함을 증명할 수 있습니다.

```swift
func someFunction() {
    var oscar = Player(name: "Oscar", health: 10, energy: 10)
    balance(&oscar.health, &oscar.energy)  // OK
}
```

*In the example above, Oscar’s health and energy are passed as the two in-out parameters to `balance(_:_:)`. The compiler can prove that memory safety is preserved because the two stored properties don’t interact in any way.*

위 예시에서 오스카의 체력과 에너지는 `balance(_:_:)`에 두 개의 in-out 매개변수로 전달됩니다. 컴파일러는 두 개의 저장 프로퍼티가 어떤 식으로든 상호 작용하지 않기 때문에 메모리 안전이 유지됨을 증명할 수 있습니다.

*The restriction against overlapping access to properties of a structure isn’t always necessary to preserve memory safety. Memory safety is the desired guarantee, but exclusive access is a stricter requirement than memory safety — which means some code preserves memory safety, even though it violates exclusive access to memory. Swift allows this memory-safe code if the compiler can prove that the nonexclusive access to memory is still safe. Specifically, it can prove that overlapping access to properties of a structure is safe if the following conditions apply:*

구조체 프로퍼티에 대한 중복 액세스에 대한 제한이 메모리 안전을 유지하는 데 항상 필요한 것은 아닙니다. 메모리 안전성이 바람직한 보장이지만 배타적 액세스는 메모리 안전성보다 더 엄격한 요구 사항입니다. 즉, 일부 코드는 메모리에 대한 배타적 액세스를 위반하더라도 메모리 안전성을 유지합니다. Swift는 컴파일러가 메모리에 대한 비배타적 액세스가 여전히 안전하다는 것을 증명할 수 있는 경우 이 메모리 안전 코드를 허용합니다. 특히 다음 조건이 적용되는 경우 구조체의 프로퍼티에 대한 중복 액세스가 안전함을 증명할 수 있습니다.

- *You’re accessing only stored properties of an instance, not computed properties or class properties.*
  
  연산 프로퍼티나 클래스 프로퍼티가 아닌 인스턴스의 저장 프로퍼티에만 액세스하고 있습니다.

- *The structure is the value of a local variable, not a global variable.*
  
  구조체는 전역 변수가 아닌 지역 변수의 값입니다.

- *The structure is either not captured by any closures, or it’s captured only by nonescaping closures.*
  
  구조체가 클로저에 의해 캡처되지 않거나 비탈출 클로저에 의해서만 캡처됩니다.

*If the compiler can’t prove the access is safe, it doesn’t allow the access.*

컴파일러가 접근이 안전하다는 것을 증명할 수 없다면 접근을 허용하지 않습니다.
