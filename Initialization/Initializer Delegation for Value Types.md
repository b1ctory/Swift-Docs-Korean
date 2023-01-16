## *Initializer Delegation for Value Types :  타입에 대한 초기화 위임*

*Initializers can call other initializers to perform part of an instance’s initialization. This process, known as initializer delegation, avoids duplicating code across multiple initializers.*

이니셜라이저는 다른 이니셜라이저를 호출하여 인스턴스 초기화의 일부를 수행할 수 있습니다. 이 프로세스를 초기화 위임이라고 하며, 여러 이니셜라이저 간에 코드가 중복되지 않도록 합니다.

*The rules for how initializer delegation works, and for what forms of delegation are allowed, are different for value types and class types. Value types (structures and enumerations) don’t support inheritance, and so their initializer delegation process is relatively simple, because they can only delegate to another initializer that they provide themselves. Classes, however, can inherit from other classes, as described in [Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html). This means that classes have additional responsibilities for ensuring that all stored properties they inherit are assigned a suitable value during initialization. These responsibilities are described in [Class Inheritance and Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID216) below.*

초기화 위임의 작동 방식과 허용되는 위임 형식에 대한 규칙은 값 타입과 클래스 타입에 따라 다릅니다. 값 타입(구조체 및 열거형)은 상속을 지원하지 않으므로 초기화 위임 프로세스가 상대적으로 간단합니다. 이는 자신이 직접 제공하는 다른 이니셜라이저에만 위임할 수 있기 때문입니다. 그러나 클래스는 [링크]에서 설명한 대로 다른 클래스에서 상속할 수 있습니다. 즉, 클래스는 초기화 중에 상속하는 모든 저장 프로퍼티에 적절한 값이 할당되도록 하는 추가적인 책임이 있습니다. 이러한 책임은 아래 [링크]에 설명되어 있습니다.*

*For value types, you use `self.init` to refer to other initializers from the same value type when writing your own custom initializers. You can call `self.init` only from within an initializer.*

값 타입의 경우 사용자 정의 이니셜라이저를 작성할 때 동일한 값 타입의 다른 이니셜라이저를 참조하려면 `self.init`를 사용합니다. 이니셜라이저 내에서만 `self.init`를 호출할 수 있습니다.

*Note that if you define a custom initializer for a value type, you will no longer have access to the default initializer (or the memberwise initializer, if it’s a structure) for that type. This constraint prevents a situation in which additional essential setup provided in a more complex initializer is accidentally circumvented by someone using one of the automatic initializers.*

값 타입에 대한 사용자 정의 이니셜라이저를 정의하면 해당 타입에 대한 기본 이니셜라이저(또는 구조체인 경우 멤버별 이니셜라이저)에 더 이상 액세스할 수 없습니다. 이러한 제약 조건은 자동 이니셜라이저 중 하나를 사용하는 사용자에 의해 보다 복잡한 이니셜라이저에서 제공되는 추가적인 필수 설정이 실수로 우회되는 상황을 방지합니다.

> *NOTE*
> 
> *If you want your custom value type to be initializable with the default initializer and memberwise initializer, and also with your own custom initializers, write your custom initializers in an extension rather than as part of the value type’s original implementation. For more information, see [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html).*
> 
> 사용자 정의 값 타입을 기본 이니셜라이저 및 멤버별 이니셜라이저를 사용하여 초기화할 수 있도록 하고 사용자 정의 값 타입을 원래 구현의 일부가 아닌 익스텐션으로 작성하십시오. 자세한 내용은 [링크]를 참조하십시오.

*The following example defines a custom `Rect` structure to represent a geometric rectangle. The example requires two supporting structures called `Size` and `Point`, both of which provide default values of `0.0` for all of their properties:*

다음 예제는 기하학적 직사각형을 나타내는 사용자 정의 `Rect` 구조체를 정의합니다. 이 예에서는 `Size`와 `Point`라는 두 가지 지원 구조체가 필요하며, 두 구조체 모두 모든 프로퍼티에 대해 기본값인 `0.0`을 제공합니다:

```swift
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}
```

*You can initialize the `Rect` structure below in one of three ways—by using its default zero-initialized `origin` and `size` property values, by providing a specific origin point and size, or by providing a specific center point and size. These initialization options are represented by three custom initializers that are part of the `Rect` structure’s definition:*

기본값 0으로 초기화된 `origin` 및 `size` 프로퍼티 값을 사용하거나, 특정 원점 점과 크기를 제공하거나, 특정 중심점과 크기를 제공하여 아래의 `Rect` 구조체를 초기화할 수 있습니다. 이러한 초기화 옵션은 `Rect` 구조체 정의의 일부인 세 가지 사용자 정의 이니셜라이저로 표시됩니다:

```swift
struct Rect {
    var origin = Point()
    var size = Size()
    init() {}
    init(origin: Point, size: Size) {
        self.origin = origin
        self.size = size
    }
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}
```

*The first `Rect` initializer, `init()`, is functionally the same as the default initializer that the structure would have received if it didn’t have its own custom initializers. This initializer has an empty body, represented by an empty pair of curly braces `{}`. Calling this initializer returns a `Rect` instance whose `origin` and `size` properties are both initialized with the default values of `Point(x: 0.0, y: 0.0)` and `Size(width: 0.0, height: 0.0)` from their property definitions:*

첫 번째 `Rect` 이니셜라이저인 `init()`은 구조체에 자체 사용자 지정 이니셜라이저가 없었다면 받았을 기본 이니셜라이저와 기능적으로 동일합니다. 이 이니셜라이저는 빈 본문 을 가지고 있으며, 빈 한 쌍의 곱슬 괄호 `{}`로 표시됩니다. 이 이니셜라이저를 호출하면 `origin` 및 `size` 프로퍼티가 프로퍼티 정의에서 기본값인 `Point(x: 0.0, y: 0.0)`와 `Size(width: 0.0, height: 0.0)`로 모두 초기화된 `Rect` 인스턴스가 반환됩니다:

```swift
let basicRect = Rect()
// basicRect's origin is (0.0, 0.0) and its size is (0.0, 0.0)
```

*The second `Rect` initializer, `init(origin:size:)`, is functionally the same as the memberwise initializer that the structure would have received if it didn’t have its own custom initializers. This initializer simply assigns the `origin` and `size` argument values to the appropriate stored properties:*

두 번째 `Rect` 이니셜라이저인 `init(origin: size:)`는 구조체에 자체 사용자 지정 이니셜라이저가 없었다면 받았을 멤버별 이니셜라이저와 기능적으로 동일합니다. 이 이니셜라이저는 단순히 `origin`과 `size`인수 값을 적절한 저장 프로퍼티에 할당합니다:

```swift
let originRect = Rect(origin: Point(x: 2.0, y: 2.0),
                      size: Size(width: 5.0, height: 5.0))
// originRect's origin is (2.0, 2.0) and its size is (5.0, 5.0)
```

*The third `Rect` initializer, `init(center:size:)`, is slightly more complex. It starts by calculating an appropriate origin point based on a `center` point and a `size` value. It then calls (or delegates) to the `init(origin:size:)` initializer, which stores the new origin and size values in the appropriate properties:*

세 번째 `Rect` 이니셜라이저인 `init(중앙:크기:)`는 약간 더 복잡합니다. 우선 `center` 지점과 `size` 값을 기준으로 적절한 원점을 계산합니다. 그런 다음 새 원점 및 크기 값을 적절한 프로퍼티에 저장하는 `init(origin:size:)` 이니셜라이저로 호출(또는 위임)합니다:

```swift
let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
                      size: Size(width: 3.0, height: 3.0))
// centerRect's origin is (2.5, 2.5) and its size is (3.0, 3.0)
```

*The `init(center:size:)` initializer could have assigned the new values of `origin` and `size` to the appropriate properties itself. However, it’s more convenient (and clearer in intent) for the `init(center:size:)` initializer to take advantage of an existing initializer that already provides exactly that functionality.*

`init(center:size:)` 이니셜라이저는 `origin`과 `size`의 새 값을 적절한 프로퍼티 자체에 할당했을 수 있습니다. 그러나 `init(center:size:)` 이니셜라이저가 이미 정확하게 해당 기능을 제공하는 기존 이니셜라이저를 활용하는 것이 더 편리합니다.

> *NOTE*
> 
> *For an alternative way to write this example without defining the `init()` and `init(origin:size:)` initializers yourself, see [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html).*
> 
> `init()` 및 `init(size:)` 이니셜라이저를 직접 정의하지 않고 이 예제를 작성하는 다른 방법은 [링크]를 참조하십시오.
