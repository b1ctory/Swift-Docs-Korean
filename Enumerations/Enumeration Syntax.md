## *Enumeration Syntax : 열거형 구문*

*You introduce enumerations with the `enum` keyword and place their entire definition within a pair of braces:*

`enum`키워드를 사용해서 열거를 도입하고 전체 정의를 괄호 안에 넣습니다.

```swift
enum SomeEnumeration {
    // enumeration definition goes here
}
```

*Here’s an example for the four main points of a compass:*

다음은 나침반의 네 가지 주요 지점에 대한 예입니다.

```swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```

*The values defined in an enumeration (such as `north`, `south`, `east`, and `west`) are its enumeration cases. You use the `case` keyword to introduce new enumeration cases.*

열거형에 정의된 값 (`north`, `south`, `east`, 그리고 `west` 같은)은 열거형의 케이스입니다. case 키워드를 사용해서 새로운 열거형 케이스를 소개합니다.

> *NOTE*
> 
> *Swift enumeration cases don’t have an integer value set by default, unlike languages like C and Objective-C. In the `CompassPoint` example above, `north`, `south`, `east` and `west` don’t implicitly equal `0`, `1`, `2` and `3`. Instead, the different enumeration cases are values in their own right, with an explicitly defined type of `CompassPoint`.*
> 
> Swift의 열거형 케이스는 C 및 Objective-C 와 같은 언어와 달리 기본적으로 정수 값이 설정되어 있지 않습니다. 위의  `CompassPoint` 예에서, `north`, `south`, `east` 그리고 `west`이 `0`, `1`, `2` 그리고 `3`과 암묵적으로 같지는 않습니다. 대신, 다른 열거 케이스는 명시적으로 정의된 타입의 `CompassPoint`가 있는 자체 값입니다.

*Multiple cases can appear on a single line, separated by commas:*

여러개의 사례가 쉼표로 구분되서 한 줄에 표시될 수 있습니다.

```swift
enum Planet {
    case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

*Each enumeration definition defines a new type. Like other types in Swift, their names (such as `CompassPoint` and `Planet`) start with a capital letter. Give enumeration types singular rather than plural names, so that they read as self-evident:*

각 열거형 정의는 새 타입을 정의합니다. Swift의 다른 타입과 마찬가지로, 이름 (`CompassPoint` 그리고 `Planet`같은) 도 대문자로 시작합니다. 열거형 타입을 복수 이름이 아닌 단수로 지정하여 자명하게 읽도록 합니다.

```swift
var directionToHead = CompassPoint.west
```

*The type of `directionToHead` is inferred when it’s initialized with one of the possible values of `CompassPoint`. Once `directionToHead` is declared as a `CompassPoint`, you can set it to a different `CompassPoint` value using a shorter dot syntax:*

`directionToHead`타입은 `CompassPoint` 의 가능한 값 중 하나로 초기화할 때 추론됩니다. `directionToHead`가 `CompassPoint`로 정의되면, 더 짧은 도트 구문을 사용하여 다른 `CompassPoint` 값으로 설정할 수 있습니다.

```swift
directionToHead = .east
```

*The type of `directionToHead` is already known, and so you can drop the type when setting its value. This makes for highly readable code when working with explicitly typed enumeration values.*

`directionToHead`은 이미 알려져 있으므로, 값을 설정할 때 타입을 삭제할 수 있습니다. 이렇게 하면 명시적으로 입력된 열거형 값으로 작업할 때 읽기 쉬운 코드가 생성됩니다.
