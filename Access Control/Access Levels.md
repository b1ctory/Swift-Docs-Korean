## *Access Levels*

*Swift provides five different access levels for entities within your code. These access levels are relative to the source file in which an entity is defined, and also relative to the module that source file belongs to.*

- *Open access and public access enable entities to be used within any source file from their defining module, and also in a source file from another module that imports the defining module. You typically use open or public access when specifying the public interface to a framework. The difference between open and public access is described below.*

- *Internal access enables entities to be used within any source file from their defining module, but not in any source file outside of that module. You typically use internal access when defining an app’s or a framework’s internal structure.*

- *File-private access restricts the use of an entity to its own defining source file. Use file-private access to hide the implementation details of a specific piece of functionality when those details are used within an entire file.*

- *Private access restricts the use of an entity to the enclosing declaration, and to extensions of that declaration that are in the same file. Use private access to hide the implementation details of a specific piece of functionality when those details are used only within a single declaration.*

*Open access is the highest (least restrictive) access level and private access is the lowest (most restrictive) access level.*

*Open access applies only to classes and class members, and it differs from public access by allowing code outside the module to subclass and override, as discussed below in [Subclassing](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol#Subclassing). Marking a class as open explicitly indicates that you’ve considered the impact of code from other modules using that class as a superclass, and that you’ve designed your class’s code accordingly.*

### *Guiding Principle of Access Levels*

*Access levels in Swift follow an overall guiding principle: No entity can be defined in terms of another entity that has a lower (more restrictive) access level.*

*For example:*

- *A public variable can’t be defined as having an internal, file-private, or private type, because the type might not be available everywhere that the public variable is used.*

- *A function can’t have a higher access level than its parameter types and return type, because the function could be used in situations where its constituent types are unavailable to the surrounding code.*

*The specific implications of this guiding principle for different aspects of the language are covered in detail below.*
