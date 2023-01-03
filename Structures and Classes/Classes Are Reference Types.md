## *Classes Are Reference Types : 클래스는 참조 타입*

*Unlike value types, reference types are not copied when they’re assigned to a variable or constant, or when they’re passed to a function. Rather than a copy, a reference to the same existing instance is used.*

값 타입과 달리 참조 타입은 변수 혹은 상수에 할당되거나 함수에 전달될 때 복사되지 않습니다. 복사본 대신 동일한 기존 인스턴스에 대한 참조가 사용됩니다.

*Here’s an example, using the `VideoMode` class defined above:*

위에 정의된 `VideoMode` 클래스를 사용하는 예는 다음과 같습니다.

```swift
let tenEighty = VideoMode()
tenEighty.resolution = hd
tenEighty.interlaced = true
tenEighty.name = "1080i"
tenEighty.frameRate = 25.0
```

*This example declares a new constant called `tenEighty` and sets it to refer to a new instance of the `VideoMode` class. The video mode is assigned a copy of the HD resolution of `1920` by `1080` from before. It’s set to be interlaced, its name is set to `"1080i"`, and its frame rate is set to `25.0` frames per second.*

이 예시에서는 `tenEighty`라는 새 상수를 선언하고 `VideoMode` 클래스의 새 인스턴스를 참조하도록 설정합니다. 비디오 모드에는 이전의 HD 해상도인 `1920`과 `1080`의 복사본이 할당됩니다. 인터레이스로 설정되고 이름은 `1080i` 로 설정되며 프레임 속도는 초당 `25.0` 프레임으로 설정됩니다.

*Next, `tenEighty` is assigned to a new constant, called `alsoTenEighty`, and the frame rate of `alsoTenEighty` is modified:*

다음으로 `tenEighty`는 `alsoTenEighty`라고 하는 새로운 상수에 할당되고 `alsoTenEighty`의 프레임률이 수정됩니다.

```swift
let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0
```

*Because classes are reference types, `tenEighty` and `alsoTenEighty` actually both refer to the same `VideoMode` instance. Effectively, they’re just two different names for the same single instance, as shown in the figure below:*

클래스는 참조 타입이므로 `tenEighty`와 `alsoTenEighty`는 모두 동일한 `VideoMode` 인스턴스를 참조합니다. 효과적으로 아래 그림과 같이 동일한 단일 인스턴스에 대해 두 개의 서로 다른 이름일 뿐입니다:

*![](https://docs.swift.org/swift-book/_images/sharedStateClass_2x.png)*

*Checking the `frameRate` property of `tenEighty` shows that it correctly reports the new frame rate of `30.0` from the underlying `VideoMode` instance:*

`tenEighty`의 `frameRate` 속성을 확인하면 기본 `VideoMode`인스턴스에서 `30.0`의 새 프레임률을 올바르게 보고하는 것으로 나타납니다.

```swift
print("The frameRate property of tenEighty is now \(tenEighty.frameRate)")
// Prints "The frameRate property of tenEighty is now 30.0"
```

*This example also shows how reference types can be harder to reason about. If `tenEighty` and `alsoTenEighty` were far apart in your program’s code, it could be difficult to find all the ways that the video mode is changed. Wherever you use `tenEighty`, you also have to think about the code that uses `alsoTenEighty`, and vice versa. In contrast, value types are easier to reason about because all of the code that interacts with the same value is close together in your source files.*

이 예제는 또한 참조 타입이 추론하기 더 어려울 수 있는 방법을 보여줍니다. 만약 당신의 프로그램 코드에서 `tenEighty`와 `alsoTenEighty`가 멀리 떨어져 있었다면, 비디오 모드가 변경되는 모든 방법을 찾기 어려울 수 있습니다. `tenEighty`를 사용하는 곳이라면 `alsoTenEighty`를 사용하는 코드도 생각해야하고 그 반대도 마찬가지입니다. 반면, 값 타입은 동일한 값과 상호작용하는 모든 코드가 원본 파일에서 서로 가깝기 때문에 추론하기가 더 쉽습니다.

*Note that `tenEighty` and `alsoTenEighty` are declared as constants, rather than variables. However, you can still change `tenEighty.frameRate` and `alsoTenEighty.frameRate` because the values of the `tenEighty` and `alsoTenEighty` constants themselves don’t actually change. `tenEighty` and `alsoTenEighty` themselves don’t “store” the `VideoMode` instance—instead, they both refer to a `VideoMode` instance behind the scenes. It’s the `frameRate` property of the underlying `VideoMode` that’s changed, not the values of the constant references to that `VideoMode`.*

참고로 `tenEighty`와 `alsoTenEighty`는 변수가 아닌 상수로 선언합니다. 그러나 `tenEighty`와 `alsoTenEighty`의 상수 자체의 값은 실제로 변경되지 않으므로 `tenEighty.frameRate`와 `tenEighty.frameRate`를 변경할 수 있습니다. 변경된 것은 해당 `VideoMode`에 대한 지속적인 참조 값이 아니라 기본 `VideoMode`의 `frameRate` 속성입니다.

### *Identity Operators : 식별 연산자*

*Because classes are reference types, it’s possible for multiple constants and variables to refer to the same single instance of a class behind the scenes. (The same isn’t true for structures and enumerations, because they’re always copied when they’re assigned to a constant or variable, or passed to a function.)*

클래스는 참조 타입이므로 여러 상수와 변수가 백그라운드에서 클래스의 동일한 단일 인스턴스를 참조할 수 있습니다. 구조체 및 열거형은 상수 혹은 변수에 할당되거나 함수에 전달될 때 항상 복사되기 때문에 동일하지 않습니다.

*It can sometimes be useful to find out whether two constants or variables refer to exactly the same instance of a class. To enable this, Swift provides two identity operators:*

두 상수 혹은 변수가 정확히 동일한 클래스 인스턴스를 참조하는지 여부를 확인하는 것이 유용할 수 있습니다. 이를 위해 Swift는 두 가지 식별연산자를 제공합니다.

- *Identical to (`===`)*
  
  동일 (`===`)

- *Not identical to (`!==`)*
  
  동일하지 않음 (`!==`)

*Use these operators to check whether two constants or variables refer to the same single instance:*

이러한 연산자를 사용해서 두 상수 혹은 변수가 동일한 단일 인스턴스를 참조하는지 확인합니다.

```swift
if tenEighty === alsoTenEighty {
    print("tenEighty and alsoTenEighty refer to the same VideoMode instance.")
}
// Prints "tenEighty and alsoTenEighty refer to the same VideoMode instance."
```

*Note that identical to (represented by three equals signs, or `===`) doesn’t mean the same thing as equal to (represented by two equals signs, or `==`). Identical to means that two constants or variables of class type refer to exactly the same class instance. Equal to means that two instances are considered equal or equivalent in value, for some appropriate meaning of equal, as defined by the type’s designer.*

identical to (세개의 등호 혹은 `===`으로 표시됨)은 equal to (2개의 등호 혹은 `==`으로 표시됨) 를 의미하지 않습니다. Identical to는 클래스 타입의 두 상수 혹은 변수가 정확히 동일한 클래스 인스턴스를 참조함을 의미합니다. Equal to 는 타입의 설계자가 정의한 것처럼 두 인스턴스가 일부 앱에서 동일하거나 동등한 것으로 간주됨을 의미합니다.

*When you define your own custom structures and classes, it’s your responsibility to decide what qualifies as two instances being equal. The process of defining your own implementations of the `==` and `!=` operators is described in [Equivalence Operators](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID45).*

사용자 정의 구조 및 클래스를 정의할 때 두 인스턴스가 동일한 것으로 간주되는 조건을 결정하는 것은 사용자의 책임입니다. 구현을 정의하는 프로세스인 `==`와 `!=` 연산자는 [링크]에 설명되어있습니다.

### *Pointers : 포인터*

*If you have experience with C, C++, or Objective-C, you may know that these languages use pointers to refer to addresses in memory.* *A Swift constant or variable that refers to an instance of some reference type is similar to a pointer in C, but isn’t a direct pointer to an address in memory, and doesn’t require you to write an asterisk* (`*`) *to indicate that you are creating a reference.* *Instead, these references are defined like any other constant or variable in Swift. The standard library provides pointer and buffer types that you can use if you need to interact with pointers directly—see [Manual Memory Management](https://developer.apple.com/documentation/swift/swift_standard_library/manual_memory_management).*

C, C++ 혹은 Objective-C에 대한 경험이 있다면 이러한 언어들이 메모리의 주소를 참조하기 위해 포인터를 사용한다는 것을 알 수 있습니다. 일부 참조 타입의 인스턴스를 참조하는 Swift상수 혹은 변수는 C의 포인터와 유사하지만 메모리의 주소에 대한 직접 포인터가 아니며 참조를 작성하고 있음을 나타내기 위해 별표 (`*`)를 작성할 필요가 없습니다. 대신에, 이러한 참조는 Swift의 다른 상수 혹은 변수와 같이 정의됩니다. 표준 라이브러리는 포인터와 직접 상호작용해야할 경우 사용할 수 있는 포인터 및 버퍼 타입을 제공합니다. [링크]를 참조하세요.
