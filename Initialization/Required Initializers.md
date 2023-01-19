## *Required Initializers*

*Write the `required` modifier before the definition of a class initializer to indicate that every subclass of the class must implement that initializer:*

```swift
class SomeClass {
    required init() {
        // initializer implementation goes here
    }
}
```

*You must also write the `required` modifier before every subclass implementation of a required initializer, to indicate that the initializer requirement applies to further subclasses in the chain. You don’t write the `override` modifier when overriding a required designated initializer:*

```swift
class SomeSubclass: SomeClass {
    required init() {
        // subclass implementation of the required initializer goes here
    }
}
```

> *NOTE*
> 
> *You don’t have to provide an explicit implementation of a required initializer if you can satisfy the requirement with an inherited initializer.*
