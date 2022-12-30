## *Matching Enumeration Values with a Switch Statement : 열거형 값을 Switch 문과 일치*

*You can match individual enumeration values with a `switch` statement:*

개별 열거 값을 `switch`문과 일치시킬 수 있습니다.

```swift
directionToHead = .south
switch directionToHead {
case .north:
    print("Lots of planets have a north")
case .south:
    print("Watch out for penguins")
case .east:
    print("Where the sun rises")
case .west:
    print("Where the skies are blue")
}
// Prints "Watch out for penguins"
```

*You can read this code as:*

이 코드는 이렇게 읽힐 수 있습니다:

*“Consider the value of `directionToHead`. In the case where it equals `.north`, print `"Lots of planets have a north"`. In the case where it equals `.south`, print `"Watch out for penguins"`.”*

"`directionToHead`의 값을 고려하십시오. `.north`와 같은 경우 `"Lots of planets have a north"` 를 출력합니다. " .south와 같은 경우에는 `"Watch out for penguins"`를 인쇄합니다.

*…and so on.*

등등..

*As described in [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html), a `switch` statement must be exhaustive when considering an enumeration’s cases. If the `case` for `.west` is omitted, this code doesn’t compile, because it doesn’t consider the complete list of `CompassPoint` cases. Requiring exhaustiveness ensures that enumeration cases aren’t accidentally omitted.*

[링크]에서 설명한 바와 같이 열거형의 케이스를 고려할 때 `switch`문은 완전해야 합니다. `.west`에 대한 case가 생략되면 이 코드는 `compassPoint` 케이스의 전체 목록을 고려하지 않기 때문에 컴파일되지 않습니다. 완전성을 요구하면 실수로 열거 케이스가 누락되지 않음을 보장합니다.

*When it isn’t appropriate to provide a `case` for every enumeration case, you can provide a `default` case to cover any cases that aren’t addressed explicitly:*

모든 열거형 케이스에 대해 `case`를 제공하는 것이 적절하지 않은 경우, 명시적으로 해결되지 않은 사례를 포함하는 `default`사례를 제공할 수 있습니다.

```swift
let somePlanet = Planet.earth
switch somePlanet {
case .earth:
    print("Mostly harmless")
default:
    print("Not a safe place for humans")
}
// Prints "Mostly harmless"
Iterating over Enumera
```
