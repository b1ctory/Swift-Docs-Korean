## *Strong Reference Cycles Between Class Instances*

*In the examples above, ARC is able to track the number of references to the new `Person` instance you create and to deallocate that `Person` instance when it’s no longer needed.*

*However, it’s possible to write code in which an instance of a class never gets to a point where it has zero strong references. This can happen if two class instances hold a strong reference to each other, such that each instance keeps the other alive. This is known as a strong reference cycle.*

*You resolve strong reference cycles by defining some of the relationships between classes as weak or unowned references instead of as strong references. This process is described in [Resolving Strong Reference Cycles Between Class Instances](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/automaticreferencecounting#Resolving-Strong-Reference-Cycles-Between-Class-Instances). However, before you learn how to resolve a strong reference cycle, it’s useful to understand how such a cycle is caused.*

*Here’s an example of how a strong reference cycle can be created by accident. This example defines two classes called `Person` and `Apartment`, which model a block of apartments and its residents:*

```swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment?
    deinit { print("\(name) is being deinitialized") }
}

class Apartment {
    let unit: String
    init(unit: String) { self.unit = unit }
    var tenant: Person?
    deinit { print("Apartment \(unit) is being deinitialized") }
}
```

*Every `Person` instance has a `name` property of type `String` and an optional `apartment` property that’s initially `nil`. The `apartment` property is optional, because a person may not always have an apartment.*

*Similarly, every `Apartment` instance has a `unit` property of type `String` and has an optional `tenant` property that’s initially `nil`. The tenant property is optional because an apartment may not always have a tenant.*

*Both of these classes also define a deinitializer, which prints the fact that an instance of that class is being deinitialized. This enables you to see whether instances of `Person` and `Apartment` are being deallocated as expected.*

*This next code snippet defines two variables of optional type called `john` and `unit4A`, which will be set to a specific `Apartment` and `Person` instance below. Both of these variables have an initial value of `nil`, by virtue of being optional:*

```swift
var john: Person?
var unit4A: Apartment?
```

*You can now create a specific `Person` instance and `Apartment` instance and assign these new instances to the `john` and `unit4A` variables:*

```swift
john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")
```

*Here’s how the strong references look after creating and assigning these two instances. The `john` variable now has a strong reference to the new `Person` instance, and the `unit4A` variable has a strong reference to the new `Apartment` instance:*

*![](https://docs.swift.org/swift-book/images/referenceCycle01@2x.png)*

*You can now link the two instances together so that the person has an apartment, and the apartment has a tenant. Note that an exclamation point (`!`) is used to unwrap and access the instances stored inside the `john` and `unit4A` optional variables, so that the properties of those instances can be set:*

```swift
john!.apartment = unit4A
unit4A!.tenant = john
```

*Here’s how the strong references look after you link the two instances together:*

*![](https://docs.swift.org/swift-book/images/referenceCycle02@2x.png)*

*Unfortunately, linking these two instances creates a strong reference cycle between them. The `Person` instance now has a strong reference to the `Apartment` instance, and the `Apartment` instance has a strong reference to the `Person` instance. Therefore, when you break the strong references held by the `john` and `unit4A` variables, the reference counts don’t drop to zero, and the instances aren’t deallocated by ARC:*

```swift
john = nil
unit4A = nil
```

*Note that neither deinitializer was called when you set these two variables to `nil`. The strong reference cycle prevents the `Person` and `Apartment` instances from ever being deallocated, causing a memory leak in your app.*

*Here’s how the strong references look after you set the `john` and `unit4A` variables to `nil`:*

*![](https://docs.swift.org/swift-book/images/referenceCycle03@2x.png)*

*The strong references between the `Person` instance and the `Apartment` instance remain and can’t be broken.*
