## *Type Casting for Any and AnyObject : Any와 AnyObject에 대한 타입캐스팅*

*Swift provides two special types for working with nonspecific types:*

Swift는 비특정 타입의 작업을 위한 두 가지 특수 타입을 제공합니다:

- *`Any` can represent an instance of any type at all, including function types.*
  
  `Any`는 함수 타입을 포함하여 모든 타입의 인스턴스를 나타낼 수 있습니다.

- *`AnyObject` can represent an instance of any class type.*
  
  `AnyObject`는 모든 클래스 타입의 인스턴스를 나타낼 수 있습니다.

*Use `Any` and `AnyObject` only when you explicitly need the behavior and capabilities they provide. It’s always better to be specific about the types you expect to work with in your code.*

`Any`와 `AnyObject`는 제공되는 동작과 기능이 명시적으로 필요한 경우에만 사용하세요. 코드에서 작업할 것으로 예상되는 타입을 항상 구체적으로 지정하는 것이 좋습니다.

*Here’s an example of using `Any` to work with a mix of different types, including function types and nonclass types. The example creates an array called `things`, which can store values of type `Any`:*

다음은 함수 타입과 클래스가 아닌 유형을 포함한 다양한 유형의 혼합 작업에 `Any`를 사용하는 예입니다. 이 예에서는 타입 `Any`의 값을 저장할 수 있는 `things`라는 배열을 만듭니다:

```swift
var things: [Any] = []

things.append(0)
things.append(0.0)
things.append(42)
things.append(3.14159)
things.append("hello")
things.append((3.0, 5.0))
things.append(Movie(name: "Ghostbusters", director: "Ivan Reitman"))
things.append({ (name: String) -> String in "Hello, \(name)" })
```

*The `things` array contains two `Int` values, two `Double` values, a `String` value, a tuple of type `(Double, Double)`, the movie “Ghostbusters”, and a closure expression that takes a `String` value and returns another `String` value.*

`things` 배열에는 두 개의 `Int` 값, 두 개의 `Double` 값, `String` 값, 영화 'Ghostbusters' 타입의의 `(Double, Double)` 타입 튜플, 그리고 `String` 값을 가져와서 다른 `String` 값을 반환하는 클로저 표현식이 포함됩니다.

*To discover the specific type of a constant or variable that’s known only to be of type `Any` or `AnyObject`, you can use an `is` or `as` pattern in a `switch` statement’s cases. The example below iterates over the items in the `things` array and queries the type of each item with a `switch` statement. Several of the `switch` statement’s cases bind their matched value to a constant of the specified type to enable its value to be printed:*

`Any` 또는 `AnyObject` 타입으로만 알려진 상수 또는 변수의 특정 타입을 검색하려면 `switch` 문의  `is` 또는 `as` 패턴을 사용할 수 있습니다. 아래 예제는 `things` 배열의 항목에 대해 반복하고 `switch`문으로 각 항목의 타입을 쿼리합니다. 다음과 같은 `switch` 문의 경우 일치하는 값을 지정된 타입의 상수에 바인딩하여 값을 인쇄할 수 있습니다:

```swift
for thing in things {
    switch thing {
    case 0 as Int:
        print("zero as an Int")
    case 0 as Double:
        print("zero as a Double")
    case let someInt as Int:
        print("an integer value of \(someInt)")
    case let someDouble as Double where someDouble > 0:
        print("a positive double value of \(someDouble)")
    case is Double:
        print("some other double value that I don't want to print")
    case let someString as String:
        print("a string value of \"\(someString)\"")
    case let (x, y) as (Double, Double):
        print("an (x, y) point at \(x), \(y)")
    case let movie as Movie:
        print("a movie called \(movie.name), dir. \(movie.director)")
    case let stringConverter as (String) -> String:
        print(stringConverter("Michael"))
    default:
        print("something else")
    }
}

// zero as an Int
// zero as a Double
// an integer value of 42
// a positive double value of 3.14159
// a string value of "hello"
// an (x, y) point at 3.0, 5.0
// a movie called Ghostbusters, dir. Ivan Reitman
// Hello, Michael
```

> *NOTE*
> 
> *The `Any` type represents values of any type, including optional types. Swift gives you a warning if you use an optional value where a value of type `Any` is expected. If you really do need to use an optional value as an `Any` value, you can use the `as` operator to explicitly cast the optional to `Any`, as shown below.*
> 
> `Any` 타입은 옵셔널 타입 포함한 모든 타입의 값을 나타냅니다. Swift는 `Any` 타입의 값이 예상되는 옵셔널 값을 사용할 경우 경고를 표시합니다. 옵셔널 값을 `Any` 값으로 사용해야 하는 경우 아래와 같이 `as` 연산자를 사용하여 옵셔널을 `Any`로 명시적으로 캐스팅할 수 있습니다.
> 
> ```swift
> let optionalNumber: Int? = 3
> things.append(optionalNumber)        // Warning
> things.append(optionalNumber as Any) // No warning
> ```
