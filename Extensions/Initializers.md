## *Initializers : 이니셜라이저*

*Extensions can add new initializers to existing types. This enables you to extend other types to accept your own custom types as initializer parameters, or to provide additional initialization options that were not included as part of the type’s original implementation.*

확장은 기존 타입에 새 이니셜라이저를 추가할 수 있습니다. 이렇게 하면 다른 타입을 확장하여 사용자 정의 타입을 초기화 매개 변수로 사용하거나 타입의 원래 구현에 포함되지 않은 추가 초기화 옵션을 제공할 수 있습니다.

*Extensions can add new convenience initializers to a class, but they can’t add new designated initializers or deinitializers to a class. Designated initializers and deinitializers must always be provided by the original class implementation.*

확장 기능은 클래스에 새 단축 이니셜라이저를 추가할 수 있지만 지정된 새 초기화 프로그램이나 초기화 해제 프로그램을 클래스에 추가할 수 없습니다. 지정된 이니셜라이저 및 디이니셜라이저는 항상 원래 클래스 구현에서 제공해야 합니다.

*If you use an extension to add an initializer to a value type that provides default values for all of its stored properties and doesn’t define any custom initializers, you can call the default initializer and memberwise initializer for that value type from within your extension’s initializer. This wouldn’t be the case if you had written the initializer as part of the value type’s original implementation, as described in [Initializer Delegation for Value Types](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID215).*

확장을 사용하여 저장된 모든 프로퍼티에 대한 기본값을 제공하는 값 타입에 이니셜라이저를 추가하고 사용자 정의 이니셜라이저를 정의하지 않는 경우 확장의 이니셜라이저 내에서 해당 값 타입에 대한 기본 이니셜라이저 및 멤버별 이니셜라이저를 호출할 수 있습니다.[링크]에서 설명한 대로 값 타입의 원래 구현의 일부로 이니셜라이저를 작성한 경우에는 그렇지 않습니다.

*If you use an extension to add an initializer to a structure that was declared in another module, the new initializer can’t access `self` until it calls an initializer from the defining module.*

확장자를 사용하여 다른 모듈에서 선언된 구조에 이니셜라이저를 추가하면 새 이니셜라이저가 정의 모듈에서 이니셜라이저를 호출할 때까지 `self`에 액세스할 수 없습니다.

*The example below defines a custom `Rect` structure to represent a geometric rectangle. The example also defines two supporting structures called `Size` and `Point`, both of which provide default values of `0.0` for all of their properties:*

아래 예제는 기하학적 직사각형을 나타내는 사용자 정의 `Rect` 구조체를 정의합니다. 이 예는 또한 `Size`와 `Point`라는 두 가지 지원 구조체를 정의하며, 두 구조체 모두 모든 프로퍼티에 대해 기본값인 `0.0`을 제공합니다

```swift
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
}
```

*Because the `Rect` structure provides default values for all of its properties, it receives a default initializer and a memberwise initializer automatically, as described in [Default Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID213). These initializers can be used to create new `Rect` instances:*

`Rect` 구조체는 모든 속성에 대한 기본값을 제공하므로 [링크]에 설명된 대로 기본 Initializer 및 멤버별 Initializer를 자동으로 수신합니다. 이러한 이니셜라이저를 사용하여 새로운 `Rect` 인스턴스를 만들 수 있습니다:

```swift
let defaultRect = Rect()
let memberwiseRect = Rect(origin: Point(x: 2.0, y: 2.0),
   size: Size(width: 5.0, height: 5.0))
```

*You can extend the `Rect` structure to provide an additional initializer that takes a specific center point and size:*

`Rect`구조체를 확장하여 특정 중심점과 크기를 취하는 추가 이니셜라이저를 제공할 수 있습니다

```swift
extension Rect {
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}
```

*This new initializer starts by calculating an appropriate origin point based on the provided `center` point and `size` value. The initializer then calls the structure’s automatic memberwise initializer `init(origin:size:)`, which stores the new origin and size values in the appropriate properties:*

이 새로운 이니셜라이저는 제공된 `center` 점과 `size` 값을 기반으로 적절한 원시 지점을 계산하는 것으로 시작합니다. 그런 다음 이니셜라이저는 구조의 자동 멤버와이즈 이니셜라이저 `init(origin: size:)`를 호출하여 적절한 프로퍼티에 에 새 오리진 및 크기 값을 저장합니다:

```swift
let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
                      size: Size(width: 3.0, height: 3.0))
// centerRect's origin is (2.5, 2.5) and its size is (3.0, 3.0)
```

> *NOTE*
> 
> *If you provide a new initializer with an extension, you are still responsible for making sure that each instance is fully initialized once the initializer completes.*
> 
> 새 이니셜라이저에 확장 기능을 제공하는 경우에도 이니셜라이저가 완료된 후 각 인스턴스가 완전히 초기화되도록 해야 합니다.


