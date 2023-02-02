## *Actors*

*You can use tasks to break up your program into isolated, concurrent pieces. Tasks are isolated from each other, which is what makes it safe for them to run at the same time, but sometimes you need to share some information between tasks. Actors let you safely share information between concurrent code.*

작업을 사용하여 프로그램을 분리된 동시성 조각으로 분할할 수 있습니다. 작업은 서로 격리되어 있으므로 작업을 동시에 실행하는 것이 안전하지만 때로는 작업 간에 일부 정보를 공유해야 합니다. 액터를 사용하면 동시성 코드 간에 정보를 안전하게 공유할 수 있습니다.

*Like classes, actors are reference types, so the comparison of value types and reference types in [Classes Are Reference Types](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#ID89) applies to actors as well as classes. Unlike classes, actors allow only one task to access their mutable state at a time, which makes it safe for code in multiple tasks to interact with the same instance of an actor. For example, here’s an actor that records temperatures:*

클래스와 마찬가지로 액터도 레퍼런스 타입이므로 [링크]의 값 타입과 레퍼런스 타입의 비교는 클래스뿐만 아니라 클래스에도 적용됩니다. 클래스와 달리 액터는 한 번에 하나의 작업만 변경 가능한 상태에 액세스할 수 있으므로 여러 작업의 코드가 액터의 동일한 인스턴스와 상호 작용하는 것이 안전합니다. 예를 들어, 다음은 온도를 기록하는 액터입니다:

```swift
actor TemperatureLogger {
    let label: String
    var measurements: [Int]
    private(set) var max: Int

    init(label: String, measurement: Int) {
        self.label = label
        self.measurements = [measurement]
        self.max = measurement
    }
}
```

*You introduce an actor with the `actor` keyword, followed by its definition in a pair of braces. The `TemperatureLogger` actor has properties that other code outside the actor can access, and restricts the `max` property so only code inside the actor can update the maximum value.*

`actor` 키워드를 가진 액터를 소개하고 그 정의를 한 쌍의 괄호로 소개합니다. `TemperatureLogger` 액터는 액터 외부의 다른 코드가 액세스할 수 있는 프로퍼티를 가지고 있으며 `max` 프로퍼티를 제한하여 액터 내부의 코드만 최대값을 업데이트할 수 있습니다.

*You create an instance of an actor using the same initializer syntax as structures and classes. When you access a property or method of an actor, you use `await` to mark the potential suspension point. For example:*

구조체 및 클래스와 동일한 초기화 구문을 사용하여 액터의 인스턴스를 만듭니다. 액터의 프로퍼티나 메서드에 액세스할 때는 `await`을 사용하여 잠재적인 중단점을 표시합니다. 예를 들어:

```swift
let logger = TemperatureLogger(label: "Outdoors", measurement: 25)
print(await logger.max)
// Prints "25"
```

*In this example, accessing `logger.max` is a possible suspension point. Because the actor allows only one task at a time to access its mutable state, if code from another task is already interacting with the logger, this code suspends while it waits to access the property.*

이 예에서는 `logger.max`에 액세스하는 것이 서스펜션 포인트가 될 수 있습니다. 액터는 한 번에 하나의 태스크만 변경 가능한 상태에 액세스할 수 있도록 허용하므로 다른 작업의 코드가 이미 logger와 상호 작용하고 있는 경우 이 코드는 프로퍼티에 액세스하기 위해 기다리는 동안 일시 중단됩니다.

*In contrast, code that’s part of the actor doesn’t write `await` when accessing the actor’s properties. For example, here’s a method that updates a `TemperatureLogger` with a new temperature:*

반대로 액터의 일부인 코드는 액터의 프로퍼티에 접근할 때 `await`을 쓰지 않습니다. 예를 들어 `TemperatureLogger`를 새 온도로 업데이트하는 방법은 다음과 같습니다:

```swift
extension TemperatureLogger {
    func update(with measurement: Int) {
        measurements.append(measurement)
        if measurement > max {
            max = measurement
        }
    }
}
```

*The `update(with:)` method is already running on the actor, so it doesn’t mark its access to properties like `max` with `await`. This method also shows one of the reasons why actors allow only one task at a time to interact with their mutable state: Some updates to an actor’s state temporarily break invariants. The `TemperatureLogger` actor keeps track of a list of temperatures and a maximum temperature, and it updates the maximum temperature when you record a new measurement. In the middle of an update, after appending the new measurement but before updating `max`, the temperature logger is in a temporary inconsistent state. Preventing multiple tasks from interacting with the same instance simultaneously prevents problems like the following sequence of events:*

`update(with:)` 메서드가 이미 액터에서 실행되고 있으므로 `max`와 같은 프로퍼티에 대한 액세스를 `await`과 함께 표시하지 않습니다. 이 메서드는 또한 액터들이 한 번에 하나의 작업만 그들의 가변 상태와 상호작용하도록 허용하는 이유 중 하나를 보여줍니다: 액터의 상태에 대한 일부 업데이트는 일시적으로 불변을 깨트립니다. `TemperatureLogger` 액터는 온도 목록과 최대 온도를 추적하고 새 측정값을 기록하면 최대 온도를 업데이트합니다. 업데이트 도중에 새 측정값을 추가한 후 `max`를 업데이트하기 전에 온도 logger가 일시적으로 일관성이 없는 상태가 됩니다. 여러 태스크가 동일한 인스턴스와 동시에 상호 작용하지 못하도록 하면 다음의 이벤트에 대한 시퀀스 같은 문제가 발생하지 않습니다:

1. *Your code calls the `update(with:)` method. It updates the `measurements` array first.*
   
   당신의 코드는 `update(with:)` 메서드를 호출합니다. 먼저 `measurements` 배열을 업데이트합니다.

2. *Before your code can update `max`, code elsewhere reads the maximum value and the array of temperatures.*
   
   코드가 `max`를 업데이트하기 전에 다른 곳에서 코드가 최대값과 온도 배열을 읽습니다.

3. *Your code finishes its update by changing `max`.*
   
   코드가 `max`를 변경하여 업데이트를 마칩니다.

*In this case, the code running elsewhere would read incorrect information because its access to the actor was interleaved in the middle of the call to `update(with:)` while the data was temporarily invalid. You can prevent this problem when using Swift actors because they only allow one operation on their state at a time, and because that code can be interrupted only in places where `await` marks a suspension point. Because `update(with:)` doesn’t contain any suspension points, no other code can access the data in the middle of an update.*

이 경우, 데이터가 일시적으로 유효하지 않은 상태에서 액터에 대한 접근 권한이 호출 도중 인터리브되었기 때문에 다른 곳에서 실행되는 코드가 잘못된 정보를 읽을 수 있습니다. Swift 액터를 사용하면 이 문제를 방지할 수 있습니다. 왜냐하면 그들은 한 번에 자신의 상태에 대한 작업을 한 번에 한 번만 허용하고, 그 코드는 `await`가 중단점을 표시하는 곳에서만 중단될 수 있기 때문입니다. `update(with:)`에는 중단점이 없기 때문에 업데이트 도중 다른 코드가 데이터에 액세스할 수 없습니다.

*If you try to access those properties from outside the actor, like you would with an instance of a class, you’ll get a compile-time error. For example:*

클래스 인스턴스에서와 같이 액터 외부에서 이러한 속성에 액세스하려고 하면 컴파일 타임 오류가 발생합니다. 예를 들어 다음과 같습니다:

```swift
print(logger.max) // Error
```

*Accessing `logger.max` without writing `await` fails because the properties of an actor are part of that actor’s isolated local state. Swift guarantees that only code inside an actor can access the actor’s local state. This guarantee is known as actor isolation.*

`await`을 쓰지 않고 `logger.max`에 액세스하는 것은 액터의 프로퍼티가 해당 배우의 고립된 로컬 상태의 일부이기 때문에 실패합니다. Swift는 액터 내부의 코드만 배우의 로컬 상태에 액세스할 수 있음을 보장합니다. 이 보증을 액터 격리라고 합니다.
