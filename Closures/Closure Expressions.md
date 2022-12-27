## *Closure Expressions : 클로저 표현식*

*Nested functions, as introduced in [Nested Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID178), are a convenient means of naming and defining self-contained blocks of code as part of a larger function. However, it’s sometimes useful to write shorter versions of function-like constructs without a full declaration and name. This is particularly true when you work with functions or methods that take functions as one or more of their arguments.*

[링크]에 소개된 대로 중첩 함수는 더 큰 함수의 일부로 자체 포함된 코드 블록의 이름을 지정하고 정의하는 편리한 수다닙니다. 그러나 완전한 선언과 이름 없는 함수와 유사한 구조의 짧은 버전을 작성하는 것이 유용할 때가 있습니다. 이는 함수를 하나 이상의 인수로 사용하는 함수 혹은 메서드로 작업할 때 특히 그렇습니다.

*Closure expressions are a way to write inline closures in a brief, focused syntax. Closure expressions provide several syntax optimizations for writing closures in a shortened form without loss of clarity or intent. The closure expression examples below illustrate these optimizations by refining a single example of the `sorted(by:)` method over several iterations, each of which expresses the same functionality in a more succinct way.*

클로저 표현식은 인라인 클로저를 짧고 집중적인 구문으로 작성하는 방법입니다. 클로저 표현식은 명확성이나 의도를 잃지 않고 단축된 형태로 클로저를 쓰기 위한 몇가지 구문 최적화를 제공합니다. 아래의 클로저 표현식 예제는 각각 동일한 기능을 보다 간결한 방식으로 표현하는 여러 반복에 걸쳐 `sorted(by:)` 메서드의 단일 예시를 세분화하여 이런 최적화를 설명합니다.



### *The Sorted Method : 정렬된 메서드*

*Swift’s standard library provides a method called `sorted(by:)`, which sorts an array of values of a known type, based on the output of a sorting closure that you provide. Once it completes the sorting process, the `sorted(by:)` method returns a new array of the same type and size as the old one, with its elements in the correct sorted order. The original array isn’t modified by the `sorted(by:)` method.*

Swift의 표준 라이브러리는 사용자가 제공하는 정렬 클로저의 출력을 기반으로 알려진 타입의 값 배열을 정렬하는 `sorted(by:)`라는 메서드를 제공합니다. 정렬 프로세스가 완료되면 `sorted(by:)` 메서드는 요소를 올바른 정렬 순서로 이전 배열과 동일한 타입 및 크기의 새 배열을 반환합니다. 원래 배열은 `sorted(by:)` 메서드로 수정도지 않습니다.

*The closure expression examples below use the `sorted(by:)` method to sort an array of `String` values in reverse alphabetical order. Here’s the initial array to be sorted:*

아래의 클로저 표현 예제에서는 `sorted(by:)` 메서드를 사용해서 `String` 값의 배열을 알파벳 역순으로 정렬합니다. 정렬할 초기 배열은 다음과 같습니다 :

```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
```

*The `sorted(by:)` method accepts a closure that takes two arguments of the same type as the array’s contents, and returns a `Bool` value to say whether the first value should appear before or after the second value once the values are sorted. The sorting closure needs to return `true` if the first value should appear before the second value, and `false` otherwise.*

`sorted(by:)` 메서드는 배열의 내용과 동일한 타입의 두 개의 인수를 사용하는 클로저를 허용하고 값이 정렬되면 첫번째 값이 두번째 값 앞에 나타나야 하는지 아니면 뒤에 나타나야 하는지를 알려주는 `Bool` 값을 반환합니다. 정렬 클로저는 첫번째 값이 두번째 값 앞에 나타나면 `true` 를 반환하고, 그렇지 않으면 `false`를 반환해야 합니다.

*This example is sorting an array of `String` values, and so the sorting closure needs to be a function of type `(String, String) -> Bool`.*

이 예제는 String값의 배열을 정렬하는 것이므로 정렬 클로저는 `(String, String) -> Bool` 타입의 함수여야 합니다.

*One way to provide the sorting closure is to write a normal function of the correct type, and to pass it in as an argument to the `sorted(by:)` method:*

정렬 클로저를 제공하는 한가지 방법은 올바른 형식의 정상 함수를 작성하고 이 함수를 `sorted(by:)` 메서드에 대한 인수로 전달하는 것입니다.

```swift
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}
var reversedNames = names.sorted(by: backward)
// reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```

*If the first string (`s1`) is greater than the second string (`s2`), the `backward(_:_:)` function will return `true`, indicating that `s1` should appear before `s2` in the sorted array. For characters in strings, “greater than” means “appears later in the alphabet than”. This means that the letter `"B"` is “greater than” the letter `"A"`, and the string `"Tom"` is greater than the string `"Tim"`. This gives a reverse alphabetical sort, with `"Barry"` being placed before `"Alex"`, and so on.*

첫번째 문자열 (`s1`)이 두번째 문자열 (`s2`)보다 크면 `backward(_:_:)`함수가 `true`를 반환하여 정렬된 배열에서 `s1`이 `s2` 앞에 나타나야 함을 나타냅니다. 문자열의 경우 "보다 큼"은 "보다 나중에 알파벳에 표시됨"을 의미합니다. 이것은 글자 `"B"`가 글자 "보다 크다"를 의미하고, `Tom`이라는 문자열이 `Tim`이라는 문자열보다 크다는 것을 의미합니다. 이것은 `"Barry"`가 `"Alex"`앞에 배치되는 역 알파벳 정렬 등을 제공합니다.

*However, this is a rather long-winded way to write what is essentially a single-expression function (`a > b`). In this example, it would be preferable to write the sorting closure inline, using closure expression syntax.*

그러나, 이것은 본질적으로 단일 표현 함수 (`a > b`)를 쓰는 다소 긴 방법입니다. 이 예시에서는 클로저 표현식 구문을 사용해서 정렬 클로저를 인라인으로 작성하는 것이 좋습니다.

### *Closure Expression Syntax : 클로저 표현 구문*

*Closure expression syntax has the following general form:*

클로저 표현의 일반적인 형식은 다음과 같습니다.

```swift
{ (parameters) -> return type in
    statements
}
```

*The parameters in closure expression syntax can be in-out parameters, but they can’t have a default value. Variadic parameters can be used if you name the variadic parameter. Tuples can also be used as parameter types and return types.*

클로저 표현식 구문의 매개변수는 in-out 매개변수일 수 있지만 기본값은 가질 수 없습니다. 가변 매개변수의 이름을 지정하면 가변매개변수를 사용할 수 있습니다. 튜플은 매개변수 타입 및 반환 타입으로도 사용할 수 있습니다.

*The example below shows a closure expression version of the `backward(_:_:)` function from above:*

아래 예제는 위에서 `backward(_:_:)`함수의 클로저 표현 버전을 보여줍니다.

```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

*Note that the declaration of parameters and return type for this inline closure is identical to the declaration from the `backward(_:_:)` function. In both cases, it’s written as `(s1: String, s2: String) -> Bool`. However, for the inline closure expression, the parameters and return type are written inside the curly braces, not outside of them.*

이 인라인 클로저에 대한 매개변수 및 반환 타입 선언은 `backward(_:_:)` 함수의 선언과 동일합니다. 두 경우 모두 `(s1: String, s2: String) -> Bool`로 표기됩니다. 그러나 인라인 클로저 표현식의 경우 매개변수와 반환 타입은 중괄호 외부가 아닌 중괄호 내부에 기록됩니다.

*The start of the closure’s body is introduced by the `in` keyword. This keyword indicates that the definition of the closure’s parameters and return type has finished, and the body of the closure is about to begin.*

클로저 본문의 시작은 `in` 키워드로 소개됩니다. 이 키워드는 클로저의 매개변수 및 반환 타입의 정의가 완료되었으며 클로저의 본문이 시작되려고 함을 나타냅니다.

*Because the body of the closure is so short, it can even be written on a single line:*

클로저의 본문이 너무 짧기 때문에 한 줄로도 쓸 수 있습니다.

```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```

*This illustrates that the overall call to the `sorted(by:)` method has remained the same. A pair of parentheses still wrap the entire argument for the method. However, that argument is now an inline closure.*

이것은 `sorted(by:)` 메서드에 대한 전체 호출이 동일하게 유지되었음을 보여줍니다. 한 쌍의 괄호는 여전히 메서드에 대한 전체 인수를 묶습니다. 하지만, 그 논의는 이제 인라인 클로저입니다.

### *Inferring Type From Context : 콘텍스트에서 타입 유추*

*Because the sorting closure is passed as an argument to a method, Swift can infer the types of its parameters and the type of the value it returns. The `sorted(by:)` method is being called on an array of strings, so its argument must be a function of type `(String, String) -> Bool`. This means that the `(String, String)` and `Bool` types don’t need to be written as part of the closure expression’s definition. Because all of the types can be inferred, the return arrow (`->`) and the parentheses around the names of the parameters can also be omitted:*

정렬 클로저는 메서드에 대한 인수로 전달되므로 Swift는 해당 매개변수의 타입과 반환되는 값의 타입을 유추할 수 있습니다. `sorted(by:)` 메서드가 문자열 배열에서 호출되고 있으므로 이 메서드의 인수는 `(String, String) -> Bool`타입의 함수여야 합니다. 즉, `(String, String)`과 Bool 타입은 클로저 정의의 일부로 작성할 필요가 없습니다. 모든 타입을 유추할 수 있으므로 반환 화살표 (`->`) 와 매개변수 이름 주변의 괄호로 생략할 수 있습니다.

```swift
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```

*It’s always possible to infer the parameter types and return type when passing a closure to a function or method as an inline closure expression. As a result, you never need to write an inline closure in its fullest form when the closure is used as a function or method argument.*

함수 혹은 메서드에 클로저를 인라인 클로저 표현식으로 전달할 때 매개변수 타입과 반환 타입을 항상 유추할 수 있습니다. 따라서 클로저 함수 혹은 메서드 인수로 사용되는 경우 인라인 클로저를 완전한 형식으로 작성할 필요가 없습니다.

*Nonetheless, you can still make the types explicit if you wish, and doing so is encouraged if it avoids ambiguity for readers of your code. In the case of the `sorted(by:)` method, the purpose of the closure is clear from the fact that sorting is taking place, and it’s safe for a reader to assume that the closure is likely to be working with `String` values, because it’s assisting with the sorting of an array of strings.*

그럼에도 불구하고, 원하는 경우 타입을 명시적으로 지정할 수 있으며, 코드 판독기의 모호성을 피할 수 있다면 그렇게 하는 것이 좋습니다. `sorted(by:)`메서드의 경우 정렬이 이루어지고 있다는 사실에서 클로저의 목적은 명확하며, 문자열 배열의 정렬을 지원하기 때문에 `String` 값을 사용해서 클로저가 작동할 가능성이 높다고 가정하는 것이 안전합니다.

### *Implicit Returns from Single-Expression Closures : 단일 표현식 클로저의 암묵적인 반환*

*Single-expression closures can implicitly return the result of their single expression by omitting the `return` keyword from their declaration, as in this version of the previous example:*

단일 표현식 클로저는 이전 예제의 다음 버전에서와 같이 선언에서 `return` 키워드를 생략해서 단일 표현식의 결과를 암시적으로 반환할 수 있습니다.

```swift
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

*Here, the function type of the `sorted(by:)` method’s argument makes it clear that a `Bool` value must be returned by the closure. Because the closure’s body contains a single expression (`s1 > s2`) that returns a `Bool` value, there’s no ambiguity, and the `return` keyword can be omitted.*

여기서 `sorted(by:)` 메서드 인수의 함수 타입은 클로저에 의해 `Bool` 값이 반환되어야 한다는 것을 분명히 합니다.클로저의 본문에는 `Bool` 값을 반환하는 단일 표현식 (`s1 > s2`) 이 포함되어있기 때문에 모호함이 없으며 `return` 키워드를 생략할 수 있습니다.

### *Shorthand Argument Names : 단축 인수 이름*

*Swift automatically provides shorthand argument names to inline closures, which can be used to refer to the values of the closure’s arguments by the names `$0`, `$1`, `$2`, and so on.*

Swift는 인라인 클로저에 자동으로 단축 인수 이름을 제공함, 이를 사용해서 클로저 인수 값을 `$0`, `$1`, `$2` 등의 이름으로 참조할 수 있습니다.

*If you use these shorthand argument names within your closure expression, you can omit the closure’s argument list from its definition. The type of the shorthand argument names is inferred from the expected function type, and the highest numbered shorthand argument you use determines the number of arguments that the closure takes. The `in` keyword can also be omitted, because the closure expression is made up entirely of its body:*

클로저 표현식을 사용할 때 이러한 단축 인수 이름을 사용하면 클로저의 인수 목록을 정의에서 생략할 수 있습니다. 단축키 인수 이름의 타입은 예상 함수 타입에서 유추되며 사용하는 가장 높은 번호의 단축키 인수는 클로저에 필요한 인수 수를 결정합니다. 클로저 표현식은 전체 본문으로 구성되므로 `in` 키워드도 생략할 수 있습니다.

```swift
reversedNames = names.sorted(by: { $0 > $1 } )
```

*Here, `$0` and `$1` refer to the closure’s first and second `String` arguments. Because `$1` is the shorthand argument with highest number, the closure is understood to take two arguments. Because the `sorted(by:)` function here expects a closure whose arguments are both strings, the shorthand arguments `$0` and `$1` are both of type `String`.*

여기서, `$0`과 `$1`은 클로저의 첫번째와 두번째 `String` 인수를 나타냅니다. `$1` 은 가장 높은 숫자를 가진 속기 인수이기 때문에 클로저에는 두 가지 ㅇ니수가 필요한 것으로 이해됩니다. 여기서 `sorted(by:)`  함수는 인수가 모두 문자열인 클로저를 예상하기 때문에 `$0`과 `$1`는 모두 `String`  타입입니다.

### *Operator Methods : 연산자 메서드*

*There’s actually an even shorter way to write the closure expression above. Swift’s `String` type defines its string-specific implementation of the greater-than operator (`>`) as a method that has two parameters of type `String`, and returns a value of type `Bool`. This exactly matches the method type needed by the `sorted(by:)` method. Therefore, you can simply pass in the greater-than operator, and Swift will infer that you want to use its string-specific implementation:*

실제로 위의 클로저 표현식을 쓰는 더 짧은 방법이 있습니다. Swift 의 String 타입은 보다 큰 연산자 (`>`)의 문자열특정 구현을 타입 `String`의 두 가지 매개변수를 갖는 메서드로 정의하고 `Bool` 타입의 값을 반환합니다. 이는 `sorted(by:)`메서드에 필요한 타입과 정확히 일치합니다. 따라서 보다큰 연산자를 간단히 전달할 수 있으며, Swift는 문자열특정 구현을 사용할 것이라고 추론합니다.

```swift
reversedNames = names.sorted(by: >)
```

*For more about operator methods, see [Operator Methods](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID42).*

연산자 메서드에 대한 자세한 내용은 [링크]를 참조하세요.
