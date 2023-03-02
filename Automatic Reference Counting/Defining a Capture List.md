### *Defining a Capture List*

*Each item in a capture list is a pairing of the `weak` or `unowned` keyword with a reference to a class instance (such as `self`) or a variable initialized with some value (such as `delegate = self.delegate`). These pairings are written within a pair of square braces, separated by commas.*

*Place the capture list before a closure’s parameter list and return type if they’re provided:*

```swift
lazy var someClosure = {
        [unowned self, weak delegate = self.delegate]
        (index: Int, stringToProcess: String) -> String in
    // closure body goes here
}
```

*If a closure doesn’t specify a parameter list or return type because they can be inferred from context, place the capture list at the very start of the closure, followed by the `in` keyword:*

```swift
lazy var someClosure = {
        [unowned self, weak delegate = self.delegate] in
    // closure body goes here
}
```

### *Weak and Unowned References*

*Define a capture in a closure as an unowned reference when the closure and the instance it captures will always refer to each other, and will always be deallocated at the same time.*

*Conversely, define a capture as a weak reference when the captured reference may become `nil` at some point in the future. Weak references are always of an optional type, and automatically become `nil` when the instance they reference is deallocated. This enables you to check for their existence within the closure’s body.*

> *Note*
> 
> *If the captured reference will never become `nil`, it should always be captured as an unowned reference, rather than a weak reference.*

*An unowned reference is the appropriate capture method to use to resolve the strong reference cycle in the `HTMLElement` example from [Strong Reference Cycles for Closures](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/automaticreferencecounting#Strong-Reference-Cycles-for-Closures) above. Here’s how you write the `HTMLElement` class to avoid the cycle:*

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

*You can create and print an `HTMLElement` instance as before:*

```swift
var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
print(paragraph!.asHTML())
// Prints "<p>hello, world</p>"
```

*Here’s how the references look with the capture list in place:*

*![](https://docs.swift.org/swift-book/images/closureReferenceCycle02@2x.png)*

*This time, the capture of `self` by the closure is an unowned reference, and doesn’t keep a strong hold on the `HTMLElement` instance it has captured. If you set the strong reference from the `paragraph` variable to `nil`, the `HTMLElement` instance is deallocated, as can be seen from the printing of its deinitializer message in the example below:*

```swift
paragraph = nil
// Prints "p is being deinitialized"
```

*For more information about capture lists, see [Capture Lists](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/expressions#Capture-Lists).*
