## *Default Initializers : 기본 이니셜라이저*

*Swift provides a default initializer for any structure or class that provides default values for all of its properties and doesn’t provide at least one initializer itself. The default initializer simply creates a new instance with all of its properties set to their default values.*

Swift는 모든 프로퍼티에 대한 기본값을 제공하는 구조체 또는 클래스에 대해 기본 이니셜라이저를 제공하며, 하나 이상의 이니셜라이저 자체를 제공하지 않습니다. 기본 이니셜라이저는 모든 프로퍼티를 기본값으로 설정한 상태에서 새 인스턴스를 만듭니다.

*This example defines a class called `ShoppingListItem`, which encapsulates the name, quantity, and purchase state of an item in a shopping list:*

이 예에서는 쇼핑 목록에 있는 항목의 이름, 수량 및 구매 상태를 캡슐화하는 `ShoppingListItem`이라는 클래스를 정의합니다:

```swift
class ShoppingListItem {
    var name: String?
    var quantity = 1
    var purchased = false
}
var item = ShoppingListItem()
```

*Because all properties of the `ShoppingListItem` class have default values, and because it’s a base class with no superclass, `ShoppingListItem` automatically gains a default initializer implementation that creates a new instance with all of its properties set to their default values. (The `name` property is an optional `String` property, and so it automatically receives a default value of `nil`, even though this value isn’t written in the code.) The example above uses the default initializer for the `ShoppingListItem` class to create a new instance of the class with initializer syntax, written as `ShoppingListItem()`, and assigns this new instance to a variable called `item`.*

`ShoppingListItem` 클래스의 모든 프로퍼티는 기본값을 가지며 슈퍼클래스가 없는 기본 클래스이기 때문에 `ShoppingListItem`은 모든 프로퍼티를 기본값으로 설정한 새 인스턴스를 생성하는 기본 초기화 구현을 자동으로 가져옵니다. (`name` 프로퍼티는 옵셔널 `String` 프로퍼티이므로 이 값이 코드에 기록되지 않더라도 기본값인 `nil`을 자동으로 수신합니다.) 위의 예에서는 `ShoppingListItem` 클래스에 대한 기본 이니셜라이저를 사용하여 `ShoppingListItem()`으로 작성된 이니셜라이저 구문을 사용하여 클래스의 새 인스턴스를 만들고 이 새 인스턴스를 `item`이라는 변수에 할당합니다.

### *Memberwise Initializers for Structure Types : 구조체 타입에 대한 멤버별 이니셜라이저*

*Structure types automatically receive a memberwise initializer if they don’t define any of their own custom initializers. Unlike a default initializer, the structure receives a memberwise initializer even if it has stored properties that don’t have default values.*

구조체 타입은 자체 사용자 정의 이니셜라이저를 정의하지 않는 경우 자동으로 멤버별 이니셜라이저를 수신합니다. 기본 이니셜라이저와 달리 구조는 기본값이 없는 저장 프로퍼티를 가진 경우에도 멤버별 이니셜라이저를 받습니다.

*The memberwise initializer is a shorthand way to initialize the member properties of new structure instances. Initial values for the properties of the new instance can be passed to the memberwise initializer by name.*

멤버별 이니셜라이저는 새 구조체 인스턴스의 멤버 프로퍼티를 초기화하는 간단한 방법입니다. 새 인스턴스의 프로퍼티에 대한 초기값은 이름으로 멤버별 이니셜라이저에 전달할 수 있습니다.

*The example below defines a structure called `Size` with two properties called `width` and `height`. Both properties are inferred to be of type `Double` by assigning a default value of `0.0`.*

아래 예제는 `width`와 `height`라는 두 가지 프로퍼티를 가진 `Size`라는 구조체를 정의합니다. 두 프로퍼티 모두 기본값 `0.0`을 할당하여  `Double` 타입으로 추론됩니다.

*The `Size` structure automatically receives an `init(width:height:)` memberwise initializer, which you can use to initialize a new `Size` instance:*

`Size` 구조체는 새로운 `Size` 인스턴스를 초기화하는데 사용할 수 있는`init(width:height:)`멤버별 이니셜라이저를 자동으로 수신합니다:

```swift
struct Size {
    var width = 0.0, height = 0.0
}
let twoByTwo = Size(width: 2.0, height: 2.0)
```

*When you call a memberwise initializer, you can omit values for any properties that have default values. In the example above, the `Size` structure has a default value for both its `height` and `width` properties. You can omit either property or both properties, and the initializer uses the default value for anything you omit. For example:*

멤버별 이니셜라이저를 호출할 때 기본값이 있는 프로퍼티의 값을 생략할 수 있습니다. 위의 예에서 `Size` 구조체는 `height`와 `width` 프로퍼티 모두에 대한 기본값을 가집니다. 프로퍼티 중 하나 또는 두 프로퍼티를 모두 생략할 수 있으며, 이니셜라이저는 생략한 모든 프로퍼티에 대해 기본값을 사용합니다. 예를 들어 다음과 같습니다:

```swift
let zeroByTwo = Size(height: 2.0)
print(zeroByTwo.width, zeroByTwo.height)
// Prints "0.0 2.0"

let zeroByZero = Size()
print(zeroByZero.width, zeroByZero.height)
// Prints "0.0 0.0"
```
