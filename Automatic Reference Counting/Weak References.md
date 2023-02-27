### *Weak References*

*A weak reference is a reference that doesn’t keep a strong hold on the instance it refers to, and so doesn’t stop ARC from disposing of the referenced instance. This behavior prevents the reference from becoming part of a strong reference cycle. You indicate a weak reference by placing the `weak` keyword before a property or variable declaration.*

*Because a weak reference doesn’t keep a strong hold on the instance it refers to, it’s possible for that instance to be deallocated while the weak reference is still referring to it. Therefore, ARC automatically sets a weak reference to `nil` when the instance that it refers to is deallocated. And, because weak references need to allow their value to be changed to `nil` at runtime, they’re always declared as variables, rather than constants, of an optional type.*

*You can check for the existence of a value in the weak reference, just like any other optional value, and you will never end up with a reference to an invalid instance that no longer exists.*

> *Note*
> 
> *Property observers aren’t called when ARC sets a weak reference to `nil`.*

*The example below is identical to the `Person` and `Apartment` example from above, with one important difference. This time around, the `Apartment` type’s `tenant` property is declared as a weak reference:*

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
    weak var tenant: Person?
    deinit { print("Apartment \(unit) is being deinitialized") }
}
```

*The strong references from the two variables (`john` and `unit4A`) and the links between the two instances are created as before:*

```swift
var john: Person?
var unit4A: Apartment?

john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")

john!.apartment = unit4A
unit4A!.tenant = john
```

*Here’s how the references look now that you’ve linked the two instances together:*

*![](https://docs.swift.org/swift-book/images/weakReference01@2x.png)*

*The `Person` instance still has a strong reference to the `Apartment` instance, but the `Apartment` instance now has a weak reference to the `Person` instance. This means that when you break the strong reference held by the `john` variable by setting it to `nil`, there are no more strong references to the `Person` instance:*

```swift
john = nil// Prints "John Appleseed is being deinitialized"
```

*Because there are no more strong references to the `Person` instance, it’s deallocated and the `tenant` property is set to `nil`:*

*![](https://docs.swift.org/swift-book/images/weakReference02@2x.png)*

*The only remaining strong reference to the `Apartment` instance is from the `unit4A` variable. If you break that strong reference, there are no more strong references to the `Apartment` instance:*

```swift
unit4A = nil// Prints "Apartment 4A is being deinitialized"
```

*Because there are no more strong references to the `Apartment` instance, it too is deallocated:*

*![](https://docs.swift.org/swift-book/images/weakReference03@2x.png)*

> *Note*
> 
> *In systems that use garbage collection, weak pointers are sometimes used to implement a simple caching mechanism because objects with no strong references are deallocated only when memory pressure triggers garbage collection. However, with ARC, values are deallocated as soon as their* last strong reference is removed, making weak references unsuitable for such a purpose.
