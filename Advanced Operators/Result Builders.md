## *Result Builders : 결과 빌더*

*A result builder is a type you define that adds syntax for creating nested data, like a list or tree, in a natural, declarative way. The code that uses the result builder can include ordinary Swift syntax, like `if` and `for`, to handle conditional or repeated pieces of data.*

결과 빌더는 목록이나 트리와 같은 중첩된 데이터를 자연스럽고 선언적인 방식으로 작성하기 위한 구문을 추가하는 정의하는 타입입니다. 결과 작성기를 사용하는 코드는 조건부 또는 반복되는 데이터 조각을 처리하기 위해 `if` 및 `for`와 같은 일반적인 Swift 구문을 포함할 수 있습니다.

*The code below defines a few types for drawing on a single line using stars and text.*

아래 코드는 별과 텍스트를 사용하여 한 줄에 그리기 위한 몇 가지 타입을 정의합니다.

```swift
protocol Drawable {
    func draw() -> String
}
struct Line: Drawable {
    var elements: [Drawable]
    func draw() -> String {
        return elements.map { $0.draw() }.joined(separator: "")
    }
}
struct Text: Drawable {
    var content: String
    init(_ content: String) { self.content = content }
    func draw() -> String { return content }
}
struct Space: Drawable {
    func draw() -> String { return " " }
}
struct Stars: Drawable {
    var length: Int
    func draw() -> String { return String(repeating: "*", count: length) }
}
struct AllCaps: Drawable {
    var content: Drawable
    func draw() -> String { return content.draw().uppercased() }
}
```

*The `Drawable` protocol defines the requirement for something that can be drawn, like a line or shape: The type must implement a `draw()` method. The `Line` structure represents a single-line drawing, and it serves the top-level container for most drawings. To draw a `Line`, the structure calls `draw()` on each of the line’s components, and then concatenates the resulting strings into a single string. The `Text` structure wraps a string to make it part of a drawing. The `AllCaps` structure wraps and modifies another drawing, converting any text in the drawing to uppercase.*

`Drawable` 프로토콜은 선이나 도형과 같이 그릴 수 있는 항목에 대한 요구 사항을 정의합니다. 타입은 `draw()` 메서드를 구현해야 합니다. `Line` 구조체는 단일 선 그리기를 나타내며 대부분의 그림에 대한 최상위 컨테이너 역할을 합니다. `Line`을 그리기 위해 구조체는 선의 각 구성요소에서 `draw()`를 호출한 다음 결과 문자열을 단일 문자열로 연결합니다. `Text` 구조체는 문자열을 감싸서 그림의 일부로 만듭니다. `AllCaps` 구조체는 다른 그림을 감싸고 수정하여 그림의 모든 텍스트를 대문자로 변환합니다.

*It’s possible to make a drawing with these types by calling their initializers:*

이니셜라이저를 호출하여 이러한 타입으로 그림을 그릴 수 있습니다.

```swift
let name: String? = "Ravi Patel"
let manualDrawing = Line(elements: [
     Stars(length: 3),
     Text("Hello"),
     Space(),
     AllCaps(content: Text((name ?? "World") + "!")),
     Stars(length: 2),
])
print(manualDrawing.draw())
// Prints "***Hello RAVI PATEL!**"
```

*This code works, but it’s a little awkward. The deeply nested parentheses after `AllCaps` are hard to read. The fallback logic to use “World” when `name` is `nil` has to be done inline using the `??` operator, which would be difficult with anything more complex. If you needed to include switches or `for` loops to build up part of the drawing, there’s no way to do that. A result builder lets you rewrite code like this so that it looks like normal Swift code.*

이 코드는 작동하긴 하지만 약간 어색합니다. `AllCaps` 다음에 중첩된 괄호는 읽기 어렵습니다. `name`이 `nil`일 때 "World"를 사용하는 폴백 로직은 `??` 연산자를 사용하여 인라인으로 수행해야 합니다. 더 복잡한 작업에서는 어려울 것입니다. 그림의 일부를 구성하기 위해 스위치나 `for` 루프를 포함해야 한다면 그렇게 할 방법이 없습니다. 결과 빌더를 사용하면 일반 Swift 코드처럼 보이도록 이와 같은 코드를 다시 작성할 수 있습니다.

*To define a result builder, you write the `@resultBuilder` attribute on a type declaration. For example, this code defines a result builder called `DrawingBuilder`, which lets you use a declarative syntax to describe a drawing:*

결과 빌더를 정의하려면 타입 선언에 `@resultBuilder` 프로퍼티를 작성합니다. 예를 들어 이 코드는 선언적 구문을 사용하여 그림을 설명할 수 있는 `DrawingBuilder`라는 결과 작성기를 정의합니다.

```swift
@resultBuilder
struct DrawingBuilder {
    static func buildBlock(_ components: Drawable...) -> Drawable {
        return Line(elements: components)
    }
    static func buildEither(first: Drawable) -> Drawable {
        return first
    }
    static func buildEither(second: Drawable) -> Drawable {
        return second
    }
}
```

*The `DrawingBuilder` structure defines three methods that implement parts of the result builder syntax. The `buildBlock(_:)` method adds support for writing a series of lines in a block of code. It combines the components in that block into a `Line`. The `buildEither(first:)` and `buildEither(second:)` methods add support for `if`-`else`.*

`DrawingBuilder` 구조체는 결과 빌더 구문의 일부를 구현하는 세 가지 메서드를 정의합니다. `buildBlock(_:)` 메서드는 코드 블록에 일련의 줄을 작성하기 위한 지원을 추가합니다. 해당 블록의 구성요소를 `Line`으로 결합합니다. `buildEither(first:)` 및 `buildEither(second:)` 메서드는 `if`-`else`에 대한 지원을 추가합니다.

*You can apply the `@DrawingBuilder` attribute to a function’s parameter, which turns a closure passed to the function into the value that the result builder creates from that closure. For example:*

`@DrawingBuilder` 프로퍼티를 함수의 매개변수에 적용할 수 있습니다. 이 프로퍼티는 함수에 전달된 클로저를 결과 빌더가 해당 클로저에서 생성하는 값으로 바꿉니다. 예를 들어:

```swift
func draw(@DrawingBuilder content: () -> Drawable) -> Drawable {
    return content()
}
func caps(@DrawingBuilder content: () -> Drawable) -> Drawable {
    return AllCaps(content: content())
}

func makeGreeting(for name: String? = nil) -> Drawable {
    let greeting = draw {
        Stars(length: 3)
        Text("Hello")
        Space()
        caps {
            if let name = name {
                Text(name + "!")
            } else {
                Text("World!")
            }
        }
        Stars(length: 2)
    }
    return greeting
}
let genericGreeting = makeGreeting()
print(genericGreeting.draw())
// Prints "***Hello WORLD!**"

let personalGreeting = makeGreeting(for: "Ravi Patel")
print(personalGreeting.draw())
// Prints "***Hello RAVI PATEL!**"
```

*The `makeGreeting(for:)` function takes a `name` parameter and uses it to draw a personalized greeting. The `draw(_:)` and `caps(_:)` functions both take a single closure as their argument, which is marked with the `@DrawingBuilder` attribute. When you call those functions, you use the special syntax that `DrawingBuilder` defines. Swift transforms that declarative description of a drawing into a series of calls to the methods on `DrawingBuilder` to build up the value that’s passed as the function argument. For example, Swift transforms the call to `caps(_:)` in that example into code like the following:*

`makeGreeting(for:)` 함수는 `name` 매개변수를 사용하여 맞춤 인사말을 그립니다. `draw(_:)` 및 `caps(_:)` 함수는 모두 `@DrawingBuilder` 프로퍼티로 표시된 단일 클로저를 인수로 사용합니다. 이러한 함수를 호출할 때 `DrawingBuilder`가 정의하는 특수 구문을 사용합니다. Swift는 그림의 선언적 설명을 `DrawingBuilder`의 메서드에 대한 일련의 호출로 변환하여 함수 인수로 전달된 값을 구성합니다. 예를 들어 Swift는 해당 예시에서 `caps(_:)`에 대한 호출을 다음과 같은 코드로 변환합니다.

```swift
let capsDrawing = caps {
    let partialDrawing: Drawable
    if let name = name {
        let text = Text(name + "!")
        partialDrawing = DrawingBuilder.buildEither(first: text)
    } else {
        let text = Text("World!")
        partialDrawing = DrawingBuilder.buildEither(second: text)
    }
    return partialDrawing
}
```

*Swift transforms the `if`-`else` block into calls to the `buildEither(first:)` and `buildEither(second:)` methods. Although you don’t call these methods in your own code, showing the result of the transformation makes it easier to see how Swift transforms your code when you use the `DrawingBuilder` syntax.*

Swift는 `if`-`else` 블록을 `buildEither(first:)` 및 `buildEither(second:)` 메서드에 대한 호출로 변환합니다. 자신의 코드에서 이러한 메소드를 호출하지는 않지만 변환 결과를 표시하면 `DrawingBuilder` 구문을 사용할 때 Swift가 코드를 변환하는 방법을 쉽게 확인할 수 있습니다.

*To add support for writing `for` loops in the special drawing syntax, add a `buildArray(_:)` method.*

특수 드로잉 구문에서 `for` 루프 작성 지원을 추가하려면 `buildArray(_:)` 메서드를 추가하세요.

```swift
extension DrawingBuilder {
    static func buildArray(_ components: [Drawable]) -> Drawable {
        return Line(elements: components)
    }
}
let manyStars = draw {
    Text("Stars:")
    for length in 1...3 {
        Space()
        Stars(length: length)
    }
}
```

*In the code above, the `for` loop creates an array of drawings, and the `buildArray(_:)` method turns that array into a `Line`.*

위의 코드에서 `for` 루프는 그림의 배열을 생성하고 `buildArray(_:)` 메서드는 해당 배열을 'Line'으로 바꿉니다.

*For a complete list of how Swift transforms builder syntax into calls to the builder type’s methods, see [resultBuilder](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes#resultBuilder).*

Swift가 빌더 구문을 빌더 타입의 메서드 호출로 변환하는 방법에 대한 전체 목록은 [링크]를 참조하세요.


