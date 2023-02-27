## *Resolving Strong Reference Cycles Between Class Instances*

*Swift provides two ways to resolve strong reference cycles when you work with properties of class type: weak references and unowned references.*

*Weak and unowned references enable one instance in a reference cycle to refer to the other instance without keeping a strong hold on it. The instances can then refer to each other without creating a strong reference cycle.*

*Use a weak reference when the other instance has a shorter lifetime — that is, when the other instance can be deallocated first. In the `Apartment` example above, it’s appropriate for an apartment to be able to have no tenant at some point in its lifetime, and so a weak reference is an appropriate way to break the reference cycle in this case. In contrast, use an unowned reference when the other instance has the same lifetime or a longer lifetime.*


