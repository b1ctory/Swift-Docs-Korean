### *Enumeration Types : 열거형 타입*

*The individual cases of an enumeration automatically receive the same access level as the enumeration they belong to. You can’t specify a different access level for individual enumeration cases.*

개별 열거형 케이스는 해당 케이스가 속한 열거형과 동일한 액세스 수준을 자동으로 수신합니다. 개별 열거형 케이스에 대해 다른 액세스 레벨을 지정할 수 없습니다.

*In the example below, the `CompassPoint` enumeration has an explicit access level of public. The enumeration cases `north`, `south`, `east`, and `west` therefore also have an access level of public:*

아래 예에서 `CompassPoint` 열거형에는 공개 액세스 레벨이 명시되어 있습니다. 따라서 `north`, `south`, `east` 및 `west` 열거형 케이스에도 공개 액세스 레벨이 있습니다.

```swift
public enum CompassPoint {
    case north
    case south
    case east
    case west
}
```

#### *Raw Values and Associated Values  : 원시값 및 관련값*

*The types used for any raw values or associated values in an enumeration definition must have an access level at least as high as the enumeration’s access level. For example, you can’t use a private type as the raw-value type of an enumeration with an internal access level.*

열거형 정의에서 원시 값 또는 관련 값에 사용되는 타입에는 적어도 열거형의 액세스 레벨만큼 높은 액세스 수준이 있어야 합니다. 예를 들어 내부 액세스 수준이 있는 열거형의 원시 값 타입으로 비공개 타입을 사용할 수 없습니다.

### *Nested Types : 중첩 타입*

*The access level of a nested type is the same as its containing type, unless the containing type is public. Nested types defined within a public type have an automatic access level of internal. If you want a nested type within a public type to be publicly available, you must explicitly declare the nested type as public.*

중첩 타입의 액세스 레벨은 포함 타입이 공개가 아닌 한 포함 타입과 동일합니다. 공개 타입 내에서 정의된 중첩 타입의 자동 액세스 레벨은 내부입니다. 퍼블릭 타입 내의 중첩 타입을 공개적으로 사용할 수 있게 하려면 중첩 타입을 퍼블릭으로 명시적으로 선언해야 합니다.
