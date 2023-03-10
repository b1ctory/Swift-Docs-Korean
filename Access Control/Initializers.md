## *Initializers*

*Custom initializers can be assigned an access level less than or equal to the type that they initialize. The only exception is for required initializers (as defined in [Required Initializers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization#Required-Initializers)). A required initializer must have the same access level as the class it belongs to.*

*As with function and method parameters, the types of an initializer’s parameters can’t be more private than the initializer’s own access level.*

### *Default Initializers*

*As described in [Default Initializers](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization#Default-Initializers), Swift automatically provides a default initializer without any arguments for any structure or base class that provides default values for all of its properties and doesn’t provide at least one initializer itself.*

*A default initializer has the same access level as the type it initializes, unless that type is defined as `public`. For a type that’s defined as `public`, the default initializer is considered internal. If you want a public type to be initializable with a no-argument initializer when used in another module, you must explicitly provide a public no-argument initializer yourself as part of the type’s definition.*

### *Default Memberwise Initializers for Structure Types*

*The default memberwise initializer for a structure type is considered private if any of the structure’s stored properties are private. Likewise, if any of the structure’s stored properties are file private, the initializer is file private. Otherwise, the initializer has an access level of internal.*

*As with the default initializer above, if you want a public structure type to be initializable with a memberwise initializer when used in another module, you must provide a public memberwise initializer yourself as part of the type’s definition.*


