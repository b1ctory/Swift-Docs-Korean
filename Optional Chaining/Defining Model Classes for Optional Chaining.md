## *Defining Model Classes for Optional Chaining : 옵셔널 체이닝에 대한 모델 클래스 정의*

*You can use optional chaining with calls to properties, methods, and subscripts that are more than one level deep. This enables you to drill down into subproperties within complex models of interrelated types, and to check whether it’s possible to access properties, methods, and subscripts on those subproperties.*

옵셔널 체이닝을 두 레벨 이상의 프로퍼티, 메서드 및 서브스크립트에 대한 호출과 함께 사용할 수 있습니다. 이렇게 하면 상호 연관된 타입의 복잡한 모델 내 하위 프로퍼티를 드릴다운하고 해당 하위 프로퍼티의 프로퍼티, 메서드 및 서브스크립트에 액세스할 수 있는지 여부를 확인할 수 있습니다.

*The code snippets below define four model classes for use in several subsequent examples, including examples of multilevel optional chaining. These classes expand upon the `Person` and `Residence` model from above by adding a `Room` and `Address` class, with associated properties, methods, and subscripts.*

아래 코드 스니펫은 다단계 옵셔널 체이닝의 예를 포함하여 여러 후속 예제에서 사용할 4가지 모델 클래스를 정의합니다. 이러한 클래스는 관련 프로퍼티, 메서드 및 서브스크립트와 함께 `Room` 및 `Address` 클래스를 추가하여 위에서 `Person` 및 `Residence` 모델로 확장됩니다.

*The `Person` class is defined in the same way as before:*

`Person` 클래스는 이전과 동일한 방식으로 정의됩니다:

```swift
class Person {
    var residence: Residence?
}
```

*The `Residence` class is more complex than before. This time, the `Residence` class defines a variable property called `rooms`, which is initialized with an empty array of type `[Room]`:*

`Residence` 클래스는 이전보다 더 복잡합니다. 이번에 `Residence` 클래스는 `rooms`라는 변수 프로퍼티를 정의하며, 이 속성은 `[Room]` 타입의 빈 배열로 초기화됩니다:

```swift
class Residence {
    var rooms: [Room] = []
    var numberOfRooms: Int {
        return rooms.count
    }
    subscript(i: Int) -> Room {
        get {
            return rooms[i]
        }
        set {
            rooms[i] = newValue
        }
    }
    func printNumberOfRooms() {
        print("The number of rooms is \(numberOfRooms)")
    }
    var address: Address?
}
```

*Because this version of `Residence` stores an array of `Room` instances, its `numberOfRooms` property is implemented as a computed property, not a stored property. The computed `numberOfRooms` property simply returns the value of the `count` property from the `rooms` array.*

이 버전의 `Residence`는 일련의 `Room` 인스턴스를 저장하기 때문에 해당 `numberOfRooms` 프로퍼티는 저장 프로퍼티가 아닌 연산 프로퍼티로 구현됩니다. 연산프로퍼티 `numberOfRooms`는 단순히 `rooms` 배열에서 `count` 프로퍼티의 값을 반환합니다.

*As a shortcut to accessing its `rooms` array, this version of `Residence` provides a read-write subscript that provides access to the room at the requested index in the `rooms` array.*

이 버전의 `Residence`는 `rooms` 배열에 액세스하기 위한 바로 가기로, 읽기-쓰기 서브스크립트를 제공하여 `rooms` 배열에서 요청된 인덱스로 `rooms` 배열에 액세스할 수 있도록 합니다.

*This version of `Residence` also provides a method called `printNumberOfRooms`, which simply prints the number of rooms in the residence.*

이 버전의 `Residence`는 `printNumberOfRooms`라고 불리는 레지던스의 객실 수를 간단히 출력 메서드도 제공합니다.

*Finally, `Residence` defines an optional property called `address`, with a type of `Address?`. The `Address` class type for this property is defined below.*

마지막으로, `Residence`는 `Address?` 타입의 `address`라는 옵셔널 프로퍼티를 정의합니다. 이 프로퍼티의 `Address`클래스 타입은 아래에 정의되어 있습니다.

*The `Room` class used for the `rooms` array is a simple class with one property called `name`, and an initializer to set that property to a suitable room name:*

`rooms` 배열에 사용되는 `Room` 클래스는 `name`이라는 하나의 프로퍼티를 가진 단순 클래스이며 해당 프로퍼티를 적절한 룸 이름으로 설정하기 위한 이니셜라이저입니다:

```swift
class Room {
    let name: String
    init(name: String) { self.name = name }
}
```

*The final class in this model is called `Address`. This class has three optional properties of type `String?`. The first two properties, `buildingName` and `buildingNumber`, are alternative ways to identify a particular building as part of an address. The third property, `street`, is used to name the street for that address:*

이 모델의 마지막 클래스는 `Address`입니다. 이 클래스는 `String?` 타입의 세 가지 옵셔널 프로퍼티를 가집니다. 처음 두 개의 프로퍼티인 `buildingName`과 `buildingNumber`는 주소의 일부로 특정 건물을 식별하는 대체 방법입니다. 세 번째 프로퍼티인 `street`은 해당 주소의 거리 이름을 지정하는 데 사용됩니다:

```swift
class Address {
    var buildingName: String?
    var buildingNumber: String?
    var street: String?
    func buildingIdentifier() -> String? {
        if let buildingNumber = buildingNumber, let street = street {
            return "\(buildingNumber) \(street)"
        } else if buildingName != nil {
            return buildingName
        } else {
            return nil
        }
    }
}
```

*The `Address` class also provides a method called `buildingIdentifier()`, which has a return type of `String?`. This method checks the properties of the address and returns `buildingName` if it has a value, or `buildingNumber` concatenated with `street` if both have values, or `nil` otherwise.*

`Address` 클래스는 반환 타입이 `String?`인 `buildingIdentifier()`라는 메서드도 제공합니다. 이 메서드는 주소의 프로퍼티를 확인하고 값이 있거나 `street`과 연결한 `buildingNumber` 둘 다 값이 있으면 `buildingName`값을 반환하고 값이 없으면 `nil`을 반환합니다.
