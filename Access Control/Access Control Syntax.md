## *Access Control Syntax : 엑세스 제어 구문*

*Define the access level for an entity by placing one of the `open`, `public`, `internal`, `fileprivate`, or `private` modifiers at the beginning of the entity’s declaration.*

`open`, `public`, `internal`, `fileprivate` 또는 `private` 제어자 중 하나를 항목 선언의 시작 부분에 배치하여 항목의 액세스 레벨을 정의합니다.

```swift
public class SomePublicClass {}
internal class SomeInternalClass {}
fileprivate class SomeFilePrivateClass {}
private class SomePrivateClass {}

public var somePublicVariable = 0
internal let someInternalConstant = 0
fileprivate func someFilePrivateFunction() {}
private func somePrivateFunction() {}
```

*Unless otherwise specified, the default access level is internal, as described in [Default Access Levels](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol#Default-Access-Levels). This means that `SomeInternalClass` and `someInternalConstant` can be written without an explicit access-level modifier, and will still have an access level of internal:*

따로 지정하지 않는 한 기본 액세스 레벨은 [링크]에 설명된 대로 내부입니다. 즉, `SomeInternalClass` 및 `someInternalConstant`는 명시적인 액세스 레벨 제어자 없이 작성될 수 있으며 여전히 내부 액세스 레벨을 가집니다.

```swift
class SomeInternalClass {}              // implicitly internal
let someInternalConstant = 0            // implicitly internal
```
