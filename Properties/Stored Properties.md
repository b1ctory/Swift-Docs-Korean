## *Stored Properties : 저장 프로퍼티*

*In its simplest form, a stored property is a constant or variable that’s stored as part of an instance of a particular class or structure. Stored properties can be either variable stored properties (introduced by the `var` keyword) or constant stored properties (introduced by the `let` keyword).*

가장 간단한 형태로, 저장프로퍼티는 특정 클래스 또는 구조체의 인스턴스 일부로 저장되는 상수 또는 변수입니다. 저장프로퍼티는 변수 저장프로퍼티(`var` 키워드에 의해 도입됨) 또는 상수 저장프로퍼티(`let` 키워드에 의해 도입됨)일 수 있습니다.

*You can provide a default value for a stored property as part of its definition, as described in [Default Property Values](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID206). You can also set and modify the initial value for a stored property during initialization. This is true even for constant stored properties, as described in [Assigning Constant Properties During Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID212).*

[링크]에 설명된 대로 저장프로퍼티의 기본값을 정의의 일부로 제공할 수 있습니다. 초기화 중 저장프로퍼티의 초기 값을 설정하고 수정할 수도 있습니다. 이것은 [링크]에서 설명한 바와 같이 상수 저장프로퍼티의 경우에도 해당됩니다.

*The example below defines a structure called `FixedLengthRange`, which describes a range of integers whose range length can’t be changed after it’s created:*

아래의 예는 `FixedLengthRange`라는 구조체를 정의하는데, 이 구조체는 생성된 후 범위 길이를 변경할 수 없는 정수의 범위를 설명합니다.

```swift
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
// the range represents integer values 0, 1, and 2
rangeOfThreeItems.firstValue = 6
// the range now represents integer values 6, 7, and 8
```

*Instances of `FixedLengthRange` have a variable stored property called `firstValue` and a constant stored property called `length`. In the example above, `length` is initialized when the new range is created and can’t be changed thereafter, because it’s a constant property.*

`FixedLengthRange`의 인스턴스에는 `firstValue`라는 변수 저장프로퍼티와 `length`라는 상수 저장프로퍼티가 있습니다. 위의 예에서 `length`는 새 범위가 생성될 때 초기화되며 상수 프로퍼티이기 때문에 이후에 변경할 수 없습니다.

### *Stored Properties of Constant Structure Instances " 상수 구조체 인스턴스의 저장 프로퍼티*

*If you create an instance of a structure and assign that instance to a constant, you can’t modify the instance’s properties, even if they were declared as variable properties:*

구조체의 인스턴스를 생성하고 해당 인스턴스를 상수에 할당하면 변수 프로퍼티로 선언된 경우에도 인스턴스의 프로퍼티를 수정할 수 없습니다.

```swift
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
// this range represents integer values 0, 1, 2, and 3
rangeOfFourItems.firstValue = 6
// this will report an error, even though firstValue is a variable property
```

*Because `rangeOfFourItems` is declared as a constant (with the `let` keyword), it isn’t possible to change its `firstValue` property, even though `firstValue` is a variable property.*

`rangeOfFourItems`는 (`let` 키워드를 사용하여) 상수로 선언되므로 `firstValue`가 변수 프로퍼티임에도 불구하고 `firstValue` 프로퍼티를 변경할 수 없습니다.

*This behavior is due to structures being value types. When an instance of a value type is marked as a constant, so are all of its properties.*

이 동작은 구조체가 값 타입이기 때문입니다. 값 타입의 인스턴스가 상수로 표시되면 해당하는 모든 프로퍼티도 상수로 표시됩니다.

*The same isn’t true for classes, which are reference types. If you assign an instance of a reference type to a constant, you can still change that instance’s variable properties.*

참조 타입인 클래스에 대해서는 동일하지 않습니다. 참조 타입의 인스턴스를 상수에 할당하는 경우에도 해당 인스턴스의 변수 프로퍼티를 변경할 수 있습니다.

### *Lazy Stored Properties : Lazy 저장 프로퍼티*

*A lazy stored property is a property whose initial value isn’t calculated until the first time it’s used. You indicate a lazy stored property by writing the `lazy` modifier before its declaration.*

lazy저장프로퍼티는 처음 사용할 때까지 초기 값이 계산되지 않는 프로퍼티입니다. 당신은 `lazy` 수식어를 선언 전에 써서 lazy 저장 프로퍼티를 나타냅니다.

> *NOTE*
> 
> *You must always declare a lazy property as a variable (with the `var` keyword), because its initial value might not be retrieved until after instance initialization completes. Constant properties must always have a value before initialization completes, and therefore can’t be declared as lazy.*
> 
> `var` 키워드를 사용하여 lazy 프로퍼티를 항상 변수로 선언해야 합니다.(`var` 키워드와 함께) 인스턴스 초기화가 완료될 때까지 초기 값이 검색되지 않을 수 있기 때문입니다. 상수 프로퍼티는 초기화가 완료되기 전에 항상 값을 가져야 하므로 lazy로 선언할 수 없습니다.

*Lazy properties are useful when the initial value for a property is dependent on outside factors whose values aren’t known until after an instance’s initialization is complete. Lazy properties are also useful when the initial value for a property requires complex or computationally expensive setup that shouldn’t be performed unless or until it’s needed.*

lazy 프로퍼티는 프로퍼티의 초기 값이 인스턴스의 초기화가 완료될 때까지 값을 알 수 없는 외부 요인에 의존할 때 유용합니다. lazy 프로퍼티는 프로퍼티의 초기 값이 복잡하고 계산 비용이 많이 드는 설정을 필요로 할 때도 유용합니다. 이 설정은 필요하지 않거나 필요할 때까지 수행되어서는 안 됩니다.

*The example below uses a lazy stored property to avoid unnecessary initialization of a complex class. This example defines two classes called `DataImporter` and `DataManager`, neither of which is shown in full:*

아래 예제에서는 복잡한 클래스의 불필요한 초기화를 방지하기 위해 lazy 저장 프로퍼티를 사용합니다. 이 예에서는 `DataImporter`와 `DataManager`라는 두 개의 클래스를 정의하고, 둘 다 완전히 표시되지 않습니다:

```swift
class DataImporter {
    /*
    DataImporter is a class to import data from an external file.
    The class is assumed to take a nontrivial amount of time to initialize.
    */
    var filename = "data.txt"
    // the DataImporter class would provide data importing functionality here
}

class DataManager {
    lazy var importer = DataImporter()
    var data: [String] = []
    // the DataManager class would provide data management functionality here
}

let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// the DataImporter instance for the importer property hasn't yet been created
```

*The `DataManager` class has a stored property called `data`, which is initialized with a new, empty array of `String` values. Although the rest of its functionality isn’t shown, the purpose of this `DataManager` class is to manage and provide access to this array of `String` data.*

`DataManager`클래스에는 `data`라는 저장프로퍼티가 있으며, 이 프로퍼티는 `String` 값의 빈 새 배열로 초기화됩니다. 나머지 기능은 표시되지 않지만, 이 `DataManager`클래스의 목적은 이 `String` 데이터 배열을 관리하고 액세스를 제공하는 것입니다.

*Part of the functionality of the `DataManager` class is the ability to import data from a file. This functionality is provided by the `DataImporter` class, which is assumed to take a nontrivial amount of time to initialize. This might be because a `DataImporter` instance needs to open a file and read its contents into memory when the `DataImporter` instance is initialized.*

`DataManager` 클래스의 기능 중 일부는 파일에서 데이터를 가져오는 기능입니다. 이 기능은 초기화하는 데 상당한 시간이 걸리는 것으로 가정되는 `DataImporter` 클래스에서 제공됩니다. 이는 `DataImporter` 인스턴스가 초기화될 때 `DataImporter` 인스턴스가 파일을 열고 해당 내용을 메모리로 읽어야 하기 때문일 수 있습니다.

*Because it’s possible for a `DataManager` instance to manage its data without ever importing data from a file, `DataManager` doesn’t create a new `DataImporter` instance when the `DataManager` itself is created. Instead, it makes more sense to create the `DataImporter` instance if and when it’s first used.*

`DataManager` 인스턴스는 파일에서 데이터를 가져오지 않고 데이터를 관리할 수 있기 때문에 `DataManager` 자체를 만들 때 `DataImporter` 인스턴스를 새로 만들지 않습니다. 대신 `DataImporter` 인스턴스를 처음 사용할 때 생성하는 것이 더 합리적입니다.

*Because it’s marked with the `lazy` modifier, the `DataImporter` instance for the `importer` property is only created when the `importer` property is first accessed, such as when its `filename` property is queried:*

`lazy` 수식자로 표시되어 있기 때문에 `importer` 속성의 `DataImporter` 인스턴스는 `filename` 프로퍼티가 쿼리되는 경우와 같이 `importer` 프로퍼티에 처음 액세스할 때만 생성됩니다:

```swift
print(manager.importer.filename)
// the DataImporter instance for the importer property has now been created
// Prints "data.txt"
```

> *NOTE*
> 
> *If a property marked with the `lazy` modifier is accessed by multiple threads simultaneously and the property hasn’t yet been initialized, there’s no guarantee that the property will be initialized only once.*
> 
> `lazy` 수식자로 표시된 프로퍼티가 여러 스레드에 의해 동시에 액세스되고 프로퍼티가 아직 초기화되지 않았다면 프로퍼티가 한 번만 초기화된다는 보장은 없습니다.

### *Stored Properties and Instance Variables : 저장프로퍼티 및 인스턴스 변수*

*If you have experience with Objective-C, you may know that it provides two ways to store values and references as part of a class instance. In addition to properties, you can use instance variables as a backing store for the values stored in a property.*

Objective-C를 사용한 경험이 있는 경우, Objective-C가 클래스 인스턴스의 일부로 값과 참조를 저장하는 두 가지 방법을 제공한다는 것을 알 수 있습니다. 프로퍼티 외에도 인스턴스 변수를 프로퍼티에 저장된 값의 백업 저장소로 사용할 수 있습니다.

*Swift unifies these concepts into a single property declaration. A Swift property doesn’t have a corresponding instance variable, and the backing store for a property isn’t accessed directly. This approach avoids confusion about how the value is accessed in different contexts and simplifies the property’s declaration into a single, definitive statement. All information about the property—including its name, type, and memory management characteristics—is defined in a single location as part of the type’s definition.*

Swift는 이러한 개념을 단일 속성 선언으로 통합합니다. `Swift` 프로퍼티에는 해당 인스턴스 변수가 없으며 속성의 백업 저장소에 직접 액세스하지 않습니다. 이 접근법은 값이 다른 상황에서 어떻게 접근되는지에 대한 혼란을 피하고 프로퍼티의 선언을 하나의 확정적인 진술로 단순화합니다. 프로퍼티에 대한 모든 정보(이름, 유형 및 메모리 관리 특성 포함)는 속성 정의의 일부로 단일 위치에 정의됩니다.


