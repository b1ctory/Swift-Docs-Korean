## *Extensions : 확장*

*You can extend a class, structure, or enumeration in any access context in which the class, structure, or enumeration is available. Any type members added in an extension have the same default access level as type members declared in the original type being extended. If you extend a public or internal type, any new type members you add have a default access level of internal. If you extend a file-private type, any new type members you add have a default access level of file private. If you extend a private type, any new type members you add have a default access level of private.*

클래스, 구조체 또는 열거형을 사용할 수 있는 모든 액세스 컨텍스트에서 클래스, 구조체 또는 열거형을 확장할 수 있습니다. 확장에 추가된 모든 타입 구성원은 확장되는 원래 타입에서 선언된 타입 구성원과 동일한 기본 액세스 레벨을 가집니다. 퍼블릭 또는 내부 타입을 확장할 경우 추가하는 새 타입 구성원의 기본 액세스 레벨은 내부입니다. 파일-프라이빗 타입을 확장할 경우 추가하는 새 타입 구성원은 기본 액세스 레벨인 파일 프라이빗 타입을 가집니다. 프라이빗 타입을 확장할 경우 추가하는 새 타입 구성원의 기본 액세스 레벨은 개인입니다.

*Alternatively, you can mark an extension with an explicit access-level modifier (for example, `private`) to set a new default access level for all members defined within the extension. This new default can still be overridden within the extension for individual type members.*

또는 명시적 액세스 수준 한정자(예: `private`)로 확장을 표시하여 확장 내에 정의된 모든 구성원에 대한 새 기본 액세스 레벨을 설정할 수 있습니다. 이 새 기본값은 개별 타입 구성원에 대한 확장 내에서 계속 재정의할 수 있습니다.

*You can’t provide an explicit access-level modifier for an extension if you’re using that extension to add protocol conformance. Instead, the protocol’s own access level is used to provide the default access level for each protocol requirement implementation within the extension.*

확장을 사용하여 프로토콜 준수를 추가하는 경우 확장에 대한 명시적 액세스 레벨 한정자를 제공할 수 없습니다. 대신, 프로토콜의 자체 액세스 레벨은 확장 내의 각 프로토콜 요구사항 구현에 대한 기본 액세스 레벨을 제공하는 데 사용됩니다.

### *Private Members in Extensions : 프라이빗 멤버 확장*

*Extensions that are in the same file as the class, structure, or enumeration that they extend behave as if the code in the extension had been written as part of the original type’s declaration. As a result, you can:*

확장하는 클래스, 구조체 또는 열거형과 동일한 파일에 있는 확장명은 확장명의 코드가 원래 타입 선언의 일부로 작성된 것처럼 동작합니다. 결과적으로 다음을 수행할 수 있습니다:

- *Declare a private member in the original declaration, and access that member from extensions in the same file.*
  
  원래 선언에서 프라이빗 멤버를 선언하고, 동일한 파일의 확장자에서 해당 멤버에 액세스합니다.

- *Declare a private member in one extension, and access that member from another extension in the same file.*
  
  한 확장명에 프라이빗 멤버를 선언하고 동일한 파일에 있는 다른 확장명에서 해당 멤버에 액세스합니다.

- *Declare a private member in an extension, and access that member from the original declaration in the same file.*
  
  확장자에서 프라이빗 멤버를 선언하고 동일한 파일의 원래 선언에서 해당 멤버에 액세스합니다.

*This behavior means you can use extensions in the same way to organize your code, whether or not your types have private entities. For example, given the following simple protocol:*

이 동작은 타입에 개인 엔티티가 있는지 여부에 관계없이 동일한 방법으로 확장을 사용하여 코드를 구성할 수 있음을 의미합니다. 예를 들어, 다음과 같은 간단한 프로토콜이 제공됩니다:

```swift
protocol SomeProtocol {
    func doSomething()
}
```

*You can use an extension to add protocol conformance, like this:*

확장 기능을 사용하여 다음과 같은 프로토콜 준수를 추가할 수 있습니다:

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
