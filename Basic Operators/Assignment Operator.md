## *Assignment Operator : 할당(대입) 연산자*

*The assignment operator (`a = b`) initializes or updates the value of `a` with the value of `b`:*

할당연산자 (`a = b`)는 `a`의 값을 `b` 로 초기화 하거나 업데이트합니다 :

```swift
let b = 10
var a = 5
a = b
// a is now equal to 10
```

*If the right side of the assignment is a tuple with multiple values, its elements can be decomposed into multiple constants or variables at once:*

오른쪽에 할당된 값이 여러 값을 가진 튜플일 경우, 해당 요소는 여러개의 상수 혹은 변수로 분해될 수 있습니다.

```swift
let (x, y) = (1, 2)
// x is equal to 1, and y is equal to 2
```

*Unlike the assignment operator in C and Objective-C, the assignment operator in Swift doesn’t itself return a value. The following statement isn’t valid:*

C 및 Objective-C 의 할당연산자와 달리  Swift의 할당 연산자 자체는 값을 반환하지 않습니다. 다음의 구문은 유효하지 않습니다 :

```swift
if x = y {
    // This isn't valid, because x = y doesn't return a value.
}
```

*This feature prevents the assignment operator (`=`) from being used by accident when the equal to operator (`==`) is actually intended. By making `if x = y` invalid, Swift helps you to avoid these kinds of errors in your code.*

이 기능은 등호 연산자 (`==`)가 실제로 의도된 경우 할당 연산자 (`=`)가 실수로 사용되는 것을 방지합니다. `if x = y` 를 무효화함으로써 Swift는 코드에서 이러한 종류의 오류를 피할 수 있도록 도와줍니다.
