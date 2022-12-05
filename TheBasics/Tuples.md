## *Tuples*

*Tuples group multiple values into a single compound value. The values within a tuple can be of any type and don’t have to be of the same type as each other.*

튜플은 여러 값을 단일 복합 값으로 그룹화합니다. 튜플 내의 값은 모든 타입일 수 있으며 서로 동일한 타입일 필요는 없습니다.



*In this example, `(404, "Not Found")` is a tuple that describes an HTTP status code. An HTTP status code is a special value returned by a web server whenever you request a web page. A status code of `404 Not Found` is returned if you request a webpage that doesn’t exist.*

이 예시에서 (404, "Not Found")는 HTTP 상태 코드를 설명하는 튜플입니다. HTTP 상태코드는 웹페이지를 요청할 때마다 웹서버에서 반환하는 특수값입니다. 존재하지 않는 웹페이지를 요청하면 404 Not Found 상태 코드가 반환됩니다.



```swift
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
```

*The `(404, "Not Found")` tuple groups together an `Int` and a `String` to give the HTTP status code two separate values: a number and a human-readable description. It can be described as “a tuple of type `(Int, String)`”.*

(404, "Not Found") 튜플은 Int와 Stirng을 함께 그룹화하여 HTTP 상태 코드에 숫자와 사람이 읽을 수 있는 설명이라는 두 가지 개별 값을 제공합니다. (Int, String) 타입의 튜플로 설명할 수 있습니다.



*You can create tuples from any permutation of types, and they can contain as many different types as you like. There’s nothing stopping you from having a tuple of type `(Int, Int, Int)`, or `(String, Bool)`, or indeed any other permutation you require.*

타입의 순열에서 튜플을 생성할 수 있으며, 원하는만큼 다양한 타입을 포함할 수 있습니다. (Int, Int, Int) 혹은 (String, Bool)  타입의 튜플 혹은 실제로 필요한 다른 순열을 갖는 것을 막을 수 있는 것은 없습니다.



*You can decompose a tuple’s contents into separate constants or variables, which you then access as usual:*

튜플의 내용을 별도의 상수 혹은 변수로 분해하여 평소처럼 엑세스할 수 있습니다.



```swift
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"
print("The status message is \(statusMessage)")
// Prints "The status message is Not Found"
```



*If you only need some of the tuple’s values, ignore parts of the tuple with an underscore (`_`) when you decompose the tuple:*

튜플의 값 중 일부만이 필요할 경우, 튜플을 분해할 때 언더바 (_)가 있는 튜플 부분은 무시하세요.

```swift
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Prints "The status code is 404"
```

*Alternatively, access the individual element values in a tuple using index numbers starting at zero:*

대안으로, 0에서 시작하는 인덱스 번호를 사용하여 튜플의 개별 요소 값에 엑세스 합니다.



```swift
print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
print("The status message is \(http404Error.1)")
// Prints "The status message is Not Found"
```

*You can name the individual elements in a tuple when the tuple is defined:*

튜플이 정의될 때 튜플의 개별 요소 이름을 지정할 수 있습니다.



```swift
let http200Status = (statusCode: 200, description: "OK")
```

*If you name the elements in a tuple, you can use the element names to access the values of those elements:*

튜플의 요소를 지정하는 경우 요소 이름을 사용해서 해당 요소 값에 엑세스 할 수 있습니다.

```swift
print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK"
```

*Tuples are particularly useful as the return values of functions. A function that tries to retrieve a web page might return the `(Int, String)` tuple type to describe the success or failure of the page retrieval. By returning a tuple with two distinct values, each of a different type, the function provides more useful information about its outcome than if it could only return a single value of a single type. For more information, see [Functions with Multiple Return Values](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID164).*

튜플은 함수의 반환값으로 특히 유용합니다. 웹페이지 검색을 시도하는 함수는 페이지 검색의 성공 또는 실패를 설명하는 (Int, String) 튜플 유형을 반환할 수 있습니다. 두 개의 다른 값을 가진 튜플을 각각 다른 유형으로 반환함으로써 함수는 단일 타입의 단일 값만 반환할 수 있는 경우보다 결과에 대한 더 유용한 정보를 제공합니다. 자세한 내용은 [링크] 를 참조하세요.



> *NOTE*
> 
> *Tuples are useful for simple groups of related values. They’re not suited to the creation of complex data structures. If your data structure is likely to be more complex, model it as a class or structure, rather than as a tuple. For more information, see [Structures and Classes](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html).*
> 
> 튜플은 관련 값의 단순 그룹에 유용합니다. 튜플은 복잡한 데이터 구조를 만드는데 적합하지 않습니다. 데이터 구조가 더 복잡할 가능성이 있으면 튜플이 아닌 클래스나 구조체로 모델링하세요. 자세한 내용은 [링크]를 참조하세요.
