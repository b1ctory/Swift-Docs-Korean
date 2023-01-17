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

### *Two-Phase Initialization*

*Class initialization in Swift is a two-phase process. In the first phase, each stored property is assigned an initial value by the class that introduced it. Once the initial state for every stored property has been determined, the second phase begins, and each class is given the opportunity to customize its stored properties further before the new instance is considered ready for use.*

*The use of a two-phase initialization process makes initialization safe, while still giving complete flexibility to each class in a class hierarchy. Two-phase initialization prevents property values from being accessed before they’re initialized, and prevents property values from being set to a different value by another initializer unexpectedly.*

> *NOTE*
> 
> *Swift’s two-phase initialization process is similar to initialization in Objective-C. The main difference is that during phase 1, Objective-C assigns zero or null values (such as `0` or `nil`) to every property. Swift’s initialization flow is more flexible in that it lets you set custom initial values, and can cope with types for which `0` or `nil` isn’t a valid default value.*

*Swift’s compiler performs four helpful safety-checks to make sure that two-phase initialization is completed without error:*

***Safety check 1***

*A designated initializer must ensure that all of the properties introduced by its class are initialized before it delegates up to a superclass initializer.*

*As mentioned above, the memory for an object is only considered fully initialized once the initial state of all of its stored properties is known. In order for this rule to be satisfied, a designated initializer must make sure that all of its own properties are initialized before it hands off up the chain.*

***Safety check 2***

*A designated initializer must delegate up to a superclass initializer before assigning a value to an inherited property. If it doesn’t, the new value the designated initializer assigns will be overwritten by the superclass as part of its own initialization.*

***Safety check 3***

*A convenience initializer must delegate to another initializer before assigning a value to any property (including properties defined by the same class). If it doesn’t, the new value the convenience initializer assigns will be overwritten by its own class’s designated initializer.*

***Safety check 4***

*An initializer can’t call any instance methods, read the values of any instance properties, or refer to `self` as a value until after the first phase of initialization is complete.*

*The class instance isn’t fully valid until the first phase ends. Properties can only be accessed, and methods can only be called, once the class instance is known to be valid at the end of the first phase.*

*Here’s how two-phase initialization plays out, based on the four safety checks above:*

***Phase 1***

- *A designated or convenience initializer is called on a class.*

- *Memory for a new instance of that class is allocated. The memory isn’t yet initialized.*

- *A designated initializer for that class confirms that all stored properties introduced by that class have a value. The memory for these stored properties is now initialized.*

- *The designated initializer hands off to a superclass initializer to perform the same task for its own stored properties.*

- *This continues up the class inheritance chain until the top of the chain is reached.*

- *Once the top of the chain is reached, and the final class in the chain has ensured that all of its stored properties have a value, the instance’s memory is considered to be fully initialized, and phase 1 is complete.*

***Phase 2***

- *Working back down from the top of the chain, each designated initializer in the chain has the option to customize the instance further. Initializers are now able to access `self` and can modify its properties, call its instance methods, and so on.*

- *Finally, any convenience initializers in the chain have the option to customize the instance and to work with `self`.*

*Here’s how phase 1 looks for an initialization call for a hypothetical subclass and superclass:*

*![](https://docs.swift.org/swift-book/_images/twoPhaseInitialization01_2x.png)*

*In this example, initialization begins with a call to a convenience initializer on the subclass. This convenience initializer can’t yet modify any properties. It delegates across to a designated initializer from the same class.*

*The designated initializer makes sure that all of the subclass’s properties have a value, as per safety check 1. It then calls a designated initializer on its superclass to continue the initialization up the chain.*

*The superclass’s designated initializer makes sure that all of the superclass properties have a value. There are no further superclasses to initialize, and so no further delegation is needed.*

*As soon as all properties of the superclass have an initial value, its memory is considered fully initialized, and phase 1 is complete.*

*Here’s how phase 2 looks for the same initialization call:*

*![](https://docs.swift.org/swift-book/_images/twoPhaseInitialization01_2x.png)*

*The superclass’s designated initializer now has an opportunity to customize the instance further (although it doesn’t have to).*

*Once the superclass’s designated initializer is finished, the subclass’s designated initializer can perform additional customization (although again, it doesn’t have to).*

*Finally, once the subclass’s designated initializer is finished, the convenience initializer that was originally called can perform additional customization.*

## ### 0116

### *Initializer Inheritance and Overriding*

*Unlike subclasses in Objective-C, Swift subclasses don’t inherit their superclass initializers by default. Swift’s approach prevents a situation in which a simple initializer from a superclass is inherited by a more specialized subclass and is used to create a new instance of the subclass that isn’t fully or correctly initialized.*

> *NOTE*
> 
> *Superclass initializers are inherited in certain circumstances, but only when it’s safe and appropriate to do so. For more information, see [Automatic Initializer Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID222) below.*

*If you want a custom subclass to present one or more of the same initializers as its superclass, you can provide a custom implementation of those initializers within the subclass.*

*When you write a subclass initializer that matches a superclass designated initializer, you are effectively providing an override of that designated initializer. Therefore, you must write the `override` modifier before the subclass’s initializer definition. This is true even if you are overriding an automatically provided default initializer, as described in [Default Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID213).*

*As with an overridden property, method or subscript, the presence of the `override` modifier prompts Swift to check that the superclass has a matching designated initializer to be overridden, and validates that the parameters for your overriding initializer have been specified as intended.*

> *NOTE*
> 
> *You always write the `override` modifier when overriding a superclass designated initializer, even if your subclass’s implementation of the initializer is a convenience initializer.*

*Conversely, if you write a subclass initializer that matches a superclass convenience initializer, that superclass convenience initializer can never be called directly by your subclass, as per the rules described above in [Initializer Delegation for Class Types](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID219). Therefore, your subclass is not (strictly speaking) providing an override of the superclass initializer. As a result, you don’t write the `override` modifier when providing a matching implementation of a superclass convenience initializer.*

*The example below defines a base class called `Vehicle`. This base class declares a stored property called `numberOfWheels`, with a default `Int` value of `0`. The `numberOfWheels` property is used by a computed property called `description` to create a `String` description of the vehicle’s characteristics:*

```swift
class Vehicle {
    var numberOfWheels = 0
    var description: String {
        return "\(numberOfWheels) wheel(s)"
    }
}
```

*The `Vehicle` class provides a default value for its only stored property, and doesn’t provide any custom initializers itself. As a result, it automatically receives a default initializer, as described in [Default Initializers](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID213). The default initializer (when available) is always a designated initializer for a class, and can be used to create a new `Vehicle` instance with a `numberOfWheels` of `0`:*

```swift
let vehicle = Vehicle()
print("Vehicle: \(vehicle.description)")
// Vehicle: 0 wheel(s)
```

*The next example defines a subclass of `Vehicle` called `Bicycle`:*

```swift
class Bicycle: Vehicle {
    override init() {
        super.init()
        numberOfWheels = 2
    }
}
```

*The `Bicycle` subclass defines a custom designated initializer, `init()`. This designated initializer matches a designated initializer from the superclass of `Bicycle`, and so the `Bicycle` version of this initializer is marked with the `override` modifier.*

*The `init()` initializer for `Bicycle` starts by calling `super.init()`, which calls the default initializer for the `Bicycle` class’s superclass, `Vehicle`. This ensures that the `numberOfWheels` inherited property is initialized by `Vehicle` before `Bicycle` has the opportunity to modify the property. After calling `super.init()`, the original value of `numberOfWheels` is replaced with a new value of `2`.*

*If you create an instance of `Bicycle`, you can call its inherited `description` computed property to see how its `numberOfWheels` property has been updated:*

```swift
let bicycle = Bicycle()
print("Bicycle: \(bicycle.description)")
// Bicycle: 2 wheel(s)
```

*If a subclass initializer performs no customization in phase 2 of the initialization process, and the superclass has a synchronous, zero-argument designated initializer, you can omit a call to `super.init()` after assigning values to all of the subclass’s stored properties. If the superclass’s initializer is asynchronous, you need to write `await super.init()` explicitly.*

*This example defines another subclass of `Vehicle`, called `Hoverboard`. In its initializer, the `Hoverboard` class sets only its `color` property. Instead of making an explicit call to `super.init()`, this initializer relies on an implicit call to its superclass’s initializer to complete the process.*

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

```swift
let hoverboard = Hoverboard(color: "silver")
print("Hoverboard: \(hoverboard.description)")
// Hoverboard: 0 wheel(s) in a beautiful silver
```

> *NOTE*
> 
> *Subclasses can modify inherited variable properties during initialization, but can’t modify inherited constant properties.*

### *Automatic Initializer Inheritance*

*As mentioned above, subclasses don’t inherit their superclass initializers by default. However, superclass initializers are automatically inherited if certain conditions are met. In practice, this means that you don’t need to write initializer overrides in many common scenarios, and can inherit your superclass initializers with minimal effort whenever it’s safe to do so.*

*Assuming that you provide default values for any new properties you introduce in a subclass, the following two rules apply:*

***Rule 1***

*If your subclass doesn’t define any designated initializers, it automatically inherits all of its superclass designated initializers.*

***Rule 2***

*If your subclass provides an implementation of all of its superclass designated initializers—either by inheriting them as per rule 1, or by providing a custom implementation as part of its definition—then it automatically inherits all of the superclass convenience initializers.*

*These rules apply even if your subclass adds further convenience initializers.*

> *NOTE*
> 
> *A subclass can implement a superclass designated initializer as a subclass convenience initializer as part of satisfying rule 2.*

### *Designated and Convenience Initializers in Action*

*The following example shows designated initializers, convenience initializers, and automatic initializer inheritance in action. This example defines a hierarchy of three classes called `Food`, `RecipeIngredient`, and `ShoppingListItem`, and demonstrates how their initializers interact.*

*The base class in the hierarchy is called `Food`, which is a simple class to encapsulate the name of a foodstuff. The `Food` class introduces a single `String` property called `name` and provides two initializers for creating `Food` instances:*

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

*![](https://docs.swift.org/swift-book/_images/initializersExample01_2x.png)*

*Classes don’t have a default memberwise initializer, and so the `Food` class provides a designated initializer that takes a single argument called `name`. This initializer can be used to create a new `Food` instance with a specific name:*

```swift
let namedMeat = Food(name: "Bacon")
// namedMeat's name is "Bacon"
```

*The `init(name: String)` initializer from the `Food` class is provided as a designated initializer, because it ensures that all stored properties of a new `Food` instance are fully initialized. The `Food` class doesn’t have a superclass, and so the `init(name: String)` initializer doesn’t need to call `super.init()` to complete its initialization.*

*The `Food` class also provides a convenience initializer, `init()`, with no arguments. The `init()` initializer provides a default placeholder name for a new food by delegating across to the `Food` class’s `init(name: String)` with a `name` value of `[Unnamed]`:*

```swift
let mysteryMeat = Food()
// mysteryMeat's name is "[Unnamed]"
```

*The second class in the hierarchy is a subclass of `Food` called `RecipeIngredient`. The `RecipeIngredient` class models an ingredient in a cooking recipe. It introduces an `Int` property called `quantity` (in addition to the `name` property it inherits from `Food`) and defines two initializers for creating `RecipeIngredient` instances:*

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

*![](https://docs.swift.org/swift-book/_images/initializersExample02_2x.png)*

*The `RecipeIngredient` class has a single designated initializer, `init(name: String, quantity: Int)`, which can be used to populate all of the properties of a new `RecipeIngredient` instance. This initializer starts by assigning the passed `quantity` argument to the `quantity` property, which is the only new property introduced by `RecipeIngredient`. After doing so, the initializer delegates up to the `init(name: String)` initializer of the `Food` class. This process satisfies safety check 1 from [Two-Phase Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID220) above.*

*`RecipeIngredient` also defines a convenience initializer, `init(name: String)`, which is used to create a `RecipeIngredient` instance by name alone. This convenience initializer assumes a quantity of `1` for any `RecipeIngredient` instance that’s created without an explicit quantity. The definition of this convenience initializer makes `RecipeIngredient` instances quicker and more convenient to create, and avoids code duplication when creating several single-quantity `RecipeIngredient` instances. This convenience initializer simply delegates across to the class’s designated initializer, passing in a `quantity` value of `1`.*

*The `init(name: String)` convenience initializer provided by `RecipeIngredient` takes the same parameters as the `init(name: String)` designated initializer from `Food`. Because this convenience initializer overrides a designated initializer from its superclass, it must be marked with the `override` modifier (as described in [Initializer Inheritance and Overriding](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html#ID221)).*

*Even though `RecipeIngredient` provides the `init(name: String)` initializer as a convenience initializer, `RecipeIngredient` has nonetheless provided an implementation of all of its superclass’s designated initializers. Therefore, `RecipeIngredient` automatically inherits all of its superclass’s convenience initializers too.*

*In this example, the superclass for `RecipeIngredient` is `Food`, which has a single convenience initializer called `init()`. This initializer is therefore inherited by `RecipeIngredient`. The inherited version of `init()` functions in exactly the same way as the `Food` version, except that it delegates to the `RecipeIngredient` version of `init(name: String)` rather than the `Food` version.*

*All three of these initializers can be used to create new `RecipeIngredient` instances:*

```swift
let oneMysteryItem = RecipeIngredient()
let oneBacon = RecipeIngredient(name: "Bacon")
let sixEggs = RecipeIngredient(name: "Eggs", quantity: 6)
```

*The third and final class in the hierarchy is a subclass of `RecipeIngredient` called `ShoppingListItem`. The `ShoppingListItem` class models a recipe ingredient as it appears in a shopping list.*

*Every item in the shopping list starts out as “unpurchased”. To represent this fact, `ShoppingListItem` introduces a Boolean property called `purchased`, with a default value of `false`. `ShoppingListItem` also adds a computed `description` property, which provides a textual description of a `ShoppingListItem` instance:*

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

*Because it provides a default value for all of the properties it introduces and doesn’t define any initializers itself, `ShoppingListItem` automatically inherits all of the designated and convenience initializers from its superclass.*

*The figure below shows the overall initializer chain for all three classes:*

*![](https://docs.swift.org/swift-book/_images/initializersExample03_2x.png)*

*You can use all three of the inherited initializers to create a new `ShoppingListItem` instance:*

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
