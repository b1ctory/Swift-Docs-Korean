## *Subclassing : 서브클래싱*

*You can subclass any class that can be accessed in the current access context and that’s defined in the same module as the subclass. You can also subclass any open class that’s defined in a different module. A subclass can’t have a higher access level than its superclass — for example, you can’t write a public subclass of an internal superclass.*

현재 액세스 컨텍스트에서 액세스할 수 있고 하위 클래스와 동일한 모듈에 정의된 모든 클래스를 하위 클래스로 만들 수 있습니다. 또한 다른 모듈에 정의된 모든 퍼블릭 클래스를 하위 클래스로 만들 수 있습니다. 서브클래스는 슈퍼클래스보다 높은 액세스 레벨을 가질 수 없습니다. 예를 들어 내부 슈퍼클래스의 퍼블릭 서브클래스를 작성할 수 없습니다.

*In addition, for classes that are defined in the same module, you can override any class member (method, property, initializer, or subscript) that’s visible in a certain access context. For classes that are defined in another module, you can override any open class member.*

또한 동일한 모듈에 정의된 클래스의 경우 특정 액세스 컨텍스트에서 볼 수 있는 모든 클래스 멤버(메서드, 프로퍼티, 이니셜라이저 또는 서브스크립트)를 재정의할 수 있습니다. 다른 모듈에 정의된 클래스의 경우 열려 있는 모든 클래스 멤버를 재정의할 수 있습니다.

*An override can make an inherited class member more accessible than its superclass version. In the example below, class `A` is a public class with a file-private method called `someMethod()`. Class `B` is a subclass of `A`, with a reduced access level of “internal”. Nonetheless, class `B` provides an override of `someMethod()` with an access level of “internal”, which is higher than the original implementation of `someMethod()`:*

재정의는 상속된 클래스 멤버가 해당 슈퍼클래스 버전보다 액세스하기 쉽도록 만들 수 있습니다. 아래 예에서 `A` 클래스는 `someMethod()`라는 파일 프라이빗 메서드가 있는 퍼블릭 클래스입니다. `B` 클래스는 `A`의 하위 클래스이며 액세스 레벨이 '내부'로 축소되었습니다. 그럼에도 불구하고 클래스 `B`는 `someMethod()`의 원래 구현보다 높은 '내부' 액세스 수준으로 `someMethod()`의 재정의를 제공합니다.

```swift
public class A {
    fileprivate func someMethod() {}
}

internal class B: A {
    override internal func someMethod() {}
}
```

*It’s even valid for a subclass member to call a superclass member that has lower access permissions than the subclass member, as long as the call to the superclass’s member takes place within an allowed access level context (that is, within the same source file as the superclass for a file-private member call, or within the same module as the superclass for an internal member call):*

슈퍼클래스 멤버에 대한 호출이 허용된 액세스 수준 컨텍스트 내에서(즉, 동일한 소스 파일 내에서 발생하는 한) 하위클래스 멤버가 하위클래스 멤버보다 액세스 권한이 낮은 슈퍼클래스 멤버를 호출하는 것도 유효합니다. 파일 프라이빗하위 클래스 멤버가 하위 클래스 멤버보다 낮은 액세스 권한을 가진 슈퍼 클래스 멤버를 호출하는 것은 허용된 액세스 수준 컨텍스트 내에서 슈퍼 클래스 멤버에 대한 호출이 이루어지는 한 유효합니다. (즉, 파일-프라이빗 멤버 호출의 경우 슈퍼클래스와 동일한 소스 파일 내에서 또는 내부 구성원 호출의 경우 슈퍼클래스와 동일한 모듈 내에서): 멤버 호출을 위한 슈퍼클래스 또는 내부 멤버 호출을 위한 슈퍼클래스와 동일한 모듈 내):

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

슈퍼클래스 `A`와 서브클래스 `B`가 동일한 소스 파일에 정의되어 있으므로 `B` 구현의 `someMethod()`에서 `super.someMethod()`를 호출하는 것이 유효합니다.
