### *Switch*

*A `switch` statement considers a value and compares it against several possible matching patterns. It then executes an appropriate block of code, based on the first pattern that matches successfully. A `switch` statement provides an alternative to the `if` statement for responding to multiple potential states.*

`switch` 문은 값을 고려해서 가능한 여러 일치 패턴과 비교합니다. 그런 다음 성공적으로 일치하는 첫번째 패턴을 기반으로 적절한 코드 블록을 실행합니다. `switch`문은 여러 잠재적 상태에 응답하기 위한 `if` 문에 대한 대안을 제공합니다.

*In its simplest form, a `switch` statement compares a value against one or more values of the same type.*

가장 간단한 형태로, `switch` 문은 동일한 타입의 하나 이상의 값과 비교합니다.

```swift
switch some value to consider {
case value 1:
    respond to value 1
case value 2,
     value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
}
```

*Every `switch` statement consists of multiple possible cases, each of which begins with the `case` keyword. In addition to comparing against specific values, Swift provides several ways for each case to specify more complex matching patterns. These options are described later in this chapter.*

모든 `switch` 문은 여러 개의 가능한 경우로 구성되며, 각각은 `case` 키워드로 시작합니다. Swift는 특정 값과 비교하는 것 외에도 각 경우에 대해 보다 복잡한 일치 패턴을 지정하는 몇가지 방법을 제공합니다.  이러한 옵션은 이 장의 뒷부분에 설명되어있습니다.

*Like the body of an `if` statement, each `case` is a separate branch of code execution. The `switch` statement determines which branch should be selected. This procedure is known as switching on the value that’s being considered.*

`if` 문의 본문처럼, 각각의 `case`는 코드 실행의 별개의 분기입니다. `switch`문은 어떤 분기를 선택할지 결정합니다. 이 절차를 고려 중인 값을 켜는 것으로 알려져 있습니다.

*Every `switch` statement must be exhaustive. That is, every possible value of the type being considered must be matched by one of the `switch` cases. If it’s not appropriate to provide a case for every possible value, you can define a default case to cover any values that aren’t addressed explicitly. This default case is indicated by the `default` keyword, and must always appear last.*

모든 `switch` 문은 철저해야 합니다. 즉, 고려되는 타입의 모든 가능한 값은 `switch` 케이스 중 하나와 일치해야 합니다. 가능한 모든 값에 대해 대소문자를 제공하는 것이 적절하지 않은 경우 명시적으로 처리되지 않은 값을 포함하도록 기본 대소문자를 정의할 수 있습니다. 이 기본 사레는 `default` 키워드로 표시되며 항상 마지막에 나타나야 합니다.

*This example uses a `switch` statement to consider a single lowercase character called `someCharacter`:*

이 예에서는 `switch` 문을 사용해서 `someCharacter`라는 단일 소문자를 고려합니다.

```swift
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
// Prints "The last letter of the alphabet"
```

*The `switch` statement’s first case matches the first letter of the English alphabet, `a`, and its second case matches the last letter, `z`. Because the `switch` must have a case for every possible character, not just every alphabetic character, this `switch` statement uses a `default` case to match all characters other than `a` and `z`. This provision ensures that the `switch` statement is exhaustive.*

`switch` 문의 첫번째 케이스는 영어 알파벳의 첫번째 문자 `a`와 일치하고 두번째 케이스는 마지막 문자 `z`와 일치합니다. switch는 모든 알파벳 문자 뿐만 아니라 가능한 모든 문자에 대해 케이스를 가져야하기 때문에 이 `switch`문은 `a`와 `z`를 제외한 모든 문자와 일치하기 위해 `default`를 사용합니다. 이 조항은 switch 문이 완전하다는 것을 보장합니다. 

#### *No Implicit Fallthrough : 암시적 실패 없음*

*In contrast with `switch` statements in C and Objective-C, `switch` statements in Swift don’t fall through the bottom of each case and into the next one by default. Instead, the entire `switch` statement finishes its execution as soon as the first matching `switch` case is completed, without requiring an explicit `break` statement. This makes the `switch` statement safer and easier to use than the one in C and avoids executing more than one `switch` case by mistake.*

C와 Objectiv-C의 `switch`문과 달리 Swift의 `switch` 문은 기본적으로 각 경우의 하단을 통과해서 다음 구문으로 ㄷ르어가지 않습니다. 대신에 전체 `switch` 문은 명시적인 `break` 문을 요구하지 않고 첫번째 일치하는 `switch` 사례가 완료되는 즉시 실행을 마칩니다. 이것은 C에 있는 것보다 `switch` 문을 더 안전하고 쉽게 사용할 수 있게 해주며 실수로 둘 이상의 `switch` 사례를 실행하는 것을 방지합니다.

> *NOTE*
> 
> *Although `break` isn’t required in Swift, you can use a `break` statement to match and ignore a particular case or to break out of a matched case before that case has completed its execution. For details, see [Break in a Switch Statement](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID139).*
> 
> Swift에서 break이 필요하진 않지만 break 문을 사용해서 특정 사례를 일치시키고 무시하거나 해당 사례가 실행되기 전에 일치하는 사례에서 벗어날 수 있습니다. 자세한 내용은 [링크]를 참조하세요.

*The body of each case must contain at least one executable statement. It isn’t valid to write the following code, because the first case is empty:*

각 사례의 본문에는 적어도 하나의 실행 가능한 구문이 포함되어야 합니다 .첫번째 사례가 비어있기 때문에 다음 코드를 작성할 수 없습니다.

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a": // Invalid, the case has an empty body
case "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// This will report a compile-time error.
```

*Unlike a `switch` statement in C, this `switch` statement doesn’t match both `"a"` and `"A"`. Rather, it reports a compile-time error that `case "a":` doesn’t contain any executable statements. This approach avoids accidental fallthrough from one case to another and makes for safer code that’s clearer in its intent.*

C의 `switch` 구문과 달리 이 `switch` 문은 `a`와 `switch`문 모두와 일치하지 않습니다. A는 오히려 `case "a":`에 실행 가능한 문이 포함되어 있지 않은 컴파일 타임 오류를 보고합니다. 이 접근 방식은 한 케이스에서 다른 케이스로 실수로 넘어가는 것을 방지하고 의도적으로 더 안전한 코드를 만듭니다.

*To make a `switch` with a single case that matches both `"a"` and `"A"`, combine the two values into a compound case, separating the values with commas.*

`a`와 `A`가 모두 일치하는 단일 케이스로 `switch`를 만드는 것은 두 값을 복합 케이스로 결합해서 쉼표로 값을 구분합니다.

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// Prints "The letter A"
```

*For readability, a compound case can also be written over multiple lines. For more information about compound cases, see [Compound Cases](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID548).*

가독성을 위해 복합 케이스를 여러 줄에 걸쳐 쓸 수도 있습니다. 복합 케이스에 대한 자세한 내용은 [링크]를 참조하세요.

> *NOTE*
> 
> *To explicitly fall through at the end of a particular `switch` case, use the `fallthrough` keyword, as described in [Fallthrough](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID140).*
> 
> 특정 `switch` 케이스의 끝에 명시적으로 실패하려면 [링크]에 설명된 대로 `fallthrough` 키워드를 사용하세요.

#### *Interval Matching : 간격 매칭*

*Values in `switch` cases can be checked for their inclusion in an interval. This example uses number intervals to provide a natural-language count for numbers of any size:*

switch의 케이스에 담긴 값은 간격에 포함되어 있는지 확인할 수 있습니다. 이 예시에서는 숫자 간격을 사용해서 모든 크기의 숫자에 대해 자연어 카운트를 제공합니다.

```swift
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// Prints "There are dozens of moons orbiting Saturn."
```

*In the above example, `approximateCount` is evaluated in a `switch` statement. Each `case` compares that value to a number or interval. Because the value of `approximateCount` falls between 12 and 100, `naturalCount` is assigned the value `"dozens of"`, and execution is transferred out of the `switch` statement.*

위의 예에서 `approximateCount`는 switch문에서 평가됩니다. 각각의 `case`는 그 값을 숫자나 구간과 비교합니다. `approximateCount` 값이 12에서 100 사이에 있기 때문에 `naturalCount` 값에는 `discues` 값이 할당되고 실행은 switch 문에서 전송됩니다.

#### *Tuples : 튜플*

*You can use tuples to test multiple values in the same `switch` statement. Each element of the tuple can be tested against a different value or interval of values. Alternatively, use the underscore character (`_`), also known as the wildcard pattern, to match any possible value.*

튜플을 사용해서 동일한 switch 문에서 여러 값을 테스트할 수 있습니다. 튜플의 각 요소는 서로 다른 값 혹은 값의 간격에 대해 테스트할 수 있습니다. 혹은 와일드카드 패턴이라고도 하는 밑줄 문자(`_`)를 사용해서 가능한 값과 일치시킵니다. 

*The example below takes an (x, y) point, expressed as a simple tuple of type `(Int, Int)`, and categorizes it on the graph that follows the example.*

아래 예제는 `(Int, Int)` 타입의 단순 튜플로 구현된 (x,y)점을 취하는 예제를 따르는 그래프입니다.

```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("\(somePoint) is at the origin")
case (_, 0):
    print("\(somePoint) is on the x-axis")
case (0, _):
    print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
    print("\(somePoint) is inside the box")
default:
    print("\(somePoint) is outside of the box")
}
// Prints "(1, 1) is inside the box"
```

![](https://docs.swift.org/swift-book/_images/coordinateGraphSimple_2x.png)

*The `switch` statement determines whether the point is at the origin (0, 0), on the red x-axis, on the green y-axis, inside the blue 4-by-4 box centered on the origin, or outside of the box.*

switch문은 점이 원점 (0,0)에 있는지, 빨간색 x축에 있는지, 녹색 y축에 있는지, 원점을 중심으로 하는 파란색 4x4 박스 안에 있는지, 상자 밖에 있는지를 결정합니다.

*Unlike C, Swift allows multiple `switch` cases to consider the same value or values. In fact, the point (0, 0) could match all four of the cases in this example. However, if multiple matches are possible, the first matching case is always used. The point (0, 0) would match `case (0, 0)` first, and so all other matching cases would be ignored.*

C와는 달리 Swift는 여러 `switch` 사례가 동일한 값 혹은 값을 고려할 수 있도록합니다. 실제로 점 (0,0)은 이 예제의 네 가지 경우 모두와 일치할 수 있습니다. 그러나 여러개의 일치가 가능한 경우에는 항상 첫번째 일치 사례가 사용됩니다. 점 (0,0)이 먼저 `case (0, 0)`와 일치하므로 다른 모든 일치 사례는 무시됩니다.

#### *Value Bindings : 값 바인딩*

*A `switch` case can name the value or values it matches to temporary constants or variables, for use in the body of the case. This behavior is known as value binding, because the values are bound to temporary constants or variables within the case’s body.*

`switch` 케이스는 케이스 본문에서 사용하기 위해 임시 상수 혹은 변수와 일치하는 값의 이름을 지정할 수 있습니다. 이 동작을 값 바인딩이라고 하는데, 값이 케이스 본문 내의 임시 상수 혹은 변수에 바인딩되기 때문입니다.

*The example below takes an (x, y) point, expressed as a tuple of type `(Int, Int)`, and categorizes it on the graph that follows:*

아래 예제는 `(Int, Int)` 타입의 튜플로 표현된 (x,y) 점을 취하고 다음 그래프에 분류합니다.

```swift
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}
// Prints "on the x-axis with an x value of 2"
```

![](https://docs.swift.org/swift-book/_images/coordinateGraphMedium_2x.png)

*The `switch` statement determines whether the point is on the red x-axis, on the green y-axis, or elsewhere (on neither axis).*

switch 문은 점이 빨간색 x축 위에 있는지, 녹색 y축 위에 있는지, 아니면 다른곳 (어느 축에도 없음)에 있는지 결정합니다.

*The three `switch` cases declare placeholder constants `x` and `y`, which temporarily take on one or both tuple values from `anotherPoint`. The first case, `case (let x, 0)`, matches any point with a `y` value of `0` and assigns the point’s `x` value to the temporary constant `x`. Similarly, the second case, `case (0, let y)`, matches any point with an `x` value of `0` and assigns the point’s `y` value to the temporary constant `y`.*

세 개의 `switch` 케이스는 자리 표시자 상수 x와 y를 선언하며, 이는 일시적으로 `anotherPoint`에서 하나 혹은 둘 다의 튜플 값을 취합니다. 첫 번째 케이스인 `case (let x, 0)`는 `y`값이 `0`인 임의의 점과 일치하고 점의 `x`값을 임시 상수 `x`에 할당합니다. 마찬가지로 두번째 경우인 `case (0, let y)`는 `x`값이 `0`인 임의의 점과 일치하고 `y`값을 임시 상수 `y`에 할당합니다.

*After the temporary constants are declared, they can be used within the case’s code block. Here, they’re used to print the categorization of the point.*

임시 상수가 선언된 후에는 케이스의 코드 블록 내에서 사용할 수 있습니다. 여기서는 점의 분류를 출력하는데 사용됩니다.

*This `switch` statement doesn’t have a `default` case. The final case, `case let (x, y)`, declares a tuple of two placeholder constants that can match any value. Because `anotherPoint` is always a tuple of two values, this case matches all possible remaining values, and a `default` case isn’t needed to make the `switch` statement exhaustive.*

`switch` 문에는 `default` 케이스가 없습니다. 마지막 케이스인 `case let (x, y)`는 임의의 값과 일치할 수 있는 두 자리 표시자 상수의 튜플을 선언합니다. `anotherPoint`는 항상 두 값의 튜플이기 때문에 이 경우는 가능한 모든 나머지 값과 일치하며 switch  문을 완전하게 만들기 위해 `default` 케이스가 필요하지 ㅇ낳습니다.

#### *Where*

*A `switch` case can use a `where` clause to check for additional conditions.*

`switch` 케이스는 `where` 절을 사용해서 추가 조건을 확인할 수 있습니다.

*The example below categorizes an (x, y) point on the following graph:*

아래 예제에서는 다음 그래프의 (x, y) 점을 분류합니다.

```swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// Prints "(1, -1) is on the line x == -y"
```

![](https://docs.swift.org/swift-book/_images/coordinateGraphComplex_2x.png)

*The `switch` statement determines whether the point is on the green diagonal line where `x == y`, on the purple diagonal line where `x == -y`, or neither.*

`switch` 문은 점이 `x == y` 인 초록색 대각선 위에 있는지, `x == -y`인 보라색 대각선 위에 있는지 혹은 둘 다 아닌지를 결정합니다.

*The three `switch` cases declare placeholder constants `x` and `y`, which temporarily take on the two tuple values from `yetAnotherPoint`. These constants are used as part of a `where` clause, to create a dynamic filter. The `switch` case matches the current value of `point` only if the `where` clause’s condition evaluates to `true` for that value.*

세 개의 `switch` 케이스는 자리 표시자 상수 `x`와 `y`를 선언하며, 이는 일시적으로 `yetAnotherPoint`에서 두 개의 튜플 값을 취합니다. 이러한 상수는 동적 필터를 만들기 위해 `where` 절의 일부로 사용됩니다. `switch` 케이스는 `where` 절의 조건이 해당 값에 대해 `true`로 평가되는 경우에만 `point`의 현재 값과 일치합니다.

*As in the previous example, the final case matches all possible remaining values, and so a `default` case isn’t needed to make the `switch` statement exhaustive.*

앞의 예시와 마찬가지로 최종 사례는 가능한 모든 나머지 값과 일치하므로 `switch` 문을 완전하게 만들기 위해 `default` 케이스가 필요하지 않습니다.

#### *Compound Cases : 복합 케이스*

*Multiple switch cases that share the same body can be combined by writing several patterns after `case`, with a comma between each of the patterns. If any of the patterns match, then the case is considered to match. The patterns can be written over multiple lines if the list is long. For example:*

동일한 본문을 공유하는 여러개의 스위치 케이스는 각각의 패턴 사이에 쉼표를 사용해서 `case` 뒤에 여러 개의 패턴을 작성해서 결합할 수 있습니다. 패턴 중 하나라도 일치하면 케이스가 일치하는 것으로 간주됩니다. 목록이 긴 경우 패턴을 여러 줄에 걸쳐 쓸 수 있습니다. 예를 들어 :

```swift
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    print("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
     "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    print("\(someCharacter) is a consonant")
default:
    print("\(someCharacter) isn't a vowel or a consonant")
}
// Prints "e is a vowel"
```

*The `switch` statement’s first case matches all five lowercase vowels in the English language. Similarly, its second case matches all lowercase English consonants. Finally, the `default` case matches any other character.*

`switch` 구문의 첫번째 케이스는 영어의 다섯 개의 소문자 모음과 일치합니다. 마찬가지로, 두번째 케이스는 모든 소문자 영어 자음과 일치합니다. 마지막으로 `default` 케이스는 다른 문자와 일치합니다. 

*Compound cases can also include value bindings. All of the patterns of a compound case have to include the same set of value bindings, and each binding has to get a value of the same type from all of the patterns in the compound case. This ensures that, no matter which part of the compound case matched, the code in the body of the case can always access a value for the bindings and that the value always has the same type.*

복합 케이스에는 값 바인딩도 포함될 수 있습니다. 복합 케이스의 모든 패턴은 동일한 값 바인딩 세트를 포함해야 하며, 각각의 바인딩은 복합 케이스 내의 모든 패턴으로부터 동일한 타입의 값을 얻어야 합니다. 이렇게 하면 복합 케이스의 어느 부분이 일치하는지에 관계없이 케이스 본체의 코드가 바인딩에 대한 값에 항상 엑세스할 수 있고 값이 항상 동일한 타입을 갖도록 할 수 있습니다.

```swift
let stillAnotherPoint = (9, 0)
switch stillAnotherPoint {
case (let distance, 0), (0, let distance):
    print("On an axis, \(distance) from the origin")
default:
    print("Not on an axis")
}
// Prints "On an axis, 9 from the origin"
```

*The `case` above has two patterns: `(let distance, 0)` matches points on the x-axis and `(0, let distance)` matches points on the y-axis. Both patterns include a binding for `distance` and `distance` is an integer in both patterns—which means that the code in the body of the `case` can always access a value for `distance`.*

위의 `case`는 두 가지 패턴을 가지고 있습니다 : `(let distance, 0)`은 x축의 점과 일치하고 `(0, let distance)`는 y축의 점과 일치합니다. 두 패턴 모두 distance 에 대한 바인딩을 포함하며 `distance`는 두 패턴 모두에서 정수입니다. 즉, `case`의 본문의 코드는 항상 `distance`에 대한 값에 접근할 수 있습니다.


