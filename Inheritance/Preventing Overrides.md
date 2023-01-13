## *Preventing Overrides : 재정의 방지*

*You can prevent a method, property, or subscript from being overridden by marking it as final. Do this by writing the `final` modifier before the method, property, or subscript’s introducer keyword (such as `final var`, `final func`, `final class func`, and `final subscript`).*

메서드, 프로퍼티 또는 서브스크립트를 final로 표시하여 재정의를 방지할 수 있습니다. 메서드, 프로퍼티 또는 서브스크립트의 introducer 키워드(예: `final var`, `final func`, `final class func` 및 `final subscript`) 앞에 `final` 수식어를 작성하여 이 작업을 수행합니다.

*Any attempt to override a final method, property, or subscript in a subclass is reported as a compile-time error. Methods, properties, or subscripts that you add to a class in an extension can also be marked as final within the extension’s definition.*

하위 클래스에서 최종 메서드, 프로퍼티 또는 서브스크립트를 재정의하려는 시도는 컴파일 타임 오류로 보고됩니다. 익스텐션의 클래스에 추가하는 메서드, 프로퍼티 또는 서브스크립트도 확장 정의 내에서 final로 표시할 수 있습니다.

*You can mark an entire class as final by writing the `final` modifier before the `class` keyword in its class definition (`final class`). Any attempt to subclass a final class is reported as a compile-time error.*

클래스 정의(`final class`)에서 `class` 키워드 앞에 `final` 수식어를 작성하여 전체 클래스를 `final`로 표시할 수 있습니다. 최종 클래스를 하위 클래스로 분류하려는 시도는 컴파일 타임 오류로 보고됩니다.


