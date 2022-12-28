## *Trailing Closures : 후행클로저*

*If you need to pass a closure expression to a function as the function’s final argument and the closure expression is long, it can be useful to write it as a trailing closure instead. You write a trailing closure after the function call’s parentheses, even though the trailing closure is still an argument to the function. When you use the trailing closure syntax, you don’t write the argument label for the first closure as part of the function call. A function call can include multiple trailing closures; however, the first few examples below use a single trailing closure.*

클로저 표현식을 함수의 최종 인수로 전달해야하고 클로저가 긴 경우, 대신 후행 클로저로 작성하는 것이 유용할 수 있습니다. 후행 클로저가 함수에 대한 인수인 경우에도 함수 호출의 괄호 뒤에 후행 클로저를 씁니다. 후행 클로저 구문을 사용할 때 함수 호출의 일부로 첫번째 클로저에 대한 인수 레이블을 작성하지 않습니다. 함수 호출에는 여러개의 후행 클로저가 포함될 수 있지만, 아래의 처음 몇가지 예시에서는 단일 후행 클로저를 사용합니다.

```swift
func someFunctionThatTakesAClosure(closure: () -> Void) {
    // function body goes here
}

// Here's how you call this function without using a trailing closure:

someFunctionThatTakesAClosure(closure: {
    // closure's body goes here
})

// Here's how you call this function with a trailing closure instead:

someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
```

*The string-sorting closure from the [Closure Expression Syntax](https://docs.swift.org/swift-book/LanguageGuide/Closures.html#ID97) section above can be written outside of the `sorted(by:)` method’s parentheses as a trailing closure:*

위의 [링크]의 문자열-정렬 클로저는 `sorted(by:)`메서드의 괄호 밖에서 후행 클로저로 작성할 수 있습니다.

```swift
reversedNames = names.sorted() { $0 > $1 }
```

*If a closure expression is provided as the function’s or method’s only argument and you provide that expression as a trailing closure, you don’t need to write a pair of parentheses `()` after the function or method’s name when you call the function:*

클로저 표현식이 함수 혹은 메서드의 유일한 인수로 제공되고 해당 표현식을 후행 클로저로 제공하는 경우 함수를 호출할 때 함수 혹은 메서드 이름 뒤에 괄호 `()` 쌍을 쓸 필요가 없습니다.

```swift
reversedNames = names.sorted { $0 > $1 }
```

*Trailing closures are most useful when the closure is sufficiently long that it isn’t possible to write it inline on a single line. As an example, Swift’s `Array` type has a `map(_:)` method, which takes a closure expression as its single argument. The closure is called once for each item in the array, and returns an alternative mapped value (possibly of some other type) for that item. You specify the nature of the mapping and the type of the returned value by writing code in the closure that you pass to `map(_:)`.*

후행 클로저는 클로저가 너무 길어서 한 줄에 인라인으로 쓸 수 없을 때 가장 유용합니다. 예를 들어 Swift의 `Array` 타입에는 클로저 표현식을 단일 인수로 하는 `map(_:)` 메서드가 있습니다. 클로저는 배열의 각 항목에 대해 한 번 호출되고 해당 항목에 대한 대체 매핑 값 (가능한 경우 다른 타입) 을 반환합니다. `map(_:)`에 전달하는 코드를 클로저에 작성해서 매핑의 특성과 반환되는 값의 타입을 지정합니다.

*After applying the provided closure to each array element, the `map(_:)` method returns a new array containing all of the new mapped values, in the same order as their corresponding values in the original array.*

제공된 클로저를 각 배열 요소에 적용한 후 `map(_:)` 메서드는 원래 배열의 해당 값과 동일한 순서로 모든 새 매핑 값을 포함하는 새 배열을 반환합니다. 

*Here’s how you can use the `map(_:)` method with a trailing closure to convert an array of `Int` values into an array of `String` values. The array `[16, 58, 510]` is used to create the new array `["OneSix", "FiveEight", "FiveOneZero"]`:*

다음은 후행 클로저와 함께 `map(_:)` 메서드를 사용해서 `Int` 값의 배열을 `String` 값의 배열로 변환하는 방법입니다. 배열 `[156, 58, 510]`은 새 배열 `["OneSix", "FiveEight", "FiveOneZero"]`를 만드는데 사용됩니다.

```swift
let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]
```

*The code above creates a dictionary of mappings between the integer digits and English-language versions of their names. It also defines an array of integers, ready to be converted into strings.*

위의 코드는 정수 숫자와 이름의 영어 버전 사이의 매핑 딕셔너리를 만듭니다. 또한 문자열로 변환할 준비가 된 정수 배열을 정의합니다.

*You can now use the `numbers` array to create an array of `String` values, by passing a closure expression to the array’s `map(_:)` method as a trailing closure:*

이제 `numbers` 배열을 사용해서 배열의 `map(_:)` 메서드에 클로저 식을 후행 클로저로 전달해서 `String` 값의 배열을 만들 수 있습니다.

```swift
let strings = numbers.map { (number) -> String in
    var number = number
    var output = ""
    repeat {
        output = digitNames[number % 10]! + output
        number /= 10
    } while number > 0
    return output
}
// strings is inferred to be of type [String]
// its value is ["OneSix", "FiveEight", "FiveOneZero"]
```

*The `map(_:)` method calls the closure expression once for each item in the array. You don’t need to specify the type of the closure’s input parameter, `number`, because the type can be inferred from the values in the array to be mapped.*

`map(_:)` 메서드는 배열의 각 항목에 대해 클로저를 한 번 호출합니다. 타입은 매핑할 배열의 값에서 유추할 수 있으므로 클로저의 입력 매개변수 유형인 `number`를 지정할 필요가 없습니다. 

*In this example, the variable `number` is initialized with the value of the closure’s `number` parameter, so that the value can be modified within the closure body. (The parameters to functions and closures are always constants.) The closure expression also specifies a return type of `String`, to indicate the type that will be stored in the mapped output array.*

이 예시에서 변수 `number`는 클로저의 number 매개변수 값으로 초기화되어 클로저 본문 내에서 값을 수정할 수 있습니다. (함수 및 클로저에 대한 매개변수는 항상 상수입니다.) 클로저 표현식은 또한 매핑된 출력 배열에 저장될 타입을 나타내기 위해 `String`의 반환 타입을 지정합니다.

*The closure expression builds a string called `output` each time it’s called. It calculates the last digit of `number` by using the remainder operator (`number % 10`), and uses this digit to look up an appropriate string in the `digitNames` dictionary. The closure can be used to create a string representation of any integer greater than zero.*

클로저는 호출될 때마다 `output` 이라는 문자열을 작성합니다. 나머지 연산자 (`number % 10`)를 사용해서 `number`의 마지막 자리를 계산하고, 이 자리를 이용해서 `digitNames` 딕셔너리에서 적절한 문자열을 검색합니다. 클로저는 0보다 큰 정수의 문자열 표현을 만드는데 사용할 수 있습니다.

> *NOTE*
> 
> *The call to the `digitNames` dictionary’s subscript is followed by an exclamation point (`!`), because dictionary subscripts return an optional value to indicate that the dictionary lookup can fail if the key doesn’t exist. In the example above, it’s guaranteed that `number % 10` will always be a valid subscript key for the `digitNames` dictionary, and so an exclamation point is used to force-unwrap the `String` value stored in the subscript’s optional return value.*
> 
> `digitNames` 딕셔너리의 첨자에 대한 호출 뒤에 느낌표 (`!`)가 붙습니다. 딕셔너리 첨자는 키가 없는 경우 딕셔너리 조회가 실패할 수 있음을 나타내는 옵셔널 값을 반환하기 때문입니다. 위의 예에서 `number % 10`은 항상 `digitNames` 딕셔너리의 유효한 첨자 키가 되므로 느낌표를 사용해서 첨자의 옵셔널 반환 값에 저장된 `String` 값을 강제로 해제할 수 있습니다.

*The string retrieved from the `digitNames` dictionary is added to the front of `output`, effectively building a string version of the number in reverse. (The expression `number % 10` gives a value of `6` for `16`, `8` for `58`, and `0` for `510`.)*

digitNames 딕셔너리에서 검색된 문자열은 output의 앞쪽에 추가되어 역방향으로 숫자의 문자열 버전을 효과적으로 구축합니다. (`number % 10` 이라는 표현은 `16`의 경우 `6`, `58`의 경우 `8`, `510`의 경우 `0`의 값을 제공합니다.)

*The `number` variable is then divided by `10`. Because it’s an integer, it’s rounded down during the division, so `16` becomes `1`, `58` becomes `5`, and `510` becomes `51`.*

`number` 변수는 `10`으로 나뉩니다. 정수이기 때문에 나눗셈을 하면 반올림되므로 `16`은 `1`이 되고 `58`은 `5`가 되고 `510`은 `51`이 됩니다.

*The process is repeated until `number` is equal to `0`, at which point the `output` string is returned by the closure, and is added to the output array by the `map(_:)` method.*

이 과정은 `number`가  `0`과 같을 때까지 반복되며, 여기서 `output` 문자열은 클로저에 의해 반환되고 `map(_:)` 메서드에 의해 출력 배열에 추가됩니다.

*The use of trailing closure syntax in the example above neatly encapsulates the closure’s functionality immediately after the function that closure supports, without needing to wrap the entire closure within the `map(_:)` method’s outer parentheses.*

위의 예에서 후행 클로저 구문을 사용하면 `map(_:)` 메서드의 외부 괄호 안에서 전체 클로저를 감쌀 필요 없이 클로저가 지원하는 함수 직후에 클로저의 기능을 깔끔하게 캡슐화합니다.

*If a function takes multiple closures, you omit the argument label for the first trailing closure and you label the remaining trailing closures. For example, the function below loads a picture for a photo gallery:*

만약 함수가 여러개의 클로저를 사용하는 경우, 첫번째 후행 클로저에 대한 인수 레이블을 생략하고 나머지 후행 클로저에 레이블을 지정합니다. 예를 들어, 아래 함수는 사진 갤러리의 사진을 로드합니다. 

```swift
func loadPicture(from server: Server, completion: (Picture) -> Void, onFailure: () -> Void) {
    if let picture = download("photo.jpg", from: server) {
        completion(picture)
    } else {
        onFailure()
    }
}
```

*When you call this function to load a picture, you provide two closures. The first closure is a completion handler that displays a picture after a successful download. The second closure is an error handler that displays an error to the user.*

사진을 로드하기 위해 이 함수를 호출하면 두 개의 클로저가 제공됩니다. 첫번째 클로저는 성공적으로 다운로드 한 후 사진을 표시하는 completion handler 입니다. 두번째 클로저는 사용자에게 오류를 표시하는 오류 핸들러입니다.

```swift
loadPicture(from: someServer) { picture in
    someView.currentPicture = picture
} onFailure: {
    print("Couldn't download the next picture.")
}
```

*In this example, the `loadPicture(from:completion:onFailure:)` function dispatches its network task into the background, and calls one of the two completion handlers when the network task finishes. Writing the function this way lets you cleanly separate the code that’s responsible for handling a network failure from the code that updates the user interface after a successful download, instead of using just one closure that handles both circumstances.*

이 예에서 `loadPicture(from:completion:onFailure:)`` 함수는 네트워크 작업을 백그라운드로 디스패치하고 네트워크 작업이 끝나면 두 개의 completionHandler 중 하나를 호출합니다. 이러한 방식으로 함수를 작성하면 두 상황을 모두 처리하는 하나의 클로저만 사용하는 대신 다운로드가 성공한 후 사용자 인터페이스를 업데이트하는 코드에서 네트워크 장애 처리를 담당하는 코드를 깨끗하게 분리할 수 있습니다.

> *NOTE*
> 
> *Completion handlers can become hard to read, especially when you have to nest multiple handlers. An alternate approach is to use asynchronous code, as described in [Concurrency](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html).*
> 
> Completion Handler 는 특히 여러 핸들러를 중첩해야 하는 경우 읽기 어려울 수 있습니다. 다른 방법은 [링크]에 설명된대로 비동기 코드를 사용하는 것입니다.


