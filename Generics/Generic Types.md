## *Generic Types : 제네릭 타입*

*In addition to generic functions, Swift enables you to define your own generic types. These are custom classes, structures, and enumerations that can work with any type, in a similar way to `Array` and `Dictionary`.*

Swift를 사용하면 제네릭 함수 외에도 자신만의 제네릭 타입을 정의할 수 있습니다. 이러한 클래스, 구조체 및 열거형은 `Array` 및 `Dictionary`와 유사한 방식으로 모든 타입에서 작동할 수 있습니다.

*This section shows you how to write a generic collection type called `Stack`. A stack is an ordered set of values, similar to an array, but with a more restricted set of operations than Swift’s `Array` type. An array allows new items to be inserted and removed at any location in the array. A stack, however, allows new items to be appended only to the end of the collection (known as pushing a new value on to the stack). Similarly, a stack allows items to be removed only from the end of the collection (known as popping a value off the stack).*

이 섹션에서는 `Stack`이라는 일반 컬렉션 타입을 작성하는 방법을 보여 줍니다. 스택은 배열과 유사하지만 Swift의 `Array` 타입보다 더 제한된 작업 집합을 가진 순서가 지정된 값 집합입니다. 배열을 사용하면 배열의 모든 위치에서 새 항목을 삽입하고 제거할 수 있습니다. 그러나 스택을 사용하면 컬렉션 끝에만 새 항목을 추가할 수 있습니다(새 값을 스택에 푸시하는 것으로 알려져 있음). 마찬가지로 스택을 사용하면 컬렉션 끝에서만 항목을 제거할 수 있습니다(스택에서 값을 팝핑하는 것으로 알려져 있음).

> *Note*
> 
> *The concept of a stack is used by the `UINavigationController` class to model the view controllers in its navigation hierarchy. You call the `UINavigationController` class `pushViewController(_:animated:)` method to add (or push) a view controller on to the navigation stack, and its `popViewControllerAnimated(_:)` method to remove (or pop) a view controller from the navigation stack. A stack is a useful collection model whenever you need a strict “last in, first out” approach to managing a collection.*
> 
> 스택의 개념은 `UINavigationController` 클래스에서 탐색 계층 구조의 보기 컨트롤러를 모델링하는 데 사용됩니다. `UINavigationController` 클래스의 `pushViewController(_:animated:)` 메서드를 호출하여 탐색 스택에 뷰 컨트롤러를 추가(또는 푸시)하고 `popViewControllerAnimated(_:)` 메서드를 호출하여 뷰를 제거(또는 팝)합니다. 탐색 스택의 컨트롤러. 스택은 컬렉션 관리에 엄격한 "후입선출" 접근 방식이 필요할 때마다 유용한 컬렉션 모델입니다.

*The illustration below shows the push and pop behavior for a stack:*

아래의 그림은 스택의 푸시, 팝 행위를 보여줍니다.

![](https://docs.swift.org/swift-book/images/stackPushPop~dark@2x.png)

1. *There are currently three values on the stack.*
   
   현재 스택에 3개의 값이 들어있습니다.

2. *A fourth value is pushed onto the top of the stack.*
   
   네번째 값은 스택의 맨 위에 푸시됩니다.

3. *The stack now holds four values, with the most recent one at the top.*
   
   이제 스택은 가장 최근 값이 맨 위에 오도록 4개의 값을 보유합니다.

4. *The top item in the stack is popped.*
   
   스택 맨 위 아이템이 팝 되었습니다.

5. *After popping a value, the stack once again holds three values.*
   
   값을 팝핑한 이후, 스택은 다시 세개의 값을 가지고 있습니다.

*Here’s how to write a nongeneric version of a stack, in this case for a stack of `Int` values:*

제네릭이 아닌 버전의 스택을 작성하는 방법은 다음과 같습니다. 이 경우에는 `Int` 값의 스택에 대한 것입니다.

```swift
struct IntStack {
    var items: [Int] = []
    mutating func push(_ item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
}
```

*This structure uses an `Array` property called `items` to store the values in the stack. `Stack` provides two methods, `push` and `pop`, to push and pop values on and off the stack. These methods are marked as `mutating`, because they need to modify (or mutate) the structure’s `items` array.*

이 구조체는 스택에 값을 저장하기 위해 `items`라는 `Array` 프로퍼티를 사용합니다. `Stack`은 값을 스택 안팎으로 푸시하고 팝하는 두 가지 방법인 `push` 및 `pop`을 제공합니다. 이러한 메서드는 구조체의 `items` 배열을 수정(또는 변경)해야 하므로 `mutating`으로 표시됩니다.

*The `IntStack` type shown above can only be used with `Int` values, however. It would be much more useful to define a generic `Stack` structure, that can manage a stack of any type of value.*

그러나 위에 표시된 `IntStack` 타입은 `Int` 값에만 사용할 수 있습니다. 모든 타입의 값 스택을 관리할 수 있는 일반적인 `Stack` 구조체를 정의하는 것이 훨씬 더 유용할 것입니다.

*Here’s a generic version of the same code:*

동일한 코드의 제네릭 버전은 다음과 같습니다.

```swift
struct Stack<Element> {
    var items: [Element] = []
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
```

*Note how the generic version of `Stack` is essentially the same as the nongeneric version, but with a type parameter called `Element` instead of an actual type of `Int`. This type parameter is written within a pair of angle brackets (`<Element>`) immediately after the structure’s name.*

`Stack`의 제네릭 버전은 기본적으로 제네릭이 아닌 버전과 동일하지만 `Int`의 실제 타입 대신 `Element`라는 타입 매개변수가 있습니다. 이 타입 매개변수는 구조체 이름 바로 뒤에 있는 한 쌍의 꺽쇠 괄호(`<Element>`) 안에 작성됩니다.

*`Element` defines a placeholder name for a type to be provided later. This future type can be referred to as `Element` anywhere within the structure’s definition. In this case, `Element` is used as a placeholder in three places:*

`Element`는 나중에 제공할 타입의 플레이스홀더 이름을 정의합니다. 이 미래 타입은 구조체 정의 내 어디에서나 `Element`라고 할 수 있습니다. 이 경우 `Element`는 다음 세 위치에서 플레이스홀더로 사용됩니다.

- *To create a property called `items`, which is initialized with an empty array of values of type `Element`*
  
  `Element` 타입 값의 빈 배열로 초기화되는 `items`라는 프로퍼티를 생성할 때

- *To specify that the `push(_:)` method has a single parameter called `item`, which must be of type `Element`*
  
  `push(_:)` 메서드에 `Element` 타입이어야 하는 `item`이라는 단일 매개변수가 있음을 지정할 때

- *To specify that the value returned by the `pop()` method will be a value of type `Element`*
  
  `pop()` 메서드에서 반환된 값이 `Element` 타입의 값이 되도록 지정할 때

*Because it’s a generic type, `Stack` can be used to create a stack of any valid type in Swift, in a similar manner to `Array` and `Dictionary`.*

제네릭 타입이기 때문에 `Stack`은 Swift에서 `Array` 및 `Dictionary`와 유사한 방식으로 모든 유효한 타입의 스택을 만드는 데 사용할 수 있습니다.

*You create a new `Stack` instance by writing the type to be stored in the stack within angle brackets. For example, to create a new stack of strings, you write `Stack<String>()`:*

각 괄호 안에 스택에 저장할 타입을 작성하여 새 `Stack` 인스턴스를 만듭니다. 예를 들어 새 문자열 스택을 만들려면 `Stack<String>()`을 작성합니다.

```swift
var stackOfStrings = Stack<String>()
stackOfStrings.push("uno")
stackOfStrings.push("dos")
stackOfStrings.push("tres")
stackOfStrings.push("cuatro")
// the stack now contains 4 strings
```

*Here’s how `stackOfStrings` looks after pushing these four values on to the stack:*

다음은 이 4개의 값을 스택에 푸시한 후 `stackOfStrings`가 어떻게 보이는지 보여줍니다.![](https://docs.swift.org/swift-book/images/stackPushedFourStrings@2x.png)

*Popping a value from the stack removes and returns the top value, `"cuatro"`:*

스택으로부터 값을 팝핑하면 최상단 값 `"cuatro"`을 제거하고 리턴합니다.

```swift
let fromTheTop = stackOfStrings.pop()
// fromTheTop is equal to "cuatro", and the stack now contains 3 strings
```

*Here’s how the stack looks after popping its top value:*

다음은 스택에서 최상단 값을 팝핑한 이후의 모습입니다.

*![](https://docs.swift.org/swift-book/images/stackPoppedOneString@2x.png)*
