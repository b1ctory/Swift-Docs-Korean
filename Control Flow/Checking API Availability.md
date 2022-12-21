## *Checking API Availability : API 가용성 확인*

*Swift has built-in support for checking API availability, which ensures that you don’t accidentally use APIs that are unavailable on a given deployment target.*

 Swift에는 API 가용성 확인을 위한 지원이 내장되어 있어 지정된 배포 대상에서 사용할 수 없는 API 를 실수로 사용하지 않도록 보장합니다.

*The compiler uses availability information in the SDK to verify that all of the APIs used in your code are available on the deployment target specified by your project. Swift reports an error at compile time if you try to use an API that isn’t available.*

컴파일러는 SDK의 가용성 정보를 사용해서 프로젝트에서 지정한 배포 대상에서 코드에 사용된 모든 API를 사용할 수 있는지 확인합니다. 사용할 수 없는 API를 사용하려고 하면 Swift가 컴파일 시 오류를 보고합니다.

*You use an availability condition in an `if` or `guard` statement to conditionally execute a block of code, depending on whether the APIs you want to use are available at runtime. The compiler uses the information from the availability condition when it verifies that the APIs in that block of code are available.*

사용할 API 가 런타임에 사용 가능한지 여부에 따라 조건부로 코드 블록을 실행하려면 `if` 혹은 `guard`문에서 가용성 조건을 사용합니다. 컴파일러는 해당 코드 블록의 API가 사용 가능한지 확인할 때 가용성 조건의 정보를 사용합니다.

```swift
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}
```

__The availability condition above specifies that in iOS, the body of the `if` statement executes only in iOS 10 and later; in macOS, only in macOS 10.12 and later. The last argument, `*`, is required and specifies that on any other platform, the body of the `if` executes on the minimum deployment target specified by your target._

위의 가용성 조건은 iOS에서 `if`문의 본문이 iOS 10 이상에서만 실행되고 macOS에서는 macOS 에서는 macOS 10.12 이상에서만 실행되도록 지정합니다. 마지막 인수인 `*`는 필수이며 다른 플랫폼에서 `if`의 본문의 대상이 지정한 최소 배포 대상에서 실행됨을 지정합니다.

*In its general form, the availability condition takes a list of platform names and versions. You use platform names such as `iOS`, `macOS`, `watchOS`, and `tvOS`—for the full list, see [Declaration Attributes](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html#ID348). In addition to specifying major version numbers like iOS 8 or macOS 10.10, you can specify minor versions numbers like iOS 11.2.6 and macOS 10.13.3.*

일반적인 형태에서 가용성 조건은 플랫폼 이름 및 버전 목록을 사용합니다.`iOS`, `macOS`, `watchOS` 그리고 `tvOS`와 같은 플랫폼 이름을 사용합니다. - 전체 목록은 [링크]를 확인하세요. iOS 8 혹은 macOS 10.10과 같은 주요 버전을 지정하는 것 외에도 iOS 11.2.6 및 macOS 10.13.3과 같은 부 버전 번호를 지정할 수 있습니다.

```swift
if #available(platform name version, ..., *) {
    statements to execute if the APIs are available
} else {
    fallback statements to execute if the APIs are unavailable
}
```

*When you use an availability condition with a `guard` statement, it refines the availability information that’s used for the rest of the code in that code block.*

`guard`문과 함께 가용성 조건을 사용하면 해당 코드 블록이 나머지 코드에 사용되는 가용성 정보가 세분화됩니다.

```swift
@available(macOS 10.12, *)
struct ColorPreference {
    var bestColor = "blue"
}

func chooseBestColor() -> String {
    guard #available(macOS 10.12, *) else {
        return "gray"
    }
    let colors = ColorPreference()
    return colors.bestColor
}
```

*In the example above, the `ColorPreference` structure requires macOS 10.12 or later. The `chooseBestColor()` function begins with an availability guard. If the platform version is too old to use `ColorPreference`, it falls back to behavior that’s always available. After the `guard` statement, you can use APIs that require macOS 10.12 or later.*

위의 예시에서 `ColorPreference` 구조체에는 macOS 10.12 이상의 버전이 필요합니다. `chooseBestColor()` 함수는 유효성 guard로 시작합니다. 플랫폼 버전이 너무 오래되어 `ColorPreference`를 사용할 수 없으면 항상 사용할 수 있는 동작으로 돌아갑니다. `guard` 구문 이후에는 macOS 10.12 이상이 필요한 API를 사용할 수 있습니다.

*In addition to `#available`, Swift also supports the opposite check using an unavailability condition. For example, the following two checks do the same thing:*

Swift는 `#available` 이외에도 사용 불가 조건을 이용한 반대 검사도 지원합니다. 예를 들어 다음 두 검사에서 동일한 작업을 수행합니다.

```swift
if #available(iOS 10, *) {
} else {
    // Fallback code
}

if #unavailable(iOS 10) {
    // Fallback code
}
```

*Using the `#unavailable` form helps ma*ke your code more readable when the check contains only fallback code.

`#unavailable` 형식을 사용하면 검사에 fallback 코드만 포함되어 있을 때 코드를 더 쉽게 읽을 수 있습니다.


