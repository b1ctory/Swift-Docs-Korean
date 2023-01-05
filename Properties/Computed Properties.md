## *Computed Properties : 연산 프로퍼티*

*In addition to stored properties, classes, structures, and enumerations can define computed properties, which don’t actually store a value. Instead, they provide a getter and an optional setter to retrieve and set other properties and values indirectly.*

저장프로퍼티 외에도 클래스, 구조체 및 열거형은 실제로 값을 저장하지 않는 연산 프로퍼티를 정의할 수 있습니다. 대신 다른 프로퍼티와 값을 간접적으로 검색하고 설정할 수 있는 게터와 옵셔널 세터를 제공합니다.

```swift
struct Point {
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
                  size: Size(width: 10.0, height: 10.0))
let initialSquareCenter = square.center
// initialSquareCenter is at (5.0, 5.0)
square.center = Point(x: 15.0, y: 15.0)
print("square.origin is now at (\(square.origin.x), \(square.origin.y))")
// Prints "square.origin is now at (10.0, 10.0)"
```

*This example defines three structures for working with geometric shapes:*

이 예에서는 기하학적 도형 작업을 위한 세 가지 구조체를 정의합니다:

- *`Point` encapsulates the x- and y-coordinate of a point.*
  
  `Point`는 점의 x 좌표와 y 좌표를 캡슐화합니다.

- *`Size` encapsulates a `width` and a `height`.*
  
  `Size`는 `width`와 `height`를 캡슐화합니다.

- *`Rect` defines a rectangle by an origin point and a size.*
  
  `Rect`는 원점과 크기로 직사각형을 정의합니다.

*The `Rect` structure also provides a computed property called `center`. The current center position of a `Rect` can always be determined from its `origin` and `size`, and so you don’t need to store the center point as an explicit `Point` value. Instead, `Rect` defines a custom getter and setter for a computed variable called `center`, to enable you to work with the rectangle’s `center` as if it were a real stored property.*

`Rect` 구조체는 `center`라는 연산 프로퍼티도 제공합니다. `Rect`의 현재 중심 위치는 항상 `origin`과 `size`에서 결정할 수 있으므로 중심점을 명시적인 `Point` 값으로 저장할 필요가 없습니다. 대신 `Rect`는 `center`라는 연산 변수에 대한 사용자 지정 게터와 세터를 정의하여 직사각형의 `center`를 실제 저장프로퍼티처럼 작업할 수 있게 합니다.

*The example above creates a new `Rect` variable called `square`. The `square` variable is initialized with an origin point of `(0, 0)`, and a width and height of `10`. This square is represented by the light green square in the diagram below.*

위의 예제는 `square`라는 새로운 `Rect` 변수를 생성합니다. `square` 변수는 원점점`(0,0)`, 폭과 높이가 `10`으로 초기화됩니다. 이 사각형은 아래 다이어그램에서 연두색 사각형으로 표시됩니다.

*The `square` variable’s `center` property is then accessed through dot syntax (`square.center`), which causes the getter for `center` to be called, to retrieve the current property value. Rather than returning an existing value, the getter actually calculates and returns a new `Point` to represent the center of the square. As can be seen above, the getter correctly returns a center point of `(5, 5)`.*

그러면 `square` 변수의 `center` 속성은 도트 구문(`square.center`)을 통해 액세스되며, 이로 인해 `center`에 대한 게터가 호출되어 현재 프로퍼티 값을 검색합니다. 기존 값을 반환하는 대신, 실제로는 정사각형의 중심을 나타내는 새로운 `Point`를 계산하여 반환합니다. 위에서 볼 수 있듯이, 게터는 `(5,5)`의 중심점을 정확하게 반환합니다.*

*The `center` property is then set to a new value of `(15, 15)`, which moves the square up and to the right, to the new position shown by the dark green square in the diagram below. Setting the `center` property calls the setter for `center`, which modifies the `x` and `y` values of the stored `origin` property, and moves the square to its new position.*

`center`프로퍼티는 `(15, 15)`이라는 새 값으로 설정되어 사각형이 아래 그림의 짙은 녹색 사각형으로 표시된 새 위치로 이동합니다. `center` 속성을 설정하면 저장된 `origin` 프로퍼티의 `x`와 `y` 값을 수정하고 사각형을 새 위치로 이동하는 `center`에 대한 세터가 호출됩니다.

![](https://docs.swift.org/swift-book/_images/computedProperties_2x.png)

### *Shorthand Setter Declaration : 속기 세터 선언*

*If a computed property’s setter doesn’t define a name for the new value to be set, a default name of `newValue` is used. Here’s an alternative version of the `Rect` structure that takes advantage of this shorthand notation:*

연산 프로퍼티의 세터가 설정할 새 값의 이름을 정의하지 않으면 기본 이름인 `newValue`가 사용됩니다. 다음은 이 단축 표기법을 이용한 `Rect` 구조체의 대체 버전입니다:

```swift
struct AlternativeRect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }
    }
}
```

### *Shorthand Getter Declaration : 속기 게터 선언*

*If the entire body of a getter is a single expression, the getter implicitly returns that expression. Here’s an another version of the `Rect` structure that takes advantage of this shorthand notation and the shorthand notation for setters:*

게터의 전체 본문이 단일 표현식인 경우, 게터는 암시적으로 해당 표현식을 반환합니다. 다음은 이 속기 표기법과 세터의 속기 표기법을 활용하는 또 다른 버전의 `Rect` 구조입니다:

```swift
struct CompactRect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            Point(x: origin.x + (size.width / 2),
                  y: origin.y + (size.height / 2))
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }
    }
}
```

*Omitting the `return` from a getter follows the same rules as omitting `return` from a function, as described in [Functions With an Implicit Return](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID607).*

게터에서 `return`을 생략하는 것은 [링크]에서 설명한 것처럼 함수에서 `return`을 생략하는 것과 동일한 규칙을 따릅니다.

### *Read-Only Computed Properties : 읽기 전용 계산 프로퍼티*

*A computed property with a getter but no setter is known as a read-only computed property. A read-only computed property always returns a value, and can be accessed through dot syntax, but can’t be set to a different value.*

게터는 있지만 세터는 없는 연산프로퍼티를 읽기 전용 연산프로퍼티라고 합니다. 읽기 전용 연산 프로퍼티는 항상 값을 반환하며 도트 구문을 통해 액세스할 수 있지만 다른 값으로 설정할 수는 없습니다.

> *NOTE*
> 
> *You must declare computed properties—including read-only computed properties—as variable properties with the `var` keyword, because their value isn’t fixed. The `let` keyword is only used for constant properties, to indicate that their values can’t be changed once they’re set as part of instance initialization.*
> 
> 읽기 전용 계산 프로퍼티를 포함한 연산 프로퍼티는 값이 고정되지 않으므로 `var` 키워드를 사용하여 변수 프로퍼티로 선언해야 합니다. `let` 키워드는 인스턴스 초기화의 일부로 설정되면 값을 변경할 수 없음을 나타내기 위해 상수 프로퍼티에만 사용됩니다.

*You can simplify the declaration of a read-only computed property by removing the `get` keyword and its braces:*

`get` 키워드와 해당 괄호를 제거하여 읽기 전용 연산 프로퍼티 선언을 단순화할 수 있습니다:

```swift
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
        return width * height * depth
    }
}
let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
print("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
// Prints "the volume of fourByFiveByTwo is 40.0"
```

*This example defines a new structure called `Cuboid`, which represents a 3D rectangular box with `width`, `height`, and `depth` properties. This structure also has a read-only computed property called `volume`, which calculates and returns the current volume of the cuboid. It doesn’t make sense for `volume` to be settable, because it would be ambiguous as to which values of `width`, `height`, and `depth` should be used for a particular `volume` value*. Nonetheless, it’s useful for a `Cuboid` to provide a read-only computed property to enable external users to discover its current calculated volume.

이 예에서는 `Cuboid`라는 새로운 구조체를 정의합니다. 이 구조체는  `width`, `height`, 그리고 `depth` 프로퍼티를 가진 3D 직사각형 상자를 나타냅니다. 이 구조체는 또한 큐브의 현재 부피를 계산하고 반환하는 읽기 전용 계산 속성인 `volume`을 가지고 있습니다. `volume`을 설정하는 것은 의미가 없습니다. 특정 `volume` 값에  `width`, `height`, 그리고 `depth` 중 어떤 값을 사용해야 하는지 모호하기 때문입니다. 그럼에도 불구하고, `Cuboid`가 읽기 전용 연산 프로퍼티를 제공하여 외부 사용자가 현재 계산된 부피를 검색할 수 있도록 하는 것은 유용합니다.


