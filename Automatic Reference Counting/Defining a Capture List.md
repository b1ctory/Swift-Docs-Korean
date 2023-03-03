### *Defining a Capture List : 캡처 리스트 정의*

*Each item in a capture list is a pairing of the `weak` or `unowned` keyword with a reference to a class instance (such as `self`) or a variable initialized with some value (such as `delegate = self.delegate`). These pairings are written within a pair of square braces, separated by commas.*

캡처 목록의 각 항목은 클래스 인스턴스(예: `self`) 또는 일부 값으로 초기화된 변수(예: `delegate = self.delegate`)에 대한 참조와 `weak` 또는 `unowned` 키워드의 쌍입니다. ). 이러한 쌍은 쉼표로 구분된 한 쌍의 대괄호 안에 작성됩니다.

*Place the capture list before a closure’s parameter list and return type if they’re provided:*

클로저의 매개변수 목록 앞에 캡처 목록을 배치하고 제공된 경우 타입을 반환합니다.

```swift
lazy var someClosure = {
        [unowned self, weak delegate = self.delegate]
        (index: Int, stringToProcess: String) -> String in
    // closure body goes here
}
```

*If a closure doesn’t specify a parameter list or return type because they can be inferred from context, place the capture list at the very start of the closure, followed by the `in` keyword:*

클로저가 컨텍스트에서 유추할 수 있기 때문에 매개변수 목록이나 반환 타입을 지정하지 않는 경우 캡처 목록을 클로저 맨 앞에 배치하고 그 뒤에 `in` 키워드를 추가하세요.

```swift
lazy var someClosure = {
        [unowned self, weak delegate = self.delegate] in
    // closure body goes here
}
```

### *Weak and Unowned References : 약한참조와 미소유 참조*

*Define a capture in a closure as an unowned reference when the closure and the instance it captures will always refer to each other, and will always be deallocated at the same time.*

클로저와 클로저가 캡처하는 인스턴스가 항상 서로를 참조하고 항상 동시에 할당 해제될 때 클로저의 캡처를 미소유 참조로 정의하세요.

*Conversely, define a capture as a weak reference when the captured reference may become `nil` at some point in the future. Weak references are always of an optional type, and automatically become `nil` when the instance they reference is deallocated. This enables you to check for their existence within the closure’s body.*

반대로 캡처된 참조가 미래의 어느 시점에서 `nil`이 될 수 있는 경우 캡처를 약한 참조로 정의합니다. 약한 참조는 항상 옵셔널 타입이며 참조하는 인스턴스가 할당 해제되면 자동으로 `nil`이 됩니다. 이를 통해 클로저 본문 내에 존재 여부를 확인할 수 있습니다.

> *Note*
> 
> *If the captured reference will never become `nil`, it should always be captured as an unowned reference, rather than a weak reference.*
> 
> 캡처된 참조가 `nil`이 되지 않는 경우 항상 약한 참조가 아닌 미소유 참조로 캡처해야 합니다.

*An unowned reference is the appropriate capture method to use to resolve the strong reference cycle in the `HTMLElement` example from [Strong Reference Cycles for Closures](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/automaticreferencecounting#Strong-Reference-Cycles-for-Closures) above. Here’s how you write the `HTMLElement` class to avoid the cycle:*

소유되지 않은 참조는 [링크]를 참조하세요. 주기를 피하기 위해 `HTMLElement` 클래스를 작성하는 방법은 다음과 같습니다.

```swift
class HTMLElement {

    let name: String
    let text: String?

    lazy var asHTML: () -> String = {
            [unowned self] in
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

*This implementation of `HTMLElement` is identical to the previous implementation, apart from the addition of a capture list within the `asHTML` closure. In this case, the capture list is `[unowned self]`, which means “capture self as an unowned reference rather than a strong reference”.*

이 `HTMLElement` 구현은 `asHTML` 클로저 내에 캡처 목록을 추가한 것을 제외하면 이전 구현과 동일합니다. 이 경우 캡처 목록은 `[unowned self]`이며, 이는 "self를 강한 참조가 아닌 unowned 참조로 캡처"한다는 의미입니다.

*You can create and print an `HTMLElement` instance as before:*

이전과 같이 `HTMLElement` 인스턴스를 만들고 출력 수 있습니다.

```swift
var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
print(paragraph!.asHTML())
// Prints "<p>hello, world</p>"
```

*Here’s how the references look with the capture list in place:*

다음은 캡처 목록이 있는 참조의 모습입니다.

*![](https://docs.swift.org/swift-book/images/closureReferenceCycle02@2x.png)*

*This time, the capture of `self` by the closure is an unowned reference, and doesn’t keep a strong hold on the `HTMLElement` instance it has captured. If you set the strong reference from the `paragraph` variable to `nil`, the `HTMLElement` instance is deallocated, as can be seen from the printing of its deinitializer message in the example below:*

이번에 클로저에 의한 `self` 캡처는 미소유 참조이며 캡처한 `HTMLElement` 인스턴스를 강력하게 유지하지 않습니다. `paragraph` 변수의 강한 참조를 `nil`로 설정하면 `HTMLElement` 인스턴스가 할당 해제됩니다. 이는 아래 예의 초기화 해제 메시지 출력에서 볼 수 있습니다.

```swift
paragraph = nil
// Prints "p is being deinitialized"
```

*For more information about capture lists, see [Capture Lists](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/expressions#Capture-Lists).*

캡처 목록에 대한 자세한 내용은 [링크]를 참조하세요.
