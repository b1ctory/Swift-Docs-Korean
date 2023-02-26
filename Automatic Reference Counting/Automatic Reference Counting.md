# *Automatic Reference Counting : 자동 참조 카운팅*

*Model the lifetime of objects and their relationships.*

객체의 수명과 그 관계를 모델링합니다.

*Swift uses Automatic Reference Counting (ARC) to track and manage your app’s memory usage. In most cases, this means that memory management “just works” in Swift, and you don’t need to think about memory management yourself. ARC automatically frees up the memory used by class instances when those instances are no longer needed.*

Swift는 ARC(Automatic Reference Counting)를 사용하여 앱의 메모리 사용량을 추적하고 관리합니다. 대부분의 경우 이는 Swift에서 메모리 관리가 "그냥 작동"하고 메모리 관리에 대해 직접 생각할 필요가 없음을 의미합니다. ARC는 인스턴스가 더 이상 필요하지 않을 때 클래스 인스턴스에서 사용하는 메모리를 자동으로 해제합니다.

*However, in a few cases ARC requires more information about the relationships between parts of your code in order to manage memory for you. This chapter describes those situations and shows how you enable ARC to manage all of your app’s memory. Using ARC in Swift is very similar to the approach described in [Transitioning to ARC Release Notes](https://developer.apple.com/library/content/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html) for using ARC with Objective-C.*

그러나 ARC가 메모리를 관리하기 위해 코드 부분 간의 관계에 대한 자세한 정보를 요구하는 경우도 있습니다. 이 장에서는 이러한 상황에 대해 설명하고 ARC를 활성화하여 앱의 모든 메모리를 관리하는 방법을 보여줍니다. Swift에서 ARC를 사용하는 것은 Objective-C에서 ARC를 사용하는 경우 [링크]에서 설명한 접근 방식과 매우 유사합니다.

*Reference counting applies only to instances of classes. Structures and enumerations are value types, not reference types, and aren’t stored and passed by reference.*

참조 카운트는 클래스의 인스턴스에만 적용됩니다. 구조체 및 열거형은 참조 타입이 아닌 값 타입이며 참조에 의해 저장되고 전달되지 않습니다.

## *How ARC Works : ARC 작동 방식*

*Every time you create a new instance of a class, ARC allocates a chunk of memory to store information about that instance. This memory holds information about the type of the instance, together with the values of any stored properties associated with that instance.*

클래스의 새 인스턴스를 만들 때마다 ARC는 해당 인스턴스에 대한 정보를 저장하기 위해 메모리 청크를 할당합니다. 이 메모리는 해당 인스턴스와 연결된 모든 저장 프로퍼티의 값과 함께 인스턴스 타입에 대한 정보를 보유합니다.

*Additionally, when an instance is no longer needed, ARC frees up the memory used by that instance so that the memory can be used for other purposes instead. This ensures that class instances don’t take up space in memory when they’re no longer needed.*

또한 인스턴스가 더 이상 필요하지 않은 경우 ARC는 해당 인스턴스에서 사용하는 메모리를 해제하여 메모리를 다른 용도로 대신 사용할 수 있습니다. 이렇게 하면 클래스 인스턴스가 더 이상 필요하지 않을 때 메모리 공간을 차지하지 않습니다.

*However, if ARC were to deallocate an instance that was still in use, it would no longer be possible to access that instance’s properties, or call that instance’s methods. Indeed, if you tried to access the instance, your app would most likely crash.*

그러나 ARC가 아직 사용 중인 인스턴스를 할당 해제하면 더 이상 해당 인스턴스의 프로퍼티에 액세스하거나 해당 인스턴스의 메서드를 호출할 수 없습니다. 실제로 인스턴스에 액세스하려고 하면 앱이 충돌할 가능성이 큽니다.

*To make sure that instances don’t disappear while they’re still needed, ARC tracks how many properties, constants, and variables are currently referring to each class instance. ARC will not deallocate an instance as long as at least one active reference to that instance still exists.*

인스턴스가 여전히 필요한 동안 사라지지 않도록 ARC는 현재 각 클래스 인스턴스를 참조하는 프로퍼티, 상수 및 변수의 수를 추적합니다. ARC는 해당 인스턴스에 대한 활성 참조가 하나 이상 존재하는 한 인스턴스 할당을 취소하지 않습니다.

*To make this possible, whenever you assign a class instance to a property, constant, or variable, that property, constant, or variable makes a strong reference to the instance. The reference is called a “strong” reference because it keeps a firm hold on that instance, and doesn’t allow it to be deallocated for as long as that strong reference remains.*

이를 가능하게 하려면 클래스 인스턴스를 프로퍼티, 상수 또는 변수에 할당할 때마다 해당 프로퍼티, 상수 또는 변수가 인스턴스에 대한 강력한 참조를 만듭니다. 참조는 해당 인스턴스를 확고하게 유지하고 해당 강력한 참조가 남아 있는 한 할당 해제를 허용하지 않기 때문에 "강한" 참조라고 합니다.
