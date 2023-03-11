## *Constants, Variables, Properties, and Subscripts : 상수, 변수, 프로퍼티, 그리고 서브스크립트*

*A constant, variable, or property can’t be more public than its type. It’s not valid to write a public property with a private type, for example. Similarly, a subscript can’t be more public than either its index type or return type.*

상수, 변수 또는 프로퍼티는 해당 타입보다 더 공개적일 수 없습니다. 예를 들어, 프라이빗 타입으로 퍼블릭 프로퍼티를 작성할 수 없습니다. 마찬가지로, 서브스크립트는 인덱스 타입 또는 반환 타입보다 더 공개적일일 수 없습니다.

*If a constant, variable, property, or subscript makes use of a private type, the constant, variable, property, or subscript must also be marked as `private`:*

상수, 변수, 프로퍼티 또는 서브스크립트가 전용 타입을 사용하는 경우에는 상수, 변수, 프로퍼티 또는 서브스크립트도 `private`로 표시해야 합니다:

```swift
private var privateInstance = SomePrivateClass()
```

### *Getters and Setters : 게터와 세터*

*Getters and setters for constants, variables, properties, and subscripts automatically receive the same access level as the constant, variable, property, or subscript they belong to.*

상수, 변수, 프로퍼티 및 서브스크립트에 대한 게터 및 세터는 자동으로 자신이 속한 상수, 변수, 프로퍼티 또는 서브스크립트와 동일한 액세스 레벨을 받습니다.

*You can give a setter a lower access level than its corresponding getter, to restrict the read-write scope of that variable, property, or subscript. You assign a lower access level by writing `fileprivate(set)`, `private(set)`, or `internal(set)` before the `var` or `subscript` introducer.*

세터에 해당하는 게터보다 낮은 액세스 레벨을 부여하여 해당 변수, 속성 또는 서브스크립트의 읽기-쓰기 범위를 제한할 수 있습니다. `var` 또는 `subscript` 소개자 앞에 `fileprivate(set)`, `private(set)` 또는 `internal(set)`을 작성하여 더 낮은 액세스 레벨을 할당합니다.

> *Note*
> 
> *This rule applies to stored properties as well as computed properties. Even though you don’t write an explicit getter and setter for a stored property, Swift still synthesizes an implicit getter and setter for you to provide access to the stored property’s backing storage. Use `fileprivate(set)`, `private(set)`, and `internal(set)` to change the access level of this synthesized setter in exactly the same way as for an explicit setter in a computed property.*
> 
> 이 규칙은 저장 프로퍼티와 연산 프로퍼티에 적용됩니다. 저장 프로퍼티에 대해 명시적인 getter 및 setter를 작성하지 않더라도 Swift는 여전히 암시적 getter 및 setter를 합성하여 저장 프로퍼티의 백업 저장소에 대한 액세스를 제공합니다. `fileprivate(set)`, `private(set)` 및 `internal(set)`을 사용하여 이 합성된 setter의 액세스 레벨을 연산 프로퍼티의 명시적 setter와 똑같은 방식으로 변경합니다.

*The example below defines a structure called `TrackedString`, which keeps track of the number of times a string property is modified:*

아래 예는 문자열 프로퍼티가 수정된 횟수를 추적하는 `TrackedString`이라는 구조체를 정의합니다.

```swift
struct TrackedString {
    private(set) var numberOfEdits = 0
    var value: String = "" {
        didSet {
            numberOfEdits += 1
        }
    }
}
```

*The `TrackedString` structure defines a stored string property called `value`, with an initial value of `""` (an empty string). The structure also defines a stored integer property called `numberOfEdits`, which is used to track the number of times that `value` is modified. This modification tracking is implemented with a `didSet` property observer on the `value` property, which increments `numberOfEdits` every time the `value` property is set to a new value.*

`TrackedString` 구조체는 초기 값이 `""`(빈 문자열)인 `value`라는 문자열 저장 프로퍼티를 정의합니다. 이 구조체는 `value`가 수정된 횟수를 추적하는 데 사용되는 `numberOfEdits`라는 정수 저장 프로퍼티를 정의합니다. 이 수정 추적은 `value` 프로퍼티의 `didSet` 프로퍼티 옵저버로 구현되며 `value` 프로퍼티가 새 값으로 설정될 때마다 `numberOfEdits`가 증가합니다.

*The `TrackedString` structure and the `value` property don’t provide an explicit access-level modifier, and so they both receive the default access level of internal. However, the access level for the `numberOfEdits` property is marked with a `private(set)` modifier to indicate that the property’s getter still has the default access level of internal, but the property is settable only from within code that’s part of the `TrackedString` structure. This enables `TrackedString` to modify the `numberOfEdits` property internally, but to present the property as a read-only property when it’s used outside the structure’s definition.*

`TrackedString` 구조체와 `value` 프로퍼티는 명시적인 액세스 레벨 수정자를 제공하지 않으므로 둘 다 내부의 기본 액세스 레벨을 받습니다. 그러나 `numberOfEdits` 프로퍼티에 대한 액세스 레벨은 프로퍼티의 getter가 여전히 내부의 기본 액세스 레벨을 가지고 있음을 나타내기 위해 `private(set)` 수정자로 표시되지만 프로퍼티는 `TrackedString` 구조체입니다. 이를 통해 `TrackedString`이 내부적으로 `numberOfEdits` 프로퍼티를 수정할 수 있지만 구조체 정의 외부에서 사용될 때 프로퍼티를 읽기 전용 프로퍼티로 표시할 수 있습니다.

*If you create a `TrackedString` instance and modify its string value a few times, you can see the `numberOfEdits` property value update to match the number of modifications:*

`TrackedString` 인스턴스를 만들고 문자열 값을 몇 번 수정하면 수정 횟수와 일치하도록 `numberOfEdits` 프로퍼티 값이 업데이트되는 것을 볼 수 있습니다.

```swift
var stringToEdit = TrackedString()
stringToEdit.value = "This string will be tracked."
stringToEdit.value += " This edit will increment numberOfEdits."
stringToEdit.value += " So will this one."
print("The number of edits is \(stringToEdit.numberOfEdits)")
// Prints "The number of edits is 3"
```

*Although you can query the current value of the `numberOfEdits` property from within another source file, you can’t modify the property from another source file. This restriction protects the implementation details of the `TrackedString` edit-tracking functionality, while still providing convenient access to an aspect of that functionality.*

다른 소스 파일 내에서 `numberOfEdits` 프로퍼티의 현재 값을 쿼리할 수 있지만 다른 소스 파일에서 프로퍼티를 수정할 수는 없습니다. 이 제한은 `TrackedString` 편집 추적 기능의 구현 세부정보를 보호하는 동시에 해당 기능의 측면에 대한 편리한 액세스를 계속 제공합니다.

*Note that you can assign an explicit access level for both a getter and a setter if required. The example below shows a version of the `TrackedString` structure in which the structure is defined with an explicit access level of public. The structure’s members (including the `numberOfEdits` property) therefore have an internal access level by default. You can make the structure’s `numberOfEdits` property getter public, and its property setter private, by combining the `public` and `private(set)` access-level modifiers:*

필요한 경우 getter와 setter 모두에 대해 명시적인 액세스 레벨을 할당할 수 있습니다. 아래 예는 구조체가 퍼블릭의 명시적 액세스 레벨로 정의된 `TrackedString` 구조체의 버전을 보여줍니다. 따라서 구조체의 구성원(`numberOfEdits` 프로퍼티 포함)에는 기본적으로 내부 액세스 수준이 있습니다. `public` 및 `private(set)` 액세스 수준 한정자를 결합하여 구조체의 `numberOfEdits` 프로퍼티 게터를 공개하고 해당 프로퍼티 setter를 프라이빗으로 만들 수 있습니다.

```swift
public struct TrackedString {
    public private(set) var numberOfEdits = 0
    public var value: String = "" {
        didSet {
            numberOfEdits += 1
        }
    }
    public init() {}
}
```
