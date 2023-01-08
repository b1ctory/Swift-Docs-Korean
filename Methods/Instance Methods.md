## *Instance Methods : 인스턴스 메서드*

*Instance methods are functions that belong to instances of a particular class, structure, or enumeration. They support the functionality of those instances, either by providing ways to access and modify instance properties, or by providing functionality related to the instance’s purpose. Instance methods have exactly the same syntax as functions, as described in [Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html).*

인스턴스 메소드는 특정 클래스, 구조체 또는 열거형의 인스턴스에 속하는 함수입니다. 인스턴스 프로퍼티에 액세스하고 수정하는 방법을 제공하거나 인스턴스의 목적과 관련된 기능을 제공하여 이러한 인스턴스의 기능을 지원합니다. 인스턴스 메서드는 [링크]에 설명된 대로 함수와 구문이 동일합니다.

*You write an instance method within the opening and closing braces of the type it belongs to. An instance method has implicit access to all other instance methods and properties of that type. An instance method can be called only on a specific instance of the type it belongs to. It can’t be called in isolation without an existing instance.*

인스턴스 메서드는 해당 메서드가 속한 타입의 여닫이 괄호 안에 작성합니다. 인스턴스 메서드는 해당 유형의 다른 모든 인스턴스 메서드 및 프로퍼티에 암시적으로 액세스할 수 있습니다. 인스턴스 메서드는 해당 메서드가 속한 타입의 특정 인스턴스에서만 호출할 수 있습니다. 기존 인스턴스 없이는 분리하여 호출할 수 없습니다.

*Here’s an example that defines a simple `Counter` class, which can be used to count the number of times an action occurs:*

다음은 단순한 `Counter` 클래스를 정의하는 예입니다. 이 클래스를 사용하여 작업이 발생하는 횟수를 계산할 수 있습니다:

```swift
class Counter {
    var count = 0
    func increment() {
        count += 1
    }
    func increment(by amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}
```

*The `Counter` class defines three instance methods:*

`Counter` 클래스는 세 가지 인스턴스 메서드를 정의합니다:

- *`increment()` increments the counter by `1`.*
  
  `increment()` 는 카운터를 `1`만큼 증가시킵니다.

- *`increment(by: Int)` increments the counter by a specified integer amount.*
  
  `increment(by: Int)`는 카운터를 지정된 정수만큼 증가시킵니다.

- *`reset()` resets the counter to zero.*
  
  `reset()`은 카운터를 0으로 재설정합니다.

*The `Counter` class also declares a variable property, `count`, to keep track of the current counter value.*

`Counter` 클래스는 또한 변수 속성 `count`를 선언하여 현재 카운터 값을 추적합니다.

*You call instance methods with the same dot syntax as properties:*

프로퍼티와 동일한 점 구문을 사용하여 인스턴스 메서드를 호출합니다:

```swift
let counter = Counter()
// the initial counter value is 0
counter.increment()
// the counter's value is now 1
counter.increment(by: 5)
// the counter's value is now 6
counter.reset()
// the counter's value is now 0
```

*Function parameters can have both a name (for use within the function’s body) and an argument label (for use when calling the function), as described in [Function Argument Labels and Parameter Names](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID166). The same is true for method parameters, because methods are just functions that are associated with a type.*

[링크]에 설명된 대로 함수 매개 변수에는 이름(함수 본문 내에서 사용)과 인수 레이블(함수 호출 시 사용)이 모두 포함될 수 있습니다. 메서드는 타입과과 연관된 함수일 뿐이므로 메서드 매개 변수도 마찬가지입니다.

### *The self Property : self 프로퍼티*

*Every instance of a type has an implicit property called `self`, which is exactly equivalent to the instance itself. You use the `self` property to refer to the current instance within its own instance methods.*

타입의 모든 인스턴스에는 인스턴스 자체와 정확히 동일한 `self`라는 암시적 프로퍼티가 있습니다. 자체 인스턴스 메서드 내에서 현재 인스턴스를 참조하려면 `self` 프로퍼티를 사용합니다.

*The `increment()` method in the example above could have been written like this:*

위의 예에서 `increment()` 메서드는 다음과 같이 작성될 수 있습니다:

```swift
func increment() {
    self.count += 1
}
```

*In practice, you don’t need to write `self` in your code very often. If you don’t explicitly write `self`, Swift assumes that you are referring to a property or method of the current instance whenever you use a known property or method name within a method. This assumption is demonstrated by the use of `count` (rather than `self.count`) inside the three instance methods for `Counter`.*

실제로 코드에 자주 `self`를 쓸 필요는 없습니다. `self`를 명시적으로 쓰지 않으면 Swift는 메서드 내에서 알려진 프로퍼티나 메서드 이름을 사용할 때마다 현재 인스턴스의 프로퍼티나 메서드를 참조하는 것으로 가정합니다. 이 가정은 `Counter`에 대한 세 가지 인스턴스 메소드 내에서 (`self.count`가 아닌) `count`를 사용함으로써 입증됩니다.

*The main exception to this rule occurs when a parameter name for an instance method has the same name as a property of that instance. In this situation, the parameter name takes precedence, and it becomes necessary to refer to the property in a more qualified way. You use the `self` property to distinguish between the parameter name and the property name.*

이 규칙의 기본 예외는 인스턴스 메서드의 매개 변수 이름이 해당 인스턴스의 프로퍼티 이름과 같은 경우에 발생합니다. 이 경우 매개 변수 이름이 우선하므로 보다 정규화된 방법으로 프로퍼티를 참조해야 합니다. `self` 프로퍼티를 사용하여 매개 변수 이름과 프로퍼티 이름을 구분할 수 있습니다.

*Here, `self` disambiguates between a method parameter called `x` and an instance property that’s also called `x`:*

여기서 `self`는 `x`라는 메서드 매개 변수와 `x`라고도 하는 인스턴스 프로퍼티를 명확하게 구분합니다:

```swift
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOf(x: Double) -> Bool {
        return self.x > x
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOf(x: 1.0) {
    print("This point is to the right of the line where x == 1.0")
}
// Prints "This point is to the right of the line where x == 1.0"
```

*Without the `self` prefix, Swift would assume that both uses of `x` referred to the method parameter called `x`.*

`self` 접두사가 없으면 Swift는 `x`의 두 가지 사용 모두 `x`라는 메서드 매개 변수를 참조한다고 가정합니다.

### *Modifying Value Types from Within Instance Methods : 인스턴스 메소드 내에서 값 타입 수정*

*Structures and enumerations are value types. By default, the properties of a value type can’t be modified from within its instance methods.*

구조체 및 열거형은 값 타입입니다. 기본적으로 값 타입의 프로퍼티는 해당 인스턴스 메서드 내에서 수정할 수 없습니다.

*However, if you need to modify the properties of your structure or enumeration within a particular method, you can opt in to mutating behavior for that method. The method can then mutate (that is, change) its properties from within the method, and any changes that it makes are written back to the original structure when the method ends. The method can also assign a completely new instance to its implicit `self` property, and this new instance will replace the existing one when the method ends.*

그러나 특정 메서드 내에서 구조체 또는 열거형의 프로퍼티를 수정해야 하는 경우 해당 메서드에 대한 변환 동작을 선택할 수 있습니다. 그런 다음 메소드는 메소드 내에서 프로퍼티를 변환(즉, 변경)할 수 있으며 메소드가 종료되면 변경 내용이 원래 구조로 다시 기록됩니다. 또한 이 방법은 암시적인 `self` 프로퍼티에 완전히 새로운 인스턴스를 할당할 수 있으며, 이 새로운 인스턴스는 메서드가 끝나면 기존 인스턴스를 대체합니다.

*You can opt in to this behavior by placing the `mutating` keyword before the `func` keyword for that method:*

`mutating`키워드를 해당 메서드의 `func` 키워드 앞에 배치하여 이 동작을 선택할 수 있습니다:

```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
// Prints "The point is now at (3.0, 4.0)"
```

*The `Point` structure above defines a mutating `moveBy(x:y:)` method, which moves a `Point` instance by a certain amount. Instead of returning a new point, this method actually modifies the point on which it’s called. The `mutating` keyword is added to its definition to enable it to modify its properties.*

위의 `Point` 구조체는 `Point` 인스턴스를 일정량 이동시키는 mutating `moveBy(x:y:)` 메소드를 정의합니다. 이 메서드는 새 점을 반환하는 대신 실제로 호출된 점을 수정합니다. `mutating` 키워드는 프로퍼티를 수정할 수 있도록 정의에 추가됩니다.

*Note that you can’t call a mutating method on a constant of structure type, because its properties can’t be changed, even if they’re variable properties, as described in [Stored Properties of Constant Structure Instances](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID256):*

[링크]에 설명된 대로 구조체 타입의 상수에 대한 mutating 메서드를 호출할 수 없습니다. 그 프로퍼티는 변수 프로퍼티인 경우에도 변경할 수 없습니다.

```swift
let fixedPoint = Point(x: 3.0, y: 3.0)
fixedPoint.moveBy(x: 2.0, y: 3.0)
// this will report an error
```

### *Assigning to self Within a Mutating Method : Mutating 메서드 내에서 self에 할당*

*Mutating methods can assign an entirely new instance to the implicit `self` property. The `Point` example shown above could have been written in the following way instead:*

mutating 메서드는 암시적인 `self` 프로퍼티에 완전히 새로운 인스턴스를 할당할 수 있습니다. 위에 표시된 `Point` 예제는 대신 다음과 같은 방식으로 작성될 수 있습니다:

```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}
```

*This version of the mutating `moveBy(x:y:)` method creates a new structure whose `x` and `y` values are set to the target location. The end result of calling this alternative version of the method will be exactly the same as for calling the earlier version.*

이 mutating `moveBy(x:y:)` 메서드의 버전은 `x`와 `y` 값이 목표 위치로 설정된 새로운 구조를 만듭니다. 이 메서드의 대체 버전을 호출한 최종 결과는 이전 버전을 호출한 경우와 정확히 같습니다.

*Mutating methods for enumerations can set the implicit `self` parameter to be a different case from the same enumeration:*

열거형에 대한 mutating 메서드는 암시적 `self` 매개 변수를 동일한 열거형과 다른 경우로 설정할 수 있습니다:

```swift
enum TriStateSwitch {
    case off, low, high
    mutating func next() {
        switch self {
        case .off:
            self = .low
        case .low:
            self = .high
        case .high:
            self = .off
        }
    }
}
var ovenLight = TriStateSwitch.low
ovenLight.next()
// ovenLight is now equal to .high
ovenLight.next()
// ovenLight is now equal to .off
```

*This example defines an enumeration for a three-state switch. The switch cycles between three different power states (`off`, `low` and `high`) every time its `next()` method is called.*

이 예에서는 3-상태 스위치문에 대한 열거형을 정의합니다. 스위치문은 `next()` 메서드가 호출될 때마다 세 가지 다른 전원 상태(`off`, `low` 및 `high`) 사이를 순환합니다.


