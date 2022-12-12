## *Initializing an Empty String : 빈 문자열 초기화*

*To create an empty `String` value as the starting point for building a longer string, either assign an empty string literal to a variable, or initialize a new `String` instance with initializer syntax:*

더 긴 문자열을 작성하기 위한 시작점으로 빈 String 값을 작성하려면 빈 문자열 리터럴을 변수에 할당하거나 초기화 구문을 사용해서 새 `String` 인스턴스를 초기화하세요.

```swift
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax
// these two strings are both empty, and are equivalent to each other
```

*Find out whether a `String` value is empty by checking its Boolean `isEmpty` property:*

`Boolean` 타입의 `isEmpty` 속성을 확인해서 String 값이 비어있는지 확인하세요.

```swift
if emptyString.isEmpty {
    print("Nothing to see here")
}
// Prints "Nothing to see here"
```


