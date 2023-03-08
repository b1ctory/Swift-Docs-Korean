## *Custom Types : 사용자 정의 타입*

*If you want to specify an explicit access level for a custom type, do so at the point that you define the type. The new type can then be used wherever its access level permits. For example, if you define a file-private class, that class can only be used as the type of a property, or as a function parameter or return type, in the source file in which the file-private class is defined.*

사용자 정의 타입에 대한 명시적 액세스 레벨을 지정하려면 타입을 정의하는 지점에서 지정하십시오. 그런 다음 액세스 수준이 허용하는 모든 곳에서 새 타입을 사용할 수 있습니다. 예를 들어 파일-프라이빗 클래스를 정의하는 경우 해당 클래스는 파일-프라이빗 클래스가 정의된 원본 파일에서 프로퍼티의 타입 또는 함수 매개 변수 또는 반환 타입으로만 사용할 수 있습니다.

*The access control level of a type also affects the default access level of that type’s members (its properties, methods, initializers, and subscripts). If you define a type’s access level as private or file private, the default access level of its members will also be private or file private. If you define a type’s access level as internal or public (or use the default access level of internal without specifying an access level explicitly), the default access level of the type’s members will be internal.*

타입의 접근 제어 단계는 해당 타입의 멤버(프로퍼티, 메서드, 초기화자 및 서브스크립트)의 기본 엑세스 단계에도 영향을 미칩니다. 타입의 접근 단계를 프라이빗 또는 파일-프라이빗으로 정의할 경우, 멤버의 기본 엑세스 레벨도 프라이빗 또는 파일-프라이빗이 됩니다. 타입의 접근 단계를 내부 또는 공용으로 정의하는 경우(또는 엑세스 레벨를 명시적으로 지정하지 않고 내부의 기본 엑세스 레벨을 사용하는 경우), 타입 멤버들의 기본엑세스 레벨은 내부가 됩니다.

> *Important*
> 
> *A public type defaults to having internal members, not public members. If you want a type member to be public, you must explicitly mark it as such. This requirement ensures that the public-facing API for a type is something you opt in to publishing, and avoids presenting the internal workings of a type as public API by mistake.*
> 
> 퍼블릭 타입은 기본적으로 퍼블릭 멤버가 아닌 내부 멤버를 가집니다. 타입 멤버를 퍼블릭으로 지정하려면 타입 멤버를 퍼블릭으로 명시해야 합니다. 이 요구사항은 타입에 대한 퍼블릭 API를 게시하기로 선택하고 실수로 타입의 내부 작업을 퍼블릭 API로 표시하지 않도록 합니다.

```swift
public class SomePublicClass {                  // explicitly public class
    public var somePublicProperty = 0            // explicitly public class member
    var someInternalProperty = 0                 // implicitly internal class member
    fileprivate func someFilePrivateMethod() {}  // explicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}

class SomeInternalClass {                       // implicitly internal class
    var someInternalProperty = 0                 // implicitly internal class member
    fileprivate func someFilePrivateMethod() {}  // explicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}

fileprivate class SomeFilePrivateClass {        // explicitly file-private class
    func someFilePrivateMethod() {}              // implicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}

private class SomePrivateClass {                // explicitly private class
    func somePrivateMethod() {}                  // implicitly private class member
}
```
