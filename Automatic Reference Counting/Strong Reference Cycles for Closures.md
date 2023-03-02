## *Strong Reference Cycles for Closures : 클로저를 위한 강한 참조 사이클*

*You saw above how a strong reference cycle can be created when two class instance properties hold a strong reference to each other. You also saw how to use weak and unowned references to break these strong reference cycles.*

위에서 두 클래스 인스턴스 프로퍼티가 서로에 대한 강력한 참조를 보유할 때 강력한 순환 참조가 생성되는 방법을 확인했습니다. 또한 약한 참조와 미소유 참조를 사용하여 이러한 강한 순환 참조를 끊는 방법도 살펴보았습니다.

*A strong reference cycle can also occur if you assign a closure to a property of a class instance, and the body of that closure captures the instance. This capture might occur because the closure’s body accesses a property of the instance, such as `self.someProperty`, or because the closure calls a method on the instance, such as `self.someMethod()`. In either case, these accesses cause the closure to “capture” `self`, creating a strong reference cycle.*

강한 순환 참조는 클래스 인스턴스의 프로퍼티에 클로저를 할당하고 해당 클로저의 본문이 인스턴스를 캡처하는 경우에도 발생할 수 있습니다. 이 캡처는 클로저의 본문이 `self.someProperty`와 같은 인스턴스의 프로퍼티에 액세스하거나 클로저가 `self.someMethod()`와 같은 인스턴스의 메서드를 호출하기 때문에 발생할 수 있습니다. 두 경우 모두 이러한 액세스로 인해 클로저가 `self`를 '캡처'하여 강력한 참조 순환을 생성합니다.

*This strong reference cycle occurs because closures, like classes, are reference types. When you assign a closure to a property, you are assigning a reference to that closure. In essence, it’s the same problem as above — two strong references are keeping each other alive. However, rather than two class instances, this time it’s a class instance and a closure that are keeping each other alive.*

이 강력한 순환 참조는 클래스와 같은 클로저가 참조 타입이기 때문에 발생합니다. 프로퍼티에 클로저를 할당하면 해당 클로저에 대한 참조를 할당하는 것입니다. 본질적으로 위와 같은 문제입니다. 두 개의 강력한 참조가 서로를 살아 있게 합니다. 그러나 이번에는 두 개의 클래스 인스턴스가 아니라 클래스 인스턴스와 클로저가 서로를 살아있게 합니다.

*Swift provides an elegant solution to this problem, known as a closure capture list. However, before you learn how to break a strong reference cycle with a closure capture list, it’s useful to understand how such a cycle can be caused.*

Swift는 클로저 캡처 목록으로 알려진 이 문제에 대한 우아한 솔루션을 제공합니다. 그러나 클로저 캡처 목록으로 강력한 참조 순환을 끊는 방법을 배우기 전에 그러한 순환이 어떻게 발생할 수 있는지 이해하는 것이 좋습니다.

*The example below shows how you can create a strong reference cycle when using a closure that references `self`. This example defines a class called `HTMLElement`, which provides a simple model for an individual element within an HTML document:*

아래 예시는 `self`를 참조하는 클로저를 사용할 때 강력한 참조 순환을 생성하는 방법을 보여줍니다. 이 예는 HTML 문서 내의 개별 요소에 대한 간단한 모델을 제공하는 `HTMLElement`라는 클래스를 정의합니다.

```swift
class HTMLElement {

    let name: String
    let text: String?

    lazy var asHTML: () -> String = {
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }

    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }

    deinit {
        print("\(name) is being deinitialized")
    }

}
```

*The `HTMLElement` class defines a `name` property, which indicates the name of the element, such as `"h1"` for a heading element, `"p"` for a paragraph element, or `"br"` for a line break element. `HTMLElement` also defines an optional `text` property, which you can set to a string that represents the text to be rendered within that HTML element.*

`HTMLElement` 클래스는 제목 요소의 경우 `"h1"`, 단락 요소의 경우 `"p"`, 단락 요소의 경우 `"br"`과 같이 요소의 이름을 나타내는 `name` 프로퍼티를 정의합니다. 줄 바꿈 요소. `HTMLElement`는 또한 옵셔널 `text` 프로퍼티를 정의합니다. 이 프로퍼티는 해당 HTML 요소 내에서 렌더링할 텍스트를 나타내는 문자열로 설정할 수 있습니다.

*In addition to these two simple properties, the `HTMLElement` class defines a lazy property called `asHTML`. This property references a closure that combines `name` and `text` into an HTML string fragment. The `asHTML` property is of type `() -> String`, or “a function that takes no parameters, and returns a `String` value”.*

이 두 가지 간단한 프로퍼티 외에도 `HTMLElement` 클래스는 `asHTML`이라는 lazy프로퍼티를  정의합니다. 이 프로퍼티는 `name`과 `text`를 HTML 문자열 조각으로 결합하는 클로저를 참조합니다. `asHTML` 프로퍼티는 `() -> String` 또는 "매개변수를 사용하지 않고 `String` 값을 반환하는 함수" 타입입니다.

*By default, the `asHTML` property is assigned a closure that returns a string representation of an HTML tag. This tag contains the optional `text` value if it exists, or no text content if `text` doesn’t exist. For a paragraph element, the closure would return `"<p>some text</p>"` or `"<p />"`, depending on whether the `text` property equals `"some text"` or `nil`.*

기본적으로 `asHTML` 프로퍼티에는 HTML 태그의 문자열 표현을 반환하는 클로저가 할당됩니다. 이 태그는 옵셔널 `text` 값이 있는 경우 이를 포함하고 `text`가 없는 경우 텍스트 콘텐츠를 포함하지 않습니다. 단락 요소의 경우 클로저는 `text` 프로퍼티가 `"some text"`인지 또는 `nil`인지에 따라  `"<p>some text</p>"` 혹은 `"<p />"`를 반환합니다. 

*The `asHTML` property is named and used somewhat like an instance method. However, because `asHTML` is a closure property rather than an instance method, you can replace the default value of the `asHTML` property with a custom closure, if you want to change the HTML rendering for a particular HTML element.*

`asHTML` 프로퍼티는 인스턴스 메소드와 같이 이름이 지정되고 사용됩니다. 그러나 `asHTML`은 인스턴스 메서드가 아닌 클로저 프로퍼티이므로 특정 HTML 요소의 HTML 렌더링을 변경하려는 경우 `asHTML` 프로퍼티의 기본값을 커스텀 클로저로 바꿀 수 있습니다.

*For example, the `asHTML` property could be set to a closure that defaults to some text if the `text` property is `nil`, in order to prevent the representation from returning an empty HTML tag:*

예를 들어, 표현이 빈 HTML 태그를 반환하지 않도록 하기 위해 `asHTML` 프로퍼티는 `text` 프로퍼티가 `nil`인 경우 기본적으로 일부 텍스트로 설정되는 클로저로 설정할 수 있습니다.

```swift
let heading = HTMLElement(name: "h1")
let defaultText = "some default text"
heading.asHTML = {
    return "<\(heading.name)>\(heading.text ?? defaultText)</\(heading.name)>"
}
print(heading.asHTML())
// Prints "<h1>some default text</h1>"
```

> *Note*
> 
> *The `asHTML` property is declared as a lazy property, because it’s only needed if and when the element actually needs to be rendered as a string value for some HTML output target. The fact that `asHTML` is a lazy property means that you can refer to `self` within the default closure, because the lazy property will not be accessed until after initialization has been completed and `self` is known to exist.*
> 
> `asHTML` 프로퍼티는 지연 프로퍼티로 선언됩니다. 요소가 실제로 일부 HTML 출력 대상에 대한 문자열 값으로 렌더링되어야 하는 경우에만 필요하기 때문입니다. `asHTML`이 lazy 프로퍼티라는 사실은 기본 클로저 내에서 `self`를 참조할 수 있음을 의미합니다. lazy 프로퍼티는 초기화가 완료되고 `self`가 존재하는 것으로 알려질 때까지 액세스되지 않기 때문입니다.

*The `HTMLElement` class provides a single initializer, which takes a `name` argument and (if desired) a `text` argument to initialize a new element. The class also defines a deinitializer, which prints a message to show when an `HTMLElement` instance is deallocated.*

`HTMLElement` 클래스는 `name` 인수와 (원하는 경우) `text` 인수를 사용하여 새 요소를 초기화하는 단일 초기화 프로그램을 제공합니다. 이 클래스는 또한 `HTMLElement` 인스턴스가 할당 해제될 때 표시할 메시지를 출력하는 초기화 해제자를 정의합니다.

*Here’s how you use the `HTMLElement` class to create and print a new instance:*

다음은 `HTMLElement` 클래스를 사용하여 새 인스턴스를 만들고 출력하는 방법입니다.

```swift
var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
print(paragraph!.asHTML())
// Prints "<p>hello, world</p>"
```

> *Note*
> 
> *The `paragraph` variable above is defined as an optional `HTMLElement`, so that it can be set to `nil` below to demonstrate the presence of a strong reference cycle.*
> 
> 위의 `paragraph` 변수는 옵셔널 `HTMLElement`로 정의되므로 강력한 순환 참조의 존재를 입증하기 위해 아래에서 `nil`로 설정할 수 있습니다.

*Unfortunately, the `HTMLElement` class, as written above, creates a strong reference cycle between an `HTMLElement` instance and the closure used for its default `asHTML` value. Here’s how the cycle looks:*

안타깝게도 위에서 설명한 대로 `HTMLElement` 클래스는 `HTMLElement` 인스턴스와 기본 `asHTML` 값에 사용되는 클로저 사이에 강력한 순환참조를 생성합니다. 주기는 다음과 같습니다.

*![](https://docs.swift.org/swift-book/images/closureReferenceCycle01@2x.png)*

*The instance’s `asHTML` property holds a strong reference to its closure. However, because the closure refers to `self` within its body (as a way to reference `self.name` and `self.text`), the closure captures self, which means that it holds a strong reference back to the `HTMLElement` instance. A strong reference cycle is created between the two. (For more information about capturing values in a closure, see [Capturing Values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Capturing-Values).)*

인스턴스의 `asHTML` 프로퍼티는 종료에 대한 강력한 참조를 보유합니다. 그러나 클로저는 본문 내에서 `self`를 참조하기 때문에(`self.name` 및 `self.text`를 참조하는 방법으로) 클로저는 self를 캡처합니다. 즉, `HTMLElement` 인스턴스에 대한 강력한 참조를 보유합니다.  둘 사이에 강력한 참조 순환이 생성됩니다. (클로저에서 값 캡처에 대한 자세한 내용은 [링크]를 참조하세요.

> *Note*
> 
> *Even though the closure refers to `self` multiple times, it only captures one strong reference to the `HTMLElement` instance.*
> 
> 클로저가 `self`를 여러 번 참조하더라도 `HTMLElement` 인스턴스에 대한 하나의 강력한 참조만 캡처합니다.

*If you set the `paragraph` variable to `nil` and break its strong reference to the `HTMLElement` instance, neither the `HTMLElement` instance nor its closure are deallocated, because of the strong reference cycle:*

`paragraph` 변수를 `nil`로 설정하고 `HTMLElement` 인스턴스에 대한 강력한 참조를 끊으면 강력한 참조 순환으로 인해 `HTMLElement` 인스턴스나 해당 클로저의 할당이 해제되지 않습니다.

```swift
paragraph = nil
```

*Note that the message in the `HTMLElement` deinitializer isn’t printed, which shows that the `HTMLElement` instance isn’t deallocated.*

`HTMLElement` 초기화 해제자의 메시지는 출력되지 않으며, 이는 `HTMLElement` 인스턴스가 할당 해제되지 않았음을 나타냅니다.


