## *Property Observers : 프로퍼티 옵저버*

*Property observers observe and respond to changes in a property’s value. Property observers are called every time a property’s value is set, even if the new value is the same as the property’s current value.*

프로퍼티 옵저버는 프로퍼티 값의 변화를 관찰하고 이에 대응합니다. 새 값이 프로퍼티의 현재 값과 동일한 경우에도 프로퍼티의 값이 설정될 때마다 프로퍼티 옵저버가 호출됩니다. 

*You can add property observers in the following places:*

다음 위치에 프로퍼티 옵저버를 추가할 수 있습니다:

- *Stored properties that you define*

        사용자 정의 저장 프로퍼티

- *Stored properties that you inherit*
  
  상속하는 저장 프로퍼티

- *Computed properties that you inherit*
  
  상속하는 연산 프로퍼티

*For an inherited property, you add a property observer by overriding that property in a subclass. For a computed property that you define, use the property’s setter to observe and respond to value changes, instead of trying to create an observer. Overriding properties is described in [Overriding](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html#ID196).*

상속된 프로퍼티의 경우 하위 클래스에서 해당 프로퍼티를 재정의하여 프로퍼티 옵저버를 추가합니다. 정의하는 연산 프로퍼티의 경우 옵저버를 만드는 대신 프로퍼티 세터를 사용하여 값 변경을 관찰하고 이에 대응합니다. 재정의 속성은 [링크]에 설명되어 있습니다.

*You have the option to define either or both of these observers on a property:*

프로퍼티에서 다음 옵저버 중 하나 또는 둘 모두를 정의할 수 있는 옵션이 있습니다.

- *`willSet` is called just before the value is stored.*
  
  `willSet`은 값이 저장되기 직전에 호출됩니다.

- *`didSet` is called immediately after the new value is stored.*
  
  `didSet`은 새 값이 저장된 직후에 호출됩니다.

*If you implement a `willSet` observer, it’s passed the new property value as a constant parameter. You can specify a name for this parameter as part of your `willSet` implementation. If you don’t write the parameter name and parentheses within your implementation, the parameter is made available with a default parameter name of `newValue`.*

`willSet` 옵저버를 구현하면 새 프로퍼티 값이 상수 매개 변수로 전달됩니다. `willSet` 구현의 일부로 이 매개 변수의 이름을 지정할 수 있습니다. 구현 내에서 매개 변수 이름과 괄호를 작성하지 않으면 매개 변수는 `newValue`의 기본 매개 변수 이름으로 사용할 수 있습니다.*

*Similarly, if you implement a `didSet` observer, it’s passed a constant parameter containing the old property value. You can name the parameter or use the default parameter name of `oldValue`. If you assign a value to a property within its own `didSet` observer, the new value that you assign replaces the one that was just set.*

이와 유사하게 `didSet` 옵저버를 구현하면 이전 프로퍼티 값을 포함하는 상수 매개 변수가 전달됩니다. 매개 변수의 이름을 지정하거나 기본 매개 변수 이름인 `oldValue`를 사용할 수 있습니다. 자체 `didSet` 옵저버 내의 속성에 값을 할당하면 방금 설정한 값이 새 값으로 바뀝니다.

> *NOTE*
> 
> *The `willSet` and `didSet` observers of superclass properties are called when a property is set in a subclass initializer, after the superclass initializer has been called. They aren’t called while a class is setting its own properties, before the superclass initializer has been called.*
> 
> *For more information about initializer delegation, see [Initializer Delegation for Value Types](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID215) and [Initializer Delegation for Class Types](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID219).*
> 
> 슈퍼클래스 프로퍼티의 `willSet` 및 `didSet` 옵저버는 슈퍼클래스 이니셜라이저가 호출된 후 서브클래스 이니셜라이저에 프로퍼티가 설정되면 호출됩니다. 클래스가 자체 프로퍼티를 설정하는 동안에는 슈퍼 클래스 이니셜라이저가 호출되기 전에 호출되지 않습니다. 이니셜라이저 위임에 대한 자세한 내용은 [링크] 및 [링크]를 참조하세요.

*Here’s an example of `willSet` and `didSet` in action. The example below defines a new class called `StepCounter`, which tracks the total number of steps that a person takes while walking. This class might be used with input data from a pedometer or other step counter to keep track of a person’s exercise during their daily routine.*

여기 `willSet`와 `didSet`의 동작 예가 있습니다. 아래 예제는 사람이 걷는 동안 걷는 총 걸음 수를 추적하는 `StepCounter`라는 새로운 클래스를 정의합니다. 이 클래스는 일상적인 작업 중 한 사람의 운동을 추적하기 위해 만보계 또는 다른 단계 카운터의 입력 데이터와 함께 사용될 수 있습니다.

```swift
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
```

*The `StepCounter` class declares a `totalSteps` property of type `Int`. This is a stored property with `willSet` and `didSet` observers.*

`StepCounter` 클래스는 타입이 `Int`인 `totalStep` 프로퍼티를 선언합니다. 이것은 `willSet` 및 `didSet` 옵저버가 있는 저장프로퍼티입니다.

*The `willSet` and `didSet` observers for `totalSteps` are called whenever the property is assigned a new value. This is true even if the new value is the same as the current value.*

`totalSteps`에 대한 `willSet` 및 `didSet` 옵저버는 프로퍼티에 새 값이 할당될 때마다 호출됩니다. 이는 새 값이 현재 값과 동일한 경우에도 해당됩니다.

*This example’s `willSet` observer uses a custom parameter name of `newTotalSteps` for the upcoming new value. In this example, it simply prints out the value that’s about to be set.*

이 예의 `willSet` 옵저버는 다가오는 새 값에 대해 `newTotalSteps`의 사용자 지정 매개 변수 이름을 사용합니다. 이 예에서는 설정할 값을 출력하기만 하면 됩니다.

*The `didSet` observer is called after the value of `totalSteps` is updated. It compares the new value of `totalSteps` against the old value. If the total number of steps has increased, a message is printed to indicate how many new steps have been taken. The `didSet` observer doesn’t provide a custom parameter name for the old value, and the default name of `oldValue` is used instead.*

`didSet` 옵저버는 `totalSteps` 값이 업데이트된 후 호출됩니다. `totalStep`의 새 값을 이전 값과 비교합니다. 총 단계 수가 증가한 경우 새 단계를 수행한 횟수를 나타내는 메시지가 출력됩니다. `didSet` 옵저버는 이전 값에 대한 사용자 지정 매개 변수 이름을 제공하지 않으며 대신 기본 이름인 `oldValue`가 사용됩니다.

> *NOTE*
> 
> *If you pass a property that has observers to a function as an in-out parameter, the `willSet` and `didSet` observers are always called. This is because of the copy-in copy-out memory model for in-out parameters: The value is always written back to the property at the end of the function. For a detailed discussion of the behavior of in-out parameters, see [In-Out Parameters](https://docs.swift.org/swift-book/ReferenceManual/Declarations.html#ID545).*
> 
> 옵저버가 있는 프로퍼티를 함수에 인아웃 매개 변수로 전달하면 `willSet` 및 `didSet` 옵저버가 항상 호출됩니다. 이는 인아웃 매개 변수에 대한 copy-in copy-out 메모리 모델 때문입니다: 값은 항상 함수가 끝날 때 프로퍼티에 다시 기록됩니다. In-Out 파라미터의 동작에 대한 자세한 내용은 [링크]를 참조하십시오.


