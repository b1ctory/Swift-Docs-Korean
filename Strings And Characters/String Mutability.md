## *String Mutability : 문자열 가변성*

*You indicate whether a particular `String` can be modified (or mutated) by assigning it to a variable (in which case it can be modified), or to a constant (in which case it can’t be modified):*

특정 문자열을 변수 (수정이 가능한 경우) 혹은 상수 (수정이 불가능한 경우)에 할당해서 수정 (혹은 돌연변이(?)) 할 수 있는지 여부를 나타냅니다. 

```swift
var variableString = "Horse"
variableString += " and carriage"
// variableString is now "Horse and carriage"

let constantString = "Highlander"
constantString += " and another Highlander"
// this reports a compile-time error - a constant string cannot be modified
```

> *NOTE*
> 
> *This approach is different from string mutation in Objective-C and Cocoa, where you choose between two classes (`NSString` and `NSMutableString`) to indicate whether a string can be mutated.*
> 
> 이 접근법은 Objective-C와 문자열 돌연변이와는 다릅니다. 두 클래스 `NSString`과 `NSMutableString` 중 하나를 선택해서 문자열이 변형될 수 있는지 여부를 표시합니다.


