## *Subclassing*

*You can subclass any class that can be accessed in the current access context and that’s defined in the same module as the subclass. You can also subclass any open class that’s defined in a different module. A subclass can’t have a higher access level than its superclass — for example, you can’t write a public subclass of an internal superclass.*

*In addition, for classes that are defined in the same module, you can override any class member (method, property, initializer, or subscript) that’s visible in a certain access context. For classes that are defined in another module, you can override any open class member.*

*An override can make an inherited class member more accessible than its superclass version. In the example below, class `A` is a public class with a file-private method called `someMethod()`. Class `B` is a subclass of `A`, with a reduced access level of “internal”. Nonetheless, class `B` provides an override of `someMethod()` with an access level of “internal”, which is higher than the original implementation of `someMethod()`:*

```swift
public class A {
    fileprivate func someMethod() {}
}

internal class B: A {
    override internal func someMethod() {}
}
```

*It’s even valid for a subclass member to call a superclass member that has lower access permissions than the subclass member, as long as the call to the superclass’s member takes place within an allowed access level context (that is, within the same source file as the superclass for a file-private member call, or within the same module as the superclass for an internal member call):*

```swift
public class A {
    fileprivate func someMethod() {}
}

internal class B: A {
    override internal func someMethod() {
        super.someMethod()
    }
}
```

*Because superclass `A` and subclass `B` are defined in the same source file, it’s valid for the `B` implementation of `someMethod()` to call `super.someMethod()`.*
