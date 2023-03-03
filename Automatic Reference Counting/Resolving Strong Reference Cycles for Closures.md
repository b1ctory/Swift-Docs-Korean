## *Resolving Strong Reference Cycles for Closures : 클로저에 대한 강한 순환 참조 해결*

*You resolve a strong reference cycle between a closure and a class instance by defining a capture list as part of the closure’s definition. A capture list defines the rules to use when capturing one or more reference types within the closure’s body. As with strong reference cycles between two class instances, you declare each captured reference to be a weak or unowned reference rather than a strong reference. The appropriate choice of weak or unowned depends on the relationships between the different parts of your code.*

클로저 정의의 일부로 캡처 목록을 정의하여 클로저와 클래스 인스턴스 간의 강력한 순환 참조를 해결합니다. 캡처 목록은 클로저 본문 내에서 하나 이상의 참조 타입을 캡처할 때 사용할 규칙을 정의합니다. 두 클래스 인스턴스 간의 강한 순환 참조와 마찬가지로 캡처된 각 참조를 강한 참조가 아닌 약한 참조 또는 미소유 참조로 선언합니다. 약함과 미소유의 적절한 선택은 코드의 다른 부분 간의 관계에 따라 다릅니다.

> *Note*
> 
> *Swift requires you to write `self.someProperty` or `self.someMethod()` (rather than just `someProperty` or `someMethod()`) whenever you refer to a member of `self` within a closure. This helps you remember that it’s possible to capture `self` by accident.*
> 
> Swift에서는 클로저 내에서 `self`의 멤버를 참조할 때마다 `self.someProperty` 또는 `self.someMethod()`를 작성해야 합니다. 이렇게 하면 실수로 `self`을 캡처할 수 있음을 기억하는 데 도움이 됩니다.
