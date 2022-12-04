## *Type Aliases*

*Type aliases define an alternative name for an existing type. You define type aliases with the `typealias` keyword.*

TypeAlias는 기존 형식의 대체 이름을 정의합니다. typealias 키워드를 사용해서 타입의 별칭을 지정합니다.



*Type aliases are useful when you want to refer to an existing type by a name that’s contextually more appropriate, such as when working with data of a specific size from an external source:*

타입 별칭은 외부 원본의 특정 크기의 데이터로 작업하는 경우와 같이 상황에 따라 더 적합한 이름으로 기존 형식을 참조하려는 경우에 유용합니다.

```swift
typealias AudioSample = UInt16
```

*Once you define a type alias, you can use the alias anywhere you might use the original name:*

type alias를 정의한 후에 당신은 원래 이름을 사용할 수 있는 모든 곳에서 별칭을 사용할 수 있습니다.

```swift
var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound is now 0
```

*Here, `AudioSample` is defined as an alias for `UInt16`. Because it’s an alias, the call to `AudioSample.min` actually calls `UInt16.min`, which provides an initial value of `0` for the `maxAmplitudeFound` variable.*

여기서 AudioSample은 UInt의 별칭으로 정의됩니다. AudioSample.min에 대한 호출은 별칭이기 때문에 실제로는 maxAmplitudeFound 변수의 초기값 0을 제공하는 UInt16.min을 호출합니다. 
