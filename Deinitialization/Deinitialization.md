# *Deinitialization : 초기화해제*

*A deinitializer is called immediately before a class instance is deallocated. You write deinitializers with the `deinit` keyword, similar to how initializers are written with the `init` keyword. Deinitializers are only available on class types.*

`deinitializer`는 클래스 인스턴스가 할당 해제되기 직전에 호출됩니다. `init` 키워드로 이니셜라이저를 작성하는 것과 유사하게 `deinit` 키워드로 deinitializer를 작성합니다. Deinitializers는 클래스 타입에서만 사용할 수 있습니다.

## *How Deinitialization Works : 초기화 해제 작동 방식*

*Swift automatically deallocates your instances when they’re no longer needed, to free up resources. Swift handles the memory management of instances through automatic reference counting (ARC), as described in [Automatic Reference Counting](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html). Typically you don’t need to perform manual cleanup when your instances are deallocated. However, when you are working with your own resources, you might need to perform some additional cleanup yourself. For example, if you create a custom class to open a file and write some data to it, you might need to close the file before the class instance is deallocated.*

Swift는 더 이상 필요하지 않은 인스턴스를 자동으로 할당 해제하여 리소스를 확보합니다. Swift는 [링크](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)에 설명된 대로 자동 참조 계산(ARC)을 통해 인스턴스의 메모리 관리를 처리합니다. 일반적으로 인스턴스 할당이 취소되면 수동 정리를 수행할 필요가 없습니다. 그러나 자체 리소스로 작업하는 경우 일부 추가 정리를 직접 수행해야 할 수 있습니다. 예를 들어 사용자 지정 클래스를 만들어 파일을 열고 파일에 일부 데이터를 쓰는 경우 클래스 인스턴스의 할당이 취소되기 전에 파일을 닫아야 할 수 있습니다.

*Class definitions can have at most one deinitializer per class. The deinitializer doesn’t take any parameters and is written without parentheses:*

클래스 정의는 클래스당 최대 하나의 deinitializer를 가질 수 있습니다. deinitializer는 매개변수를 사용하지 않으며 괄호 없이 작성됩니다.

```swift
deinit {
    // perform the deinitialization
}
```

*Deinitializers are called automatically, just before instance deallocation takes place. You aren’t allowed to call a deinitializer yourself. Superclass deinitializers are inherited by their subclasses, and the superclass deinitializer is called automatically at the end of a subclass deinitializer implementation. Superclass deinitializers are always called, even if a subclass doesn’t provide its own deinitializer.*

deinitializer는 인스턴스 할당 해제가 발생하기 직전에 자동으로 호출됩니다. deinitializer를 직접 호출할 수 없습니다. 상위 클래스 초기화 deinitializer는 해당 하위 클래스에 의해 상속되며 상위 클래스 초기화 해제자는 하위 클래스 초기화 해제 구현이 끝날 때 자동으로 호출됩니다. 서브클래스가 자체적인 디이니셜라이저를 제공하지 않더라도 슈퍼클래스 deinitializer는 항상 호출됩니다.

*Because an instance isn’t deallocated until after its deinitializer is called, a deinitializer can access all properties of the instance it’s called on and can modify its behavior based on those properties (such as looking up the name of a file that needs to be closed).*

인스턴스는 deinitializer가 호출될 때까지 할당이 해제되지 않기 때문에 deinitializer는 호출된 인스턴스의 모든 프로퍼티에 액세스할 수 있으며 이러한 프로퍼티를 기반으로 동작을 수정할 수 있습니다. (닫혀야 하는 파일의 이름을 찾는 것과 같은)
