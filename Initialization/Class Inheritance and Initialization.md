## *Class Inheritance and Initialization : 클래스 상속 및 초기화*

*All of a class’s stored properties—including any properties the class inherits from its superclass—must be assigned an initial value during initialization.*

클래스가 슈퍼클래스에서 상속하는 모든 프로퍼티를 포함한 클래스의 모든 저장 프로퍼티는 초기화 중에 초기 값을 할당해야 합니다.

*Swift defines two kinds of initializers for class types to help ensure all stored properties receive an initial value. These are known as designated initializers and convenience initializers.*

Swift는 모든 저장 프로퍼티가 초기 값을 수신할 수 있도록 클래스 타입 대해 두 가지 종류의 이니셜라이저를 정의합니다. 이를 지정된 이니셜라이저 및 편의 이니셜라이저라고 합니다.

### *Designated Initializers and Convenience Initializers : 지정된 이니셜라이저 및 편의 이니셜라이저입니다*

*Designated initializers are the primary initializers for a class. A designated initializer fully initializes all properties introduced by that class and calls an appropriate superclass initializer to continue the initialization process up the superclass chain.*

지정된 이니셜라이저는 클래스의 기본 이니셜라이저입니다. 지정된 이니셜라이저는 해당 클래스에 의해 도입된 모든 프로퍼티를 완전히 초기화하고 적절한 슈퍼클래스 이니셜라이저를 호출하여 슈퍼클래스 체인에서 초기화 프로세스를 계속합니다.

*Classes tend to have very few designated initializers, and it’s quite common for a class to have only one. Designated initializers are “funnel” points through which initialization takes place, and through which the initialization process continues up the superclass chain.*

클래스에는 지정된 이니셜라이저가 거의 없는 경향이 있으며 클래스가 하나만 있는 것은 매우 일반적입니다. 지정된 이니셜라이저는 초기화가 발생하고 초기화 프로세스가 슈퍼클래스 체인에서 계속되는 "funnel" 지점입니다.

*Every class must have at least one designated initializer. In some cases, this requirement is satisfied by inheriting one or more designated initializers from a superclass, as described in [Automatic Initializer Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID222) below.*

모든 클래스에는 지정된 이니셜라이저가 하나 이상 있어야 합니다. 경우에 따라 아래 [링크]에 설명된 대로 슈퍼 클래스에서 하나 이상의 지정된 이니셜라이저를 상속하여 이 요구 사항을 충족할 수 있습니다.

*Convenience initializers are secondary, supporting initializers for a class. You can define a convenience initializer to call a designated initializer from the same class as the convenience initializer with some of the designated initializer’s parameters set to default values. You can also define a convenience initializer to create an instance of that class for a specific use case or input value type.*

편리한 이니셜라이저는 클래스에 대한 이니셜라이저를 지원하는 보조 이니셜라이저입니다. 단축 이니셜라이저를 정의하여 지정된 이니셜라이저의 일부 매개 변수를 기본값으로 설정한 상태에서 단축 이니셜라이저와 동일한 클래스에서 지정된 이니셜라이저를 호출할 수 있습니다. 또한 특정 사용 사례 또는 입력 값 타입에 대한 해당 클래스의 인스턴스를 생성하는 단축 이니셜라이저를 정의할 수 있습니다.

*You don’t have to provide convenience initializers if your class doesn’t require them. Create convenience initializers whenever a shortcut to a common initialization pattern will save time or make initialization of the class clearer in intent.*

클래스에 필요하지 않은 경우에는 편리한 이니셜라이저를 제공하지 않아도 됩니다. 공통 초기화 패턴으로 바로 가기를 사용하면 시간을 절약하거나 클래스 초기화를 명확하게 만들 수 있습니다.

### *Syntax for Designated and Convenience Initializers : 지정 및 편의 초기화 구문*

*Designated initializers for classes are written in the same way as simple initializers for value types:*

클래스에 지정된 이니셜라이저는 값 타입에 대한 단순 이니셜라이저와 동일한 방식으로 작성됩니다:

```swift
init(parameters) {
    statements
}
```

*Convenience initializers are written in the same style, but with the `convenience` modifier placed before the `init` keyword, separated by a space:*
편의 이니셜라이저는 동일한 스타일로 작성되지만, `init` 키워드 앞에 `convenience` 수식어를 두고 공백으로 구분합니다:

```swift
convenience init(parameters) {
    statements
}
```

### *Initializer Delegation for Class Types : 클래스 타입에 대한 이니셜라이저 위임*

*To simplify the relationships between designated and convenience initializers, Swift applies the following three rules for delegation calls between initializers:*

Swift는 지정된 이니셜라이저와 편의 이니셜라이저간의 관계를 단순화하기 위해 이니셜라이저간 위임 호출에 다음 세 가지 규칙을 적용합니다:

***Rule 1***

*A designated initializer must call a designated initializer from its immediate superclass.*

지정 이니셜라이저는 지정된 이니셜라이저를 직접 슈퍼클래스에서 호출해야 합니다.

***Rule 2***

*A convenience initializer must call another initializer from the same class.*

편의 이니셜라이저는 같은 클래스의 다른 이니셜라이저를 호출해야 합니다.

***Rule 3***

*A convenience initializer must ultimately call a designated initializer.*

편의 이니셜라이저는 최종적으로 지정 이니셜라이저를 호출해야 합니다.

*A simple way to remember this is:*

이를 기억하는 간단한 방법은:

- *Designated initializers must always delegate up.*
  
  지정 이니셜라이저는 항상 위임해야 합니다.

- *Convenience initializers must always delegate across.*
  
  편의 이니셜라이저는 항상 위임해야 합니다.

*These rules are illustrated in the figure below:*

이러한 규칙은 아래 그림에 설명되어있습니다:

*![](https://docs.swift.org/swift-book/_images/initializerDelegation01_2x.png)*

*Here, the superclass has a single designated initializer and two convenience initializers. One convenience initializer calls another convenience initializer, which in turn calls the single designated initializer. This satisfies rules 2 and 3 from above. The superclass doesn’t itself have a further superclass, and so rule 1 doesn’t apply.*

여기서 슈퍼클래스는 단일 지정 이니셜라이저와 두 개의 편의 이니셜라이저를 가지고 있습니다. 한 편의 이니셜라이저는 다른 편의 이니셜라이저를 호출하고, 이는 다시 단일 지정된 이니셜라이저를 호출합니다. 이것은 위에서 본 규칙 2와 3을 충족합니다. 슈퍼클래스 자체는 더 이상의 슈퍼클래스를 가지고 있지 않기 때문에 규칙 1은 적용되지 않습니다.

*The subclass in this figure has two designated initializers and one convenience initializer. The convenience initializer must call one of the two designated initializers, because it can only call another initializer from the same class. This satisfies rules 2 and 3 from above. Both designated initializers must call the single designated initializer from the superclass, to satisfy rule 1 from above.*

이 그림의 하위 클래스에는 두 개의 지정된 이니셜라이저와 한 개의 편의 이니셜라이저가 있습니다. 편의 이니셜라이저는 동일한 클래스의 다른 이니셜라이저만 호출할 수 있으므로 지정된 두 개의 이니셜라이저 중 하나를 호출해야 합니다. 이것은 위에서 본 규칙 2와 3을 충족합니다. 두 지정된 이니셜라이저는 위에서 규칙 1을 충족하기 위해 슈퍼 클래스에서 단일 지정된 이니셜라이저를 호출해야 합니다.

> *NOTE*
> 
> *These rules don’t affect how users of your classes create instances of each class. Any initializer in the diagram above can be used to create a fully initialized instance of the class they belong to. The rules only affect how you write the implementation of the class’s initializers.*
> 
> 이러한 규칙은 클래스 사용자가 각 클래스의 인스턴스를 만드는 방법에 영향을 주지 않습니다. 위 다이어그램의 이니셜라이저를 사용하여 해당 클래스가 속한 클래스의 완전한 초기화 인스턴스를 만들 수 있습니다. 규칙은 클래스의 이니셜라이저 구현을 작성하는 방법에만 영향을 미칩니다.

*The figure below shows a more complex class hierarchy for four classes. It illustrates how the designated initializers in this hierarchy act as “funnel” points for class initialization, simplifying the interrelationships among classes in the chain:*

아래 그림은 4개의 클래스에 대한 더 복잡한 클래스 계층을 보여줍니다. 이 계층에서 지정 이니셜라이저가 클래스 초기화를 위한 "funnel" 지점처럼 작동하여 체인의 클래스 간 상호 관계를 단순화하는 방법을 보여줍니다:

*![](https://docs.swift.org/swift-book/_images/initializerDelegation02_2x.png)*

### *Two-Phase Initialization : 2단계 초기화*

*Class initialization in Swift is a two-phase process. In the first phase, each stored property is assigned an initial value by the class that introduced it. Once the initial state for every stored property has been determined, the second phase begins, and each class is given the opportunity to customize its stored properties further before the new instance is considered ready for use.*

Swift에서 클래스 초기화는 2단계 프로세스입니다. 첫 번째 단계에서 각 저장 프로퍼티는 해당 프로퍼티를 도입한 클래스에 의해 초기 값이 할당됩니다. 모든 저장 프로퍼티의 초기 상태가 결정되면 두 번째 단계가 시작되고 각 클래스는 새 인스턴스를 사용할 준비가 된 것으로 간주되기 전에 저장 프로퍼티를 추가로 사용자 지정할 수 있습니다.

*The use of a two-phase initialization process makes initialization safe, while still giving complete flexibility to each class in a class hierarchy. Two-phase initialization prevents property values from being accessed before they’re initialized, and prevents property values from being set to a different value by another initializer unexpectedly.*

2단계 초기화 프로세스를 사용하면 클래스 계층의 각 클래스에 완전한 유연성을 제공하면서도 초기화를 안전하게 수행할 수 있습니다. 2단계 초기화는 프로퍼티 값이 초기화되기 전에 액세스하는 것을 방지하고 다른 이니셜라이저가 프로퍼티 값을 예기치 않게 다른 값으로 설정하는 것을 방지합니다.

> *NOTE*
> 
> *Swift’s two-phase initialization process is similar to initialization in Objective-C. The main difference is that during phase 1, Objective-C assigns zero or null values (such as `0` or `nil`) to every property. Swift’s initialization flow is more flexible in that it lets you set custom initial values, and can cope with types for which `0` or `nil` isn’t a valid default value.*
> 
> Swift의 2단계 초기화 과정은 Objective-C의 초기화와 유사합니다. 주요 차이점은 1단계 동안 Objective-C가 모든 속성에 0 또는 null 값(예: `0` 또는 `nil`)을 할당한다는 것입니다. Swift의 초기화 흐름은 사용자 지정 초기값을 설정할 수 있고 `0` 또는 `nil`이 유효한 기본값이 아닌 타입을 처리할 수 있다는 점에서 더 유연합니다.

*Swift’s compiler performs four helpful safety-checks to make sure that two-phase initialization is completed without error:*

Swift의 컴파일러는 2단계 초기화가 오류 없이 완료되도록 다음과 같은 네 가지 유용한 안전 검사를 수행합니다:

***Safety check 1***

*A designated initializer must ensure that all of the properties introduced by its class are initialized before it delegates up to a superclass initializer.*

지정 이니셜라이저는 해당 클래스에서 도입한 모든 프로퍼티가 초기화되었는지 확인한 후 슈퍼 클래스 이니셜라이저에 위임해야 합니다.

*As mentioned above, the memory for an object is only considered fully initialized once the initial state of all of its stored properties is known. In order for this rule to be satisfied, a designated initializer must make sure that all of its own properties are initialized before it hands off up the chain.*

위에서 언급한 바와 같이, 객체의 메모리는 저장된 모든 프로퍼티의 초기 상태를 알고 난 후에만 완전히 초기화된 것으로 간주됩니다. 이 규칙을 충족하려면 지정된 이니셜라이저가 체인을 해제하기 전에 자신의 모든 프로퍼티가 초기화되었는지 확인해야 합니다.

***Safety check 2***

*A designated initializer must delegate up to a superclass initializer before assigning a value to an inherited property. If it doesn’t, the new value the designated initializer assigns will be overwritten by the superclass as part of its own initialization.*

지정 이니셜라이저는 상속된 프로퍼티에 값을 할당하기 전에 슈퍼클래스 이니셜라이저까지 위임해야 합니다. 그렇지 않으면 지정 이니셜라이저가 할당한 새 값이 자체 초기화의 일부로 슈퍼 클래스에 의해 덮어쓰이게 됩니다.

***Safety check 3***

*A convenience initializer must delegate to another initializer before assigning a value to any property (including properties defined by the same class). If it doesn’t, the new value the convenience initializer assigns will be overwritten by its own class’s designated initializer.*

편의 이니셜라이저는 프로퍼티(동일 클래스에서 정의된 프로퍼티 포함)에 값을 할당하기 전에 다른 이니셜라이저에 위임해야 합니다. 그렇지 않은 경우 편의 이니셜라이저가 할당한 새 값은 자체 클래스의 지정된 이니셜라이저에 의해 덮어씌어집니다.

***Safety check 4***

*An initializer can’t call any instance methods, read the values of any instance properties, or refer to `self` as a value until after the first phase of initialization is complete.*

이니셜라이저는 첫 번째 단계가 완료될 때까지 인스턴스 메서드를 호출하거나 인스턴스 프로퍼티의 값을 읽거나 `self`를 값으로 나타낼 수 없습니다.

*The class instance isn’t fully valid until the first phase ends. Properties can only be accessed, and methods can only be called, once the class instance is known to be valid at the end of the first phase.*

클래스 인스턴스는 첫 번째 단계가 끝날 때까지 완전히 유효하지 않습니다. 첫 번째 단계가 끝날 때 클래스 인스턴스가 유효한 것으로 알려진 경우에만 프로퍼티에 액세스할 수 있고 메서드를 호출할 수 있습니다

*Here’s how two-phase initialization plays out, based on the four safety checks above:*

위의 네 가지 안전 점검을 기준으로 2단계 초기화를 수행하는 방법은 다음과 같습니다:

***Phase 1***

- *A designated or convenience initializer is called on a class.*
  
  지정된 이니셜라이저 또는 편의 이니셜라이저 클래스에서 호출됩니다.

- *Memory for a new instance of that class is allocated. The memory isn’t yet initialized.*
  
  해당 클래스의 새 인스턴스에 대한 메모리가 할당됩니다. 메모리가 아직 초기화되지 않았습니다.

- *A designated initializer for that class confirms that all stored properties introduced by that class have a value. The memory for these stored properties is now initialized.*
  
  해당 클래스에 대해 지정된 이니셜라이저를 사용하면 해당 클래스에 의해 도입된 모든 저장 프로퍼티에 값이 있음을 확인할 수 있습니다. 이제 저장 프로퍼티의 메모리가 초기화됩니다.

- *The designated initializer hands off to a superclass initializer to perform the same task for its own stored properties.*
  
  지정된 이니셜라이저는 슈퍼클래스 이니셜라이저로 전달되어 자체 저장 프로퍼티에 대해 동일한 작업을 수행합니다.

- *This continues up the class inheritance chain until the top of the chain is reached.*
  
  이것은 체인의 맨 위에 도달할 때까지 클래스 상속 체인을 계속합니다.

- *Once the top of the chain is reached, and the final class in the chain has ensured that all of its stored properties have a value, the instance’s memory is considered to be fully initialized, and phase 1 is complete.*
  
  체인의 최상위에 도달하고 체인의 최종 클래스가 모든 저장 프로퍼티에 값이 있는지 확인하면 인스턴스의 메모리가 완전히 초기화된 것으로 간주되고 단계 1이 완료됩니다.

***Phase 2***

- *Working back down from the top of the chain, each designated initializer in the chain has the option to customize the instance further. Initializers are now able to access `self` and can modify its properties, call its instance methods, and so on.*
  
  체인의 맨 위에서 아래로 작업하면 체인의 각 지정된 이니셜라이저가 인스턴스를 추가로 사용자 지정할 수 있습니다. 이제 이니셜라이저는 `self`에 액세스할 수 있으며 프로퍼티를 수정하고 인스턴스 메서드를 호출하는 등의 작업을 수행할 수 있습니다.

- *Finally, any convenience initializers in the chain have the option to customize the instance and to work with `self`.*
  
  마지막으로 체인의 모든 편의 이니셜라이저는 인스턴스를 사용자 지정하고 `self`로 작업할 수 있는 옵션을 제공합니다.

*Here’s how phase 1 looks for an initialization call for a hypothetical subclass and superclass:*

다음은 1단계에서 가상의 하위 클래스 및 슈퍼 클래스에 대한 초기화 호출을 찾는 방법입니다:

*![](https://docs.swift.org/swift-book/_images/twoPhaseInitialization01_2x.png)*

*In this example, initialization begins with a call to a convenience initializer on the subclass. This convenience initializer can’t yet modify any properties. It delegates across to a designated initializer from the same class.*

이 예에서는 초기화가 하위 클래스의 편의 이니셜라이저에 대한 호출로 시작됩니다. 이 편의 이니셜라이저는 아직 프로퍼티를 수정할 수 없습니다. 같은 클래스의 지정된 이니셜라이저로 위임합니다.

*The designated initializer makes sure that all of the subclass’s properties have a value, as per safety check 1. It then calls a designated initializer on its superclass to continue the initialization up the chain.*

지정된 이니셜라이저는 Safety Check 1 에 따라 하위 클래스의 모든 프로퍼티에 값이 있는지 확인합니다. 그런 다음 슈퍼 클래스 위 에서 지정된 이니셜라이저를 호출하여 체인 초기화를 계속합니다.

*The superclass’s designated initializer makes sure that all of the superclass properties have a value. There are no further superclasses to initialize, and so no further delegation is needed.*

슈퍼클래스의 지정된 이니셜라이저는 모든 슈퍼클래스 프로퍼티에 값이 있는지 확인합니다. 초기화할 더 이상의 슈퍼클래스가 없으므로 더 이상 위임할 필요가 없습니다.

*As soon as all properties of the superclass have an initial value, its memory is considered fully initialized, and phase 1 is complete.*

슈퍼클래스의 모든 속성이 초기값을 갖는 즉시 메모리가 완전히 초기화된 것으로 간주되고 1단계가 완료됩니다.

*Here’s how phase 2 looks for the same initialization call:*

다음은 2단계에서 동일한 초기화 호출을 찾는 방법입니다:

*![](https://docs.swift.org/swift-book/_images/twoPhaseInitialization01_2x.png)*

*The superclass’s designated initializer now has an opportunity to customize the instance further (although it doesn’t have to).*

슈퍼 클래스의 지정 이니셜라이저는 이제 인스턴스를 추가로 사용자 지정할 수 있습니다(그럴 필요는 없지만).

*Once the superclass’s designated initializer is finished, the subclass’s designated initializer can perform additional customization (although again, it doesn’t have to).*

슈퍼클래스의 지정 이니셜라이저가 완료되면 서브클래스의 지정 이니셜라이저가 추가 커스터마이징을 수행할 수 있습니다. (단, 그럴 필요는 없습니다).

*Finally, once the subclass’s designated initializer is finished, the convenience initializer that was originally called can perform additional customization.*

마지막으로, 하위 클래스의 지정된 초기화가 완료되면 원래 호출되었던 편의 이니셜라이저가 추가적인 사용자 지정을 수행할 수 있습니다.

### *Initializer Inheritance and Overriding : 이니셜라이저 상속 및 오버라이딩*

*Unlike subclasses in Objective-C, Swift subclasses don’t inherit their superclass initializers by default. Swift’s approach prevents a situation in which a simple initializer from a superclass is inherited by a more specialized subclass and is used to create a new instance of the subclass that isn’t fully or correctly initialized.*

Objective-C의 하위 클래스와 달리 Swift 하위 클래스는 기본적으로 슈퍼 클래스 이니셜라이저를 상속하지 않습니다. Swift의 접근 방식은 슈퍼 클래스의 단순 이니셜라이저가 더 전문화된 하위 클래스에 의해 상속되는 상황을 방지하고 완전히 또는 올바르게 초기화되지 않은 하위 클래스의 새 인스턴스를 만드는데 사용됩니다.

> *NOTE*
> 
> *Superclass initializers are inherited in certain circumstances, but only when it’s safe and appropriate to do so. For more information, see [Automatic Initializer Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID222) below.*
> 
> 슈퍼클래스 이니셜라이저는 특정 상황에서 상속되지만 안전하고 적절한 경우에만 상속됩니다. 자세한 내용은 아래의 [Automatic Initializer Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#)를 참조하십세요.

*If you want a custom subclass to present one or more of the same initializers as its superclass, you can provide a custom implementation of those initializers within the subclass.*

사용자 정의 하위 클래스가 해당 슈퍼 클래스와 동일한 이니셜라이저 중 하나 이상을 제공하도록 하려면 하위 클래스 내에서 이러한 이니셜라이저의 사용자 정의 구현을 제공할 수 있습니다.

*When you write a subclass initializer that matches a superclass designated initializer, you are effectively providing an override of that designated initializer. Therefore, you must write the `override` modifier before the subclass’s initializer definition. This is true even if you are overriding an automatically provided default initializer, as described in [Default Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID213).*

슈퍼클래스 지정 이니셜라이저와 일치하는 서브클래스 이니셜라이저를 작성하면 지정된 이니셜라이저의 오버라이드를 효과적으로 제공하는 것입니다. 따라서 하위 클래스의 이니셜라이저 정의 앞에 `override` 수식어를 작성해야 합니다. 이것은 [Default Initializer](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#)에 설명된 대로 자동으로 제공된 기본 이니셜라이저를 재정의하는 경우에도 적용됩니다

*As with an overridden property, method or subscript, the presence of the `override` modifier prompts Swift to check that the superclass has a matching designated initializer to be overridden, and validates that the parameters for your overriding initializer have been specified as intended.*

오버라이드된 프로퍼티, 메서드 또는 서브스크립트와 마찬가지로 `override` 수식자가 있으면 Swift는 슈퍼클래스에 오버라이드할 지정된 이니셜라이저가 있는지 확인하고, 오버라이드된 이니셜라이저의 매개 변수가 의도한 대로 지정되었는지 확인합니다.

> *NOTE*
> 
> *You always write the `override` modifier when overriding a superclass designated initializer, even if your subclass’s implementation of the initializer is a convenience initializer.*
> 
> 슈퍼 클래스 지정 이니셜라이저를 재정의할 때 하위 클래스의 이니셜라이저 구현이 편의 이니셜라이저인 경우에도 항상 `override` 수식어를 작성합니다.

*Conversely, if you write a subclass initializer that matches a superclass convenience initializer, that superclass convenience initializer can never be called directly by your subclass, as per the rules described above in [Initializer Delegation for Class Types](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID219). Therefore, your subclass is not (strictly speaking) providing an override of the superclass initializer. As a result, you don’t write the `override` modifier when providing a matching implementation of a superclass convenience initializer.*

반대로 슈퍼클래스의 편의 이니셜라이저와 일치하는 하위 클래스 이니셜라이저를 작성하는 경우 위 [Initializer Delegation for Class Types](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#)에서 설명한 규칙에 따라 해당 슈퍼클래스의 편의 이니셜라이저를 하위 클래스에서 직접 호출할 수 없습니다. 따라서 하위 클래스는 (엄밀하게 말하면) 슈퍼 클래스 이니셜라이저의 재정의를 제공하지 않습니다. 따라서 슈퍼클래스의 편의 이니셜라이저의 일치 구현을 제공할 때는 `override` 수식어를 쓰지 않습니다.

*The example below defines a base class called `Vehicle`. This base class declares a stored property called `numberOfWheels`, with a default `Int` value of `0`. The `numberOfWheels` property is used by a computed property called `description` to create a `String` description of the vehicle’s characteristics:*

아래 예에서는 `Vehicle`이라는 기본 클래스를 정의합니다. 이 기본 클래스는 디폴트 값이 `Int`값 `0`인 `numberOfWheels`라는 저장 프로퍼티를 선언합니다. `numberOfWheels` 프로퍼티는 `description`이라는 연산 프로퍼티를 사용하여 차량의 특성에 대한 `String` 설명을 생성합니다:

```swift
class Vehicle {
    var numberOfWheels = 0
    var description: String {
        return "\(numberOfWheels) wheel(s)"
    }
}
```

*The `Vehicle` class provides a default value for its only stored property, and doesn’t provide any custom initializers itself. As a result, it automatically receives a default initializer, as described in [Default Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID213). The default initializer (when available) is always a designated initializer for a class, and can be used to create a new `Vehicle` instance with a `numberOfWheels` of `0`:*

`Vehicle` 클래스는 저장 프로퍼티에만 기본값을 제공하며 사용자 지정 이니셜라이저 자체는 제공하지 않습니다. 따라서 [Default Initializer](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID213)에 설명된 대로 기본 이니셜라이저가 자동으로 수신됩니다. 기본 이니셜라이저(사용 가능한 경우)는 항상 클래스에 대해 지정된 이니셜라이저이며, `numberOfWheels`가 `0`인 새 `Vehicle` 인스턴스를 만드는데 사용할 수 있습니다.

```swift
let vehicle = Vehicle()
print("Vehicle: \(vehicle.description)")
// Vehicle: 0 wheel(s)
```

*The next example defines a subclass of `Vehicle` called `Bicycle`:*

다음 예에서는 `Bicycle`이라는 `Vehicle`의 하위 클래스를 정의합니다:

```swift
class Bicycle: Vehicle {
    override init() {
        super.init()
        numberOfWheels = 2
    }
}
```

*The `Bicycle` subclass defines a custom designated initializer, `init()`. This designated initializer matches a designated initializer from the superclass of `Bicycle`, and so the `Bicycle` version of this initializer is marked with the `override` modifier.*

`Bicycle` 하위 클래스는 사용자 지정 이니셜라이저 `init()`를 정의합니다. 이 지정된 이니셜라이저는 `Bicycle`의 슈퍼클래스의 지정된 이니셜라이저와 일치하므로 이 이니셜라이저의 `Bicycle` 버전은 `override` 수식자로 표시됩니다.

*The `init()` initializer for `Bicycle` starts by calling `super.init()`, which calls the default initializer for the `Bicycle` class’s superclass, `Vehicle`. This ensures that the `numberOfWheels` inherited property is initialized by `Vehicle` before `Bicycle` has the opportunity to modify the property. After calling `super.init()`, the original value of `numberOfWheels` is replaced with a new value of `2`.*

`Bicycle`의 `init()` 이니셜라이저는 `Bicycle` 클래스의 슈퍼 클래스인 `Vehicle`의 기본 이니셜라이저를 호출하는 `super.init()`로 시작합니다. 이렇게 하면 `Bycycle`이 프로퍼티를 수정하기 전에 `numberOfWheels` 상속 프로퍼티가 `Vehicle`에 의해 초기화됩니다. `super.init()`을 호출한 후 `numberOfWheels`의 원래 값이 새 값 `2`로 대체되었습니다.

*If you create an instance of `Bicycle`, you can call its inherited `description` computed property to see how its `numberOfWheels` property has been updated:*

`Bicycle`의 인스턴스를 생성하는 경우 상속된 `description` 연산 프로퍼티를 호출하여 `numberOfWheels`가 어떻게 업데이트 되는지 확인할 수 있습니다.

```swift
let bicycle = Bicycle()
print("Bicycle: \(bicycle.description)")
// Bicycle: 2 wheel(s)
```

*If a subclass initializer performs no customization in phase 2 of the initialization process, and the superclass has a synchronous, zero-argument designated initializer, you can omit a call to `super.init()` after assigning values to all of the subclass’s stored properties. If the superclass’s initializer is asynchronous, you need to write `await super.init()` explicitly.*

하위 클래스 이니셜라이저가 초기화 프로세스의 단계 2에서 사용자 지정을 수행하지 않고 슈퍼 클래스에 동기식 0 인수 지정 이니셜라이저가 있는 경우 하위 클래스의 모든 저장 프로퍼티에 값을 할당한 후 `super.init()`에 대한 호출을 생략할 수 있습니다. 슈퍼클래스의 이니셜라이저가 비동기인 경우 `await super.init()`를 명시적으로 작성해야 합니다.

*This example defines another subclass of `Vehicle`, called `Hoverboard`. In its initializer, the `Hoverboard` class sets only its `color` property. Instead of making an explicit call to `super.init()`, this initializer relies on an implicit call to its superclass’s initializer to complete the process.*

이 예에서는 `Hoverboard`라고 하는 `Vehicle`의 다른 하위 클래스를 정의합니다. 이니셜라이저에서 `Hoverboard` 클래스는 `color` 프로퍼티만 설정합니다. 이 이니셜라이저는 `super.init()`에 명시적으로 호출하는 대신 슈퍼클래스의 이니셜라이저에 대한 암시적 호출에 의존하여 프로세스를 완료합니다.

```swift
class Hoverboard: Vehicle {
    var color: String
    init(color: String) {
        self.color = color
        // super.init() implicitly called here
    }
    override var description: String {
        return "\(super.description) in a beautiful \(color)"
    }
}
```

*An instance of `Hoverboard` uses the default number of wheels supplied by the `Vehicle` initializer.*

`Hoverboard` 인스턴스는 `Vehicle` 이니셜라이저에서 제공하는 기본 휠 수를 사용합니다.

```swift
let hoverboard = Hoverboard(color: "silver")
print("Hoverboard: \(hoverboard.description)")
// Hoverboard: 0 wheel(s) in a beautiful silver
```

> *NOTE*
> 
> *Subclasses can modify inherited variable properties during initialization, but can’t modify inherited constant properties.*
> 
> 하위 클래스는 초기화 중에 상속된 변수 프로퍼티를 수정할 수 있지만 상속된 상수 프로퍼티는 수정할 수 없습니다.

### *Automatic Initializer Inheritance : 자동 이니셜라이저 상속*

*As mentioned above, subclasses don’t inherit their superclass initializers by default. However, superclass initializers are automatically inherited if certain conditions are met. In practice, this means that you don’t need to write initializer overrides in many common scenarios, and can inherit your superclass initializers with minimal effort whenever it’s safe to do so.*

위에서 언급한 바와 같이 하위 클래스는 기본적으로 수퍼 클래스 이니셜라이저를 상속하지 않습니다. 그러나 특정 조건이 충족되면 슈퍼클래스 이니셜라이저가 자동으로 상속됩니다. 실제로 많은 일반적인 시나리오에서 초기화 오버라이드를 작성할 필요가 없으며, 안전할 때마다 최소한의 노력으로 슈퍼클래스 초기화를 상속할 수 있습니다.

*Assuming that you provide default values for any new properties you introduce in a subclass, the following two rules apply:*

하위 클래스에 도입하는 새 프로퍼티에 기본값을 제공한다고 가정하면 다음 두 가지 규칙이 적용됩니다:

***Rule 1***

*If your subclass doesn’t define any designated initializers, it automatically inherits all of its superclass designated initializers.*

하위 클래스가 지정된 이니셜라이저를 정의하지 않으면 모든 슈퍼클래스의 지정된 이니셜라이저를 자동으로 상속합니다.

***Rule 2***

*If your subclass provides an implementation of all of its superclass designated initializers—either by inheriting them as per rule 1, or by providing a custom implementation as part of its definition—then it automatically inherits all of the superclass convenience initializers.*

하위 클래스가 규칙 1에 따라 상속하거나 정의의 일부로 사용자 지정 구현을 제공하여 모든 슈퍼클래스 지정 이니셜라이저의 구현을 제공하는 경우 모든 슈퍼클래스의 편의 이니셜라이저를 자동으로 상속합니다.

*These rules apply even if your subclass adds further convenience initializers.*

이러한 규칙은 하위 클래스에 편리 이니셜라이저가 추가된 경우에도 적용됩니다.

> *NOTE*
> 
> *A subclass can implement a superclass designated initializer as a subclass convenience initializer as part of satisfying rule 2.*
> 
> 하위 클래스는 규칙 2를 충족하는 부분으로 슈퍼 클래스 지정 이니셜라이저를 하위 클래스 편의 이니셜라이저로 구현할 수 있습니다.

### *Designated and Convenience Initializers in Action*

*The following example shows designated initializers, convenience initializers, and automatic initializer inheritance in action. This example defines a hierarchy of three classes called `Food`, `RecipeIngredient`, and `ShoppingListItem`, and demonstrates how their initializers interact.*

다음 예제에서는 지정된 이니셜라이저, 편의 이니셜라이저 및 자동 이니셜라이저 상속이 수행 중인 상태를 보여 줍니다. 이 예에서는  `Food`, `RecipeIngredient`, 그리고 `ShoppingListItem`이라는 세 가지 클래스의 계층을 정의하고 이니셜라이저가 어떻게 상호 작용하는지 보여줍니다.

*The base class in the hierarchy is called `Food`, which is a simple class to encapsulate the name of a foodstuff. The `Food` class introduces a single `String` property called `name` and provides two initializers for creating `Food` instances:*

계층의 기본 클래스는 `Food`라는 이름으로, 식품의 이름을 캡슐화하는 간단한 클래스입니다. `Food` 클래스는 `name`이라는 단일 `String` 프로퍼티를 소개하고 `Food` 인스턴스를 만들기 위한 두 가지 초기화 도구를 제공합니다:

```swift
class Food {
    var name: String
    init(name: String) {
        self.name = name
    }
    convenience init() {
        self.init(name: "[Unnamed]")
    }
}
```

*The figure below shows the initializer chain for the `Food` class:*

아래 그림은 `Food` 클래스의 이니셜라이저 체인을 보여줍니다:

*![](https://docs.swift.org/swift-book/_images/initializersExample01_2x.png)*

*Classes don’t have a default memberwise initializer, and so the `Food` class provides a designated initializer that takes a single argument called `name`. This initializer can be used to create a new `Food` instance with a specific name:*

클래스에는 기본 멤버별 이니셜라이저가 없으므로 `Food` 클래스는 `name`이라는 단일 인수를 사용하는 지정 이니셜라이저를 제공합니다. 이 이니셜라이저를 사용하여 다음과 같은 특정 이름의 새 `Food` 인스턴스를 만들 수 있습니다:

```swift
let namedMeat = Food(name: "Bacon")
// namedMeat's name is "Bacon"
```

*The `init(name: String)` initializer from the `Food` class is provided as a designated initializer, because it ensures that all stored properties of a new `Food` instance are fully initialized. The `Food` class doesn’t have a superclass, and so the `init(name: String)` initializer doesn’t need to call `super.init()` to complete its initialization.*

`Food` 클래스의 `init(name: String)` 이니셜라이저는 새로운 `Food` 인스턴스의 모든 저장 프로퍼티가 완전히 초기화되도록 하기 때문에 지정 이니셜라이저로 제공됩니다. `Food` 클래스에는 슈퍼 클래스가 없으므로 `init(name: String)` 이니셜라이저는 `super.init()`을 호출하여 초기화를 완료할 필요가 없습니다.

*The `Food` class also provides a convenience initializer, `init()`, with no arguments. The `init()` initializer provides a default placeholder name for a new food by delegating across to the `Food` class’s `init(name: String)` with a `name` value of `[Unnamed]`:*

`Food` 클래스는 또한 인수 없이 `init()`이라는 편의 이니셜라이저를 제공합니다. `init()` 이니셜라이저는 `name`값이 `[Unnamed]`인 `Food` 클래스의 `init(name:String)`에 위임하여 새 식품의 기본 placeholder 이름을 제공합니다:

```swift
let mysteryMeat = Food()
// mysteryMeat's name is "[Unnamed]"
```

*The second class in the hierarchy is a subclass of `Food` called `RecipeIngredient`. The `RecipeIngredient` class models an ingredient in a cooking recipe. It introduces an `Int` property called `quantity` (in addition to the `name` property it inherits from `Food`) and defines two initializers for creating `RecipeIngredient` instances:*

이 계층의 두 번째 클래스는 `RecipeIngredient`라는 식품의 하위 클래스 입니다. `RecipeIngredient`는 요리 레시피의 재료를 모델로 합니다. 여기에는 `quantity`라는 `Int` 프로퍼티(`Food`에서 상속되는 `name` 프로퍼티 외에도)이 도입되고 `RecipeInderent` 인스턴스를 생성하기 위한 두 가지 이니셜라이저가 정의됩니다:

```swift
class RecipeIngredient: Food {
    var quantity: Int
    init(name: String, quantity: Int) {
        self.quantity = quantity
        super.init(name: name)
    }
    override convenience init(name: String) {
        self.init(name: name, quantity: 1)
    }
}
```

*The figure below shows the initializer chain for the `RecipeIngredient` class:*

아래 그림은 `RecipeIngredient` 클래스의 이니셜라이저 체인을 보여줍니다:

*![](https://docs.swift.org/swift-book/_images/initializersExample02_2x.png)*

*The `RecipeIngredient` class has a single designated initializer, `init(name: String, quantity: Int)`, which can be used to populate all of the properties of a new `RecipeIngredient` instance. This initializer starts by assigning the passed `quantity` argument to the `quantity` property, which is the only new property introduced by `RecipeIngredient`. After doing so, the initializer delegates up to the `init(name: String)` initializer of the `Food` class. This process satisfies safety check 1 from [Two-Phase Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID220) above.*

`RecipeIncomponent` 클래스에는 새 `RecipeIncomponent` 인스턴스의 모든 프로퍼티를 채우는 데 사용할 수 있는 단일 지정 이니셜라이저 `init(name: String, quantity: Int)`가 있습니다. 이 이니셜라이저는 통과된 `quantity` 인수를 `RecipeIngredient` 가 도입한 유일한 새 프로퍼티인 `quantity` 프로퍼티에 할당하는 것으로 시작합니다. 이렇게 하면 이니셜라이저는 `Food` 클래스의 `init(name: String)` 이니셜라이저를 위임합니다. 이 프로세스는 위의 [Two-Phase Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#)의 안전 점검 1을 충족합니다.

*`RecipeIngredient` also defines a convenience initializer, `init(name: String)`, which is used to create a `RecipeIngredient` instance by name alone. This convenience initializer assumes a quantity of `1` for any `RecipeIngredient` instance that’s created without an explicit quantity. The definition of this convenience initializer makes `RecipeIngredient` instances quicker and more convenient to create, and avoids code duplication when creating several single-quantity `RecipeIngredient` instances. This convenience initializer simply delegates across to the class’s designated initializer, passing in a `quantity` value of `1`.*

`RecipeIncomponent`는 또한 이름만으로 `RecipeIncomponent` 인스턴스를 만드는 데 사용되는 편의 이니셜라이저인 `init(name: String)`를 정의합니다. 이 편의 이니셜라이저는 명시적인 양 없이 생성된 모든 `RecipeIncomponent` 인스턴스에 대해 `1`의 양을 가정합니다. 이 편의 이니셜라이저의 정의를 통해 `RecipeIncredent` 인스턴스를 더 빠르고 쉽게 만들 수 있으며, 단일 수량의 `RecipeIncredent` 인스턴스를 여러 개 만들 때 코드 중복을 방지할 수 있습니다. 이 편의 이니셜라이저는 클래스의 지정된 이니셜라이저에 `quantity` 값 `1`을 전달하는 것만으로 위임됩니다.

*The `init(name: String)` convenience initializer provided by `RecipeIngredient` takes the same parameters as the `init(name: String)` designated initializer from `Food`. Because this convenience initializer overrides a designated initializer from its superclass, it must be marked with the `override` modifier (as described in [Initializer Inheritance and Overriding](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID221)).*

`RecipeIncient`에서 제공하는 `init(name:String)` 편의 이니셜라이저는 `Food`의 `init(name:String)` 지정 이니셜라이저와 동일한 매개 변수를 취합니다. 이 편의 이니셜라이저는 지정된 이니셜라이저를 슈퍼클래스에서 재정의하므로 [Initializer Inheritance and Overriding](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#)에 설명된 대로 `override` 수식자로 표시해야 합니다.

*Even though `RecipeIngredient` provides the `init(name: String)` initializer as a convenience initializer, `RecipeIngredient` has nonetheless provided an implementation of all of its superclass’s designated initializers. Therefore, `RecipeIngredient` automatically inherits all of its superclass’s convenience initializers too.*

`RecipeIncomplement`는 `init(name: String)` 이니셜라이저를 편의 이니셜라이저로 제공하지만, `RecipeIncomplement`는 슈퍼클래스의 지정된 이니셜라이저를 모두 구현했습니다. 따라서 `RecipeIngredient`는 슈퍼클래스의 모든 편의 이니셜라이저 기능을 자동으로 이어받습니다.

*In this example, the superclass for `RecipeIngredient` is `Food`, which has a single convenience initializer called `init()`. This initializer is therefore inherited by `RecipeIngredient`. The inherited version of `init()` functions in exactly the same way as the `Food` version, except that it delegates to the `RecipeIngredient` version of `init(name: String)` rather than the `Food` version.*

이 예에서 `RecipeIngredient`의 슈퍼 클래스는 `Food`로, `init()`이라는 단일 편의 이니셜라이저를 가지고 있습니다. 따라서 이 이니셜라이저는 `RecipeIngredient`에 의해 상속됩니다. 상속된 버전의 `init()`은 `Food` 버전이 아닌 `init(name: String)`의 `RecipeIngredient` 버전에 위임된다는 점을 제외하고는 `Food` 버전과 정확히 동일한 방식으로 작동합니다.

*All three of these initializers can be used to create new `RecipeIngredient` instances:*

이러한 세 가지 초기화 도구를 모두 사용하여 새 `RecipeIncomponent` 인스턴스를 만들 수 있습니다:

```swift
let oneMysteryItem = RecipeIngredient()
let oneBacon = RecipeIngredient(name: "Bacon")
let sixEggs = RecipeIngredient(name: "Eggs", quantity: 6)
```

*The third and final class in the hierarchy is a subclass of `RecipeIngredient` called `ShoppingListItem`. The `ShoppingListItem` class models a recipe ingredient as it appears in a shopping list.*

계층의 세 번째이자 마지막 클래스는 `ShoppingListItem`으로 불리는 `RecipeIngredient`의 하위 클래스입니다. `ShoppingListItem` 클래스는 쇼핑 목록에 표시되는 레시피 재료를 모델링합니다.

*Every item in the shopping list starts out as “unpurchased”. To represent this fact, `ShoppingListItem` introduces a Boolean property called `purchased`, with a default value of `false`. `ShoppingListItem` also adds a computed `description` property, which provides a textual description of a `ShoppingListItem` instance:*

쇼핑 목록의 모든 품목은 "unpurchased"로 시작합니다. 이 사실을 나타내기 위해 `ShoppingListItem`은 기본값이 `false`인 `purchased`라는 Bool 프로퍼티를 도입합니다. `ShoppingListItem`은 `ShoppingListItem` 인스턴스에 대한 텍스트 설명을 제공하는 연산 프로퍼티 `description`도 추가합니다:

```swift
class ShoppingListItem: RecipeIngredient {
    var purchased = false
    var description: String {
        var output = "\(quantity) x \(name)"
        output += purchased ? " ✔" : " ✘"
        return output
    }
}
```

> *NOTE*
> 
> *`ShoppingListItem` doesn’t define an initializer to provide an initial value for `purchased`, because items in a shopping list (as modeled here) always start out unpurchased.*
> 
> `ShoppingListItem`(여기서 모델링한 대로)은 항상 구매되지 않은 상태로 시작하기 때문에 `purchased`에 대한 초기 값을 제공하는 이니셜라이저를 정의하지 않습니다.

*Because it provides a default value for all of the properties it introduces and doesn’t define any initializers itself, `ShoppingListItem` automatically inherits all of the designated and convenience initializers from its superclass.*

`ShoppingListItem`은 도입하는 모든 프로퍼티에 기본값을 제공하며 이니셜라이저 자체를 정의하지 않기 때문에 슈퍼클래스에서 지정된 모든 편의 이니셜라이저를 자동으로 상속합니다.

*The figure below shows the overall initializer chain for all three classes:*

아래 그림은 세 가지 클래스 모두에 대한 전체 이니셜라이저 체인을 보여줍니다:

*![](https://docs.swift.org/swift-book/_images/initializersExample03_2x.png)*

*You can use all three of the inherited initializers to create a new `ShoppingListItem` instance:*

세 가지 상속된 이니셜라이저를 모두 사용하여 새 `ShoppingListItem` 인스턴스를 만들 수 있습니다:

```swift
var breakfastList = [
    ShoppingListItem(),
    ShoppingListItem(name: "Bacon"),
    ShoppingListItem(name: "Eggs", quantity: 6),
]
breakfastList[0].name = "Orange juice"
breakfastList[0].purchased = true
for item in breakfastList {
    print(item.description)
}
// 1 x Orange juice ✔
// 1 x Bacon ✘
// 6 x Eggs ✘
```

*Here, a new array called `breakfastList` is created from an array literal containing three new `ShoppingListItem` instances. The type of the array is inferred to be `[ShoppingListItem]`. After the array is created, the name of the `ShoppingListItem` at the start of the array is changed from `"[Unnamed]"` to `"Orange juice"` and it’s marked as having been purchased. Printing the description of each item in the array shows that their default states have been set as expected.*

여기서 `breakfastList`라는 새 배열은 세 개의 새 `ShoppingListItem` 인스턴스를 포함하는 배열 리터럴에서 생성됩니다. 배열의 타입은 `[ShoppingListItem]`으로 유추됩니다. 배열이 생성되면 배열 시작 부분에 있는 `ShoppingListItem`의 이름이 `"[Unnamed]"`에서 `"Orange juice"`로 변경되고 구입한 것으로 표시됩니다. 배열의 각 항목에 대한 설명을 출력하면 해당 항목의 기본 상태가 예상대로 설정되었음을 나타냅니다.
