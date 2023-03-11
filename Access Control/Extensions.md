## *Extensions*

*You can extend a class, structure, or enumeration in any access context in which the class, structure, or enumeration is available. Any type members added in an extension have the same default access level as type members declared in the original type being extended. If you extend a public or internal type, any new type members you add have a default access level of internal. If you extend a file-private type, any new type members you add have a default access level of file private. If you extend a private type, any new type members you add have a default access level of private.*

*Alternatively, you can mark an extension with an explicit access-level modifier (for example, `private`) to set a new default access level for all members defined within the extension. This new default can still be overridden within the extension for individual type members.*

*You can’t provide an explicit access-level modifier for an extension if you’re using that extension to add protocol conformance. Instead, the protocol’s own access level is used to provide the default access level for each protocol requirement implementation within the extension.*

### *Private Members in Extensions*

*Extensions that are in the same file as the class, structure, or enumeration that they extend behave as if the code in the extension had been written as part of the original type’s declaration. As a result, you can:*

- *Declare a private member in the original declaration, and access that member from extensions in the same file.*

- *Declare a private member in one extension, and access that member from another extension in the same file.*

- *Declare a private member in an extension, and access that member from the original declaration in the same file.*

*This behavior means you can use extensions in the same way to organize your code, whether or not your types have private entities. For example, given the following simple protocol:*

```swift
protocol SomeProtocol {
    func doSomething()
}
```

*You can use an extension to add protocol conformance, like this:*

```swift
struct SomeStruct {
    private var privateVariable = 12
}

extension SomeStruct: SomeProtocol {
    func doSomething() {
        print(privateVariable)
    }
}
```
