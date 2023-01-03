## *Structures and Enumerations Are Value Types : 구조체와 열거형은 값타입*

*A value type is a type whose value is copied when it’s assigned to a variable or constant, or when it’s passed to a function.*

값타입은 변수 혹은 상수에 할당되거나 함수에 전달될 때 값이 복사되는 타입입니다.

*You’ve actually been using value types extensively throughout the previous chapters. In fact, all of the basic types in Swift—integers, floating-point numbers, Booleans, strings, arrays and dictionaries—are value types, and are implemented as structures behind the scenes.*

실제로 이전 장에서 값 타입을 광범위하게 사용해왔습니다. 실제로 Swift의 모든 기본 타입 - 정수, 부동소수점 숫자, Bool, 문자열, 배열, 딕셔너리-는값 타입이며 뒤에서 구조체로 구현됩니다.

*All structures and enumerations are value types in Swift. This means that any structure and enumeration instances you create—and any value types they have as properties—are always copied when they’re passed around in your code.*

Swift에서는 모든 구조체 및 열거형이 값 타입입니다. 즉, 작성한 구조체 및 열거형 인스턴스와 해당 인스턴스가 속성으로 가지는 모든 값 타입은 코드에서 전달될 때 항상 복사됩니다.

> *NOTE*
> 
> *Collections defined by the standard library like arrays, dictionaries, and strings use an optimization to reduce the performance cost of copying. Instead of making a copy immediately, these collections share the memory where the elements are stored between the original instance and any copies. If one of the copies of the collection is modified, the elements are copied just before the modification. The behavior you see in your code is always as if a copy took place immediately.*
> 
> 배열, 딕셔너리 및 문자열과 같은 표준 라이브러리에 의해 정의된 컬렉션은 최적화를 사용해서 복사의 성능 비용을 절감합니다. 이러한 컬렉션은 즉시 복사본을 만드는 대신 원본 인스턴스와 복사본 사이에 요소가 요소가 저장되는 메모리를 공유합니다. 컬렉션 복사본 중 하나를 수정하면 요소가 수정 직전에 복사됩니다. 코드에서 볼 수 있는 동작은 항상 복사본이 즉시 발생한 것과 같습니다.

*Consider this example, which uses the `Resolution` structure from the previous example:*

이전 예제의 `Resolution` 구조체를 사용하는 이 예시를 생각해보세요.

```swift
let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
```

*This example declares a constant called `hd` and sets it to a `Resolution` instance initialized with the width and height of full HD video (1920 pixels wide by 1080 pixels high).*

이 예시에서는 `hd`라는 상수를 선언하고 풀 HD 비디오 (폭 1920픽셀 x 높이 1080픽셀) 의 너비와 높이로 초기화된 `Resolution` 인스턴스로 설정합니다.

*It then declares a variable called `cinema` and sets it to the current value of `hd`. Because `Resolution` is a structure, a copy of the existing instance is made, and this new copy is assigned to `cinema`. Even though `hd` and `cinema` now have the same width and height, they’re two completely different instances behind the scenes.*

그런다음 `cinema`라는 변수를 선언하고 현재 값인 hd로 설정합니다. 해상도는 구조체이기 때문에 기존 인스턴스의 복사본이 만들어지고, 이 새 복사본은 `cinema`에 할당됩니다. hd와 cinema는 이제 너비와 높이가 같지만 무대 뒤에서는 전혀 다른 예시입니다.

*Next, the `width` property of `cinema` is amended to be the width of the slightly wider 2K standard used for digital cinema projection (2048 pixels wide and 1080 pixels high):*

다음으로, `cinema`의 `width` 프로퍼티는 디지털 시네마 투영에 사용되는 약간 더 넓은 2K 표준의 너비 (가로 2048픽셀, 세로 1080픽셀)로 수정됩니다.

```swift
cinema.width = 2048
```

*Checking the `width` property of `cinema` shows that it has indeed changed to be `2048`:*

`cinema`의 `width` 프로퍼티를 확인해보면 실제로 `2048`로 변경되었음을 알 수 있습니다.

```swift
print("cinema is now \(cinema.width) pixels wide")
// Prints "cinema is now 2048 pixels wide"
```

*However, the `width` property of the original `hd` instance still has the old value of `1920`:*

그러나, 원래 `hd` 인스턴스의 `width` 속성은 여전히 이전 값인 `1920`을 가지고 있습니다.

```swift
print("hd is still \(hd.width) pixels wide")
// Prints "hd is still 1920 pixels wide"
```

*When `cinema` was given the current value of `hd`, the values stored in `hd` were copied into the new `cinema` instance. The end result was two completely separate instances that contained the same numeric values. However, because they’re separate instances, setting the width of `cinema` to `2048` doesn’t affect the width stored in `hd`, as shown in the figure below:*

`cinema`에 현재값 `hd`를 지정하면 hd에 저장된 값이 새로운 `cinema` 인스턴스에 복사됩니다. 최종 결과는 동일한 숫자 값을 포함하는 완전히 별개의 두 인스턴스였습니다. 그러나 `cinema`의 너비를 `2048`로 설정해도 아래 그림과 같이 `hd`에 저장된 너비에는 영향을 미치지 않습니다.

![](https://docs.swift.org/swift-book/_images/sharedStateStruct_2x.png)

*The same behavior applies to enumerations:*

다음과 같은 동작이 열거형에도 저장됩니다.

```swift
enum CompassPoint {
    case north, south, east, west
    mutating func turnNorth() {
        self = .north
    }
}
var currentDirection = CompassPoint.west
let rememberedDirection = currentDirection
currentDirection.turnNorth()

print("The current direction is \(currentDirection)")
print("The remembered direction is \(rememberedDirection)")
// Prints "The current direction is north"
// Prints "The remembered direction is west"
```

*When `rememberedDirection` is assigned the value of `currentDirection`, it’s actually set to a copy of that value. Changing the value of `currentDirection` thereafter doesn’t affect the copy of the original value that was stored in `rememberedDirection`.*

`rememberedDirection`에 `currentDirection`값이 할당되면 실제로 해당 값의 복사본으로 설정됩니다. 이후 `currentDirection` 값을 변경해도 `rememberedDirection`에 저장된 원래 값의 복사에는 영향을 주지 않습니다.
