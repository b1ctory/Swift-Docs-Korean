## *Resolving Strong Reference Cycles Between Class Instances : 클래스 인스턴스 간의 강력한 참조 주기를 해결*

*Swift provides two ways to resolve strong reference cycles when you work with properties of class type: weak references and unowned references.*

Swift는 클래스 타입 프로퍼티로 작업할 때 강력한 참조 주기를 해결하는 두 가지 방법, 즉 약한 참조와 소유하지 않은 참조를 제공합니다.

*Weak and unowned references enable one instance in a reference cycle to refer to the other instance without keeping a strong hold on it. The instances can then refer to each other without creating a strong reference cycle.*

약하고 소유하지 않은 참조를 사용하면 참조 주기의 한 인스턴스가 강력하게 제어하지 않고 다른 인스턴스를 참조할 수 있습니다. 그러면 인스턴스가 강력한 참조 주기를 만들지 않고 서로 참조할 수 있습니다.*

*Use a weak reference when the other instance has a shorter lifetime — that is, when the other instance can be deallocated first. In the `Apartment` example above, it’s appropriate for an apartment to be able to have no tenant at some point in its lifetime, and so a weak reference is an appropriate way to break the reference cycle in this case. In contrast, use an unowned reference when the other instance has the same lifetime or a longer lifetime.*

다른 인스턴스의 수명이 짧은 경우, 즉 다른 인스턴스의 할당을 먼저 해제할 수 있는 경우 약한 참조를 사용합니다. 위의 `Apartment`의 예에서는 아파트가 수명의 어느 시점에 세입자가 없을 수 있는 것이 적절하므로, 이 경우 기준 주기를 깨기 위한 적절한 방법은 약한 기준입니다. 반대로 다른 인스턴스의 수명이 같거나 더 긴 경우 소유하지 않은 참조를 사용합니다.
