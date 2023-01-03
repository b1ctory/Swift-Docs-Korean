## *Stored Properties*

*In its simplest form, a stored property is a constant or variable that’s stored as part of an instance of a particular class or structure. Stored properties can be either variable stored properties (introduced by the `var` keyword) or constant stored properties (introduced by the `let` keyword).*

*You can provide a default value for a stored property as part of its definition, as described in [Default Property Values](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID206). You can also set and modify the initial value for a stored property during initialization. This is true even for constant stored properties, as described in [Assigning Constant Properties During Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID212).*

*The example below defines a structure called `FixedLengthRange`, which describes a range of integers whose range length can’t be changed after it’s created:*

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

### *Stored Properties of Constant Structure Instances*

*If you create an instance of a structure and assign that instance to a constant, you can’t modify the instance’s properties, even if they were declared as variable properties:*

```swift
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
// this range represents integer values 0, 1, 2, and 3
rangeOfFourItems.firstValue = 6
// this will report an error, even though firstValue is a variable property
```

*Because `rangeOfFourItems` is declared as a constant (with the `let` keyword), it isn’t possible to change its `firstValue` property, even though `firstValue` is a variable property.*

*This behavior is due to structures being value types. When an instance of a value type is marked as a constant, so are all of its properties.*

*The same isn’t true for classes, which are reference types. If you assign an instance of a reference type to a constant, you can still change that instance’s variable properties.*

### *Lazy Stored Properties*

*A lazy stored property is a property whose initial value isn’t calculated until the first time it’s used. You indicate a lazy stored property by writing the `lazy` modifier before its declaration.*

> *NOTE*
> 
> *You must always declare a lazy property as a variable (with the `var` keyword), because its initial value might not be retrieved until after instance initialization completes. Constant properties must always have a value before initialization completes, and therefore can’t be declared as lazy.*

*Lazy properties are useful when the initial value for a property is dependent on outside factors whose values aren’t known until after an instance’s initialization is complete. Lazy properties are also useful when the initial value for a property requires complex or computationally expensive setup that shouldn’t be performed unless or until it’s needed.*

*The example below uses a lazy stored property to avoid unnecessary initialization of a complex class. This example defines two classes called `DataImporter` and `DataManager`, neither of which is shown in full:*

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

*Part of the functionality of the `DataManager` class is the ability to import data from a file. This functionality is provided by the `DataImporter` class, which is assumed to take a nontrivial amount of time to initialize. This might be because a `DataImporter` instance needs to open a file and read its contents into memory when the `DataImporter` instance is initialized.*

*Because it’s possible for a `DataManager` instance to manage its data without ever importing data from a file, `DataManager` doesn’t create a new `DataImporter` instance when the `DataManager` itself is created. Instead, it makes more sense to create the `DataImporter` instance if and when it’s first used.*

*Because it’s marked with the `lazy` modifier, the `DataImporter` instance for the `importer` property is only created when the `importer` property is first accessed, such as when its `filename` property is queried:*

```swift
print(manager.importer.filename)
// the DataImporter instance for the importer property has now been created
// Prints "data.txt"
```

> *NOTE*
> 
> *If a property marked with the `lazy` modifier is accessed by multiple threads simultaneously and the property hasn’t yet been initialized, there’s no guarantee that the property will be initialized only once.*

### *Stored Properties and Instance Variables*

*If you have experience with Objective-C, you may know that it provides two ways to store values and references as part of a class instance. In addition to properties, you can use instance variables as a backing store for the values stored in a property.*

*Swift unifies these concepts into a single property declaration. A Swift property doesn’t have a corresponding instance variable, and the backing store for a property isn’t accessed directly. This approach avoids confusion about how the value is accessed in different contexts and simplifies the property’s declaration into a single, definitive statement. All information about the property—including its name, type, and memory management characteristics—is defined in a single location as part of the type’s definition.*


