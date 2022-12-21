## *Control Transfer Statements : 제어 전송문*

*Control transfer statements change the order in which your code is executed, by transferring control from one piece of code to another. Swift has five control transfer statements:*

제어 전송문은 한 코드에서 다른 코드로 제어를 전송해서 코드 실행 순서를 변경합니다. Swift는 5개의 제어 전달문을 가지고 있습니다.

- *`continue`*

- *`break`*

- *`fallthrough`*

- *`return`*

- *`throw`*

*The `continue`, `break`, and `fallthrough` statements are described below. The `return` statement is described in [Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html), and the `throw` statement is described in [Propagating Errors Using Throwing Functions](https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html#ID510).*

`continue`, `break` 그리고 `fallthrough` 는 아래에 설명되어 있습니다. `return` 문은 [링크]에, `throw`문은 [링크]에 설명되어 있습니다.

### *Continue*

*The `continue` statement tells a loop to stop what it’s doing and start again at the beginning of the next iteration through the loop. It says “I am done with the current loop iteration” without leaving the loop altogether.*

`continue`문은 루프를 통해 수행중인 작업을 중지하고 다음 반복의 시작 부분에서 다시 시작하도록 루프를 알려줍니다. 루프를 완전히 벗어나지 않고 "현재 루프 반복을 완료했습니다."라고 말합니다.

*The following example removes all vowels and spaces from a lowercase string to create a cryptic puzzle phrase:*

다음 예제는 소문자 문자열에서 모든 모음과 공백을 제거해서 암호화된 퍼즐 구문을 만듭니다.

```swift
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
for character in puzzleInput {
    if charactersToRemove.contains(character) {
        continue
    }
    puzzleOutput.append(character)
}
print(puzzleOutput)
// Prints "grtmndsthnklk"
```

*The code above calls the `continue` keyword whenever it matches a vowel or a space, causing the current iteration of the loop to end immediately and to jump straight to the start of the next iteration.*

위의 코드는 모음이나 공백과 일치할 때마다 `continue` 키워드를 호출해서 루프의 현재 반복이 즉시 종료되고 다음 반복의 시작으로 바로 이동합니다.

### *Break*

*The `break` statement ends execution of an entire control flow statement immediately. The `break` statement can be used inside a `switch` or loop statement when you want to terminate the execution of the `switch` or loop statement earlier than would otherwise be the case.*

`break`문은 전체 제어 흐름문의 실행을 즉시 종료합니다. `break`문은 `switch` 혹은 loop 문의 실행을 그렇지 않은 경우보다 빨리 종료하려는 경우에 `switch` 혹은 `loop`문 안에서 사용할 수 있습니다.

#### *Break in a Loop Statement : 루프문 깨기*

*When used inside a loop statement, `break` ends the loop’s execution immediately and transfers control to the code after the loop’s closing brace (`}`). No further code from the current iteration of the loop is executed, and no further iterations of the loop are started.*

루프 문 안에서 `break`를 사용하면 루프의 실행이 즉시 종료되고 루프의 닫힘 괄호(`}`) 후에 코드로 제어가 전달됩니다. 루프의 현재 반복에서 더이상 코드가 실행되지 않으며 루프가 더이상 반복이 시작되지 않습니다.

#### *Break in a Switch Statement : Switch문 깨기*

*When used inside a `switch` statement, `break` causes the `switch` statement to end its execution immediately and to transfer control to the code after the `switch` statement’s closing brace (`}`).*

`break`를 `switch`문 안에서 사용하면 `switch`문이 즉시 실행을 종료하고 `switch`  문의 닫힘 괄호(`}`) 후에 코드로 제어를 전송합니다.

*This behavior can be used to match and ignore one or more cases in a `switch` statement. Because Swift’s `switch` statement is exhaustive and doesn’t allow empty cases, it’s sometimes necessary to deliberately match and ignore a case in order to make your intentions explicit. You do this by writing the `break` statement as the entire body of the case you want to ignore. When that case is matched by the `switch` statement, the `break` statement inside the case ends the `switch` statement’s execution immediately.*

이 동작은 `switch`문에서 하나 이상의 케이스를 일치시키고 무시하는데 사용할 수 있습니다. Swift의 `switch`문은 포괄적이고 빈 케이스를 허용하지 않기 때문에 의도를 분명히 하기 위해 의도적으로 케이스를 일치시키고 무시하는 것이 필요할 때가 있습니다. 이는 무시하고 싶은 케이스의 전체 내용으로 `break` 를 작성함으로써 이루어집니다. 이 경우 `switch` 문과 일치하면 `break`문은 `switch` 문의 실행을 즉시 종료합니다.

> *NOTE*
> 
> *A `switch` case that contains only a comment is reported as a compile-time error. Comments aren’t statements and don’t cause a `switch` case to be ignored. Always use a `break` statement to ignore a `switch` case.*
> 
> 주석만 포함된 `switch` 케이스는 컴파일 타임 에러로 보고됩니다. 주석은 구문이 아니면 `switch` 케이스를 무시하는 원인이 되지 않습니다. `switch` 케이스를 무시하려면 항상 `break` 구문을 사용하세요.

*The following example switches on a `Character` value and determines whether it represents a number symbol in one of four languages. For brevity, multiple values are covered in a single `switch` case.*

다음 예시에서는 `Character` 값을 켜고 4개 언어 중 하나로 숫자 기호를 나타내는지 여부를 확인합니다. 간략화를 위해 다중값은 단일 `switch` 케이스에서 다룹니다.

```swift
let numberSymbol: Character = "三"  // Chinese symbol for the number 3
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "١", "一", "๑":
    possibleIntegerValue = 1
case "2", "٢", "二", "๒":
    possibleIntegerValue = 2
case "3", "٣", "三", "๓":
    possibleIntegerValue = 3
case "4", "٤", "四", "๔":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    print("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    print("An integer value couldn't be found for \(numberSymbol).")
}
// Prints "The integer value of 三 is 3."
```

*This example checks `numberSymbol` to determine whether it’s a Latin, Arabic, Chinese, or Thai symbol for the numbers `1` to `4`. If a match is found, one of the `switch` statement’s cases sets an optional `Int?` variable called `possibleIntegerValue` to an appropriate integer value.*

이 예시에서는 `numberSymbol`를 확인해서 숫자 `1`에서 `4`의 라틴, 아랍, 중국 혹은 태국 기호인지 확인합니다. 일치하는 항목이 발견되면 `switch` 문의 케이스 중 하나가 `possibleIntegerValue`라고 불리는 옵셔널인 `Int?`를 적절한 정수 값으로 설정합니다. 

*After the `switch` statement completes its execution, the example uses optional binding to determine whether a value was found. The `possibleIntegerValue` variable has an implicit initial value of `nil` by virtue of being an optional type, and so the optional binding will succeed only if `possibleIntegerValue` was set to an actual value by one of the `switch` statement’s first four cases.*

`switch` 문 실행이 완료된 후 예제에서는 옵셔널 바인딩을 사용해서 값을 찾았는지 여부를 확인합니다. `possibleIntegerValue`변수는 옵셔널 타입이기 때문에 암시적인 초기값이 `nil` 이므로 `possibleIntegerValue`이 switch문의 처음 네가지 경우 중 하나에 의해 실제 값으로 설정될 경우에만 옵셔널 바인딩이 성공합니다

*Because it’s not practical to list every possible `Character` value in the example above, a `default` case handles any characters that aren’t matched. This `default` case doesn’t need to perform any action, and so it’s written with a single `break` statement as its body. As soon as the `default` case is matched, the `break` statement ends the `switch` statement’s execution, and code execution continues from the `if let` statement.*

위의 예에서 모든 `Character` 값을 나열하는 것은 실용적이지 않기 때문에 `default` 케이스는 일치하지 않는 문자를 처리합니다. 이 `default` 케이스는 아무런 조치를 취할 필요가 없기 때문에 `break` 문 하나를 본문으로해서 작성됩니다. `default` 케이스가 일치하는 즉시 `break` 문은 `switch`문의 실행을 종료하고 `if let` 구문부터 코드 실행을 계속합니다.



### *Fallthrough*

*In Swift, `switch` statements don’t fall through the bottom of each case and into the next one. That is, the entire `switch` statement completes its execution as soon as the first matching case is completed. By contrast, C requires you to insert an explicit `break` statement at the end of every `switch` case to prevent fallthrough. Avoiding default fallthrough means that Swift `switch` statements are much more concise and predictable than their counterparts in C, and thus they avoid executing multiple `switch` cases by mistake.*

Swift에서 `switch`문은 각각의 케이스의 끝을 지나 다음 케이스로 넘어가는 것이 아닙니다. 즉, 전체 `switch` 문은 첫번째 일치 케이스가 완료되는 즉시 실행을 완료합니다. 대조적으로 C는 실패를 방지하기 위해 모든 `switch` 케이스의 끝에 명시적인 `break` 문을 삽입할 것을 요구합니다. 디폴트 fallthrough를 피한다는 것은 Swift의 `switch`문이 C에 있는 것보다 훨씬 간결하고 예측 가능하다는 것을 의미하므로 실수로 여러 `switch` 사레를 실행하는 것을 피한다는 것입니다.

*If you need C-style fallthrough behavior, you can opt in to this behavior on a case-by-case basis with the `fallthrough` keyword. The example below uses `fallthrough` to create a textual description of a number.*

C 스타일의 fallthrough 동작이 필요한 경우 `fallthrough`키워드를 사용해서 케이스-바이-케이스로 이 동작을 선택할 수 있습니다. 아래의 예제는 `fallthrough`를 사용해서 숫자에 대한 텍스트 설명을 작성합니다.

```swift
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
print(description)
// Prints "The number 5 is a prime number, and also an integer."
```

*This example declares a new `String` variable called `description` and assigns it an initial value. The function then considers the value of `integerToDescribe` using a `switch` statement. If the value of `integerToDescribe` is one of the prime numbers in the list, the function appends text to the end of `description`, to note that the number is prime. It then uses the `fallthrough` keyword to “fall into” the `default` case as well. The `default` case adds some extra text to the end of the description, and the `switch` statement is complete.*

이 예에서는 `description`이라는 새 `String` 변수를 선언하고 초기값을 할당합니다. 그런 다음 함수는 switch문을 사용해서 `integerToDescribe`값을 고려합니다. `integerToDescribe`값이 목록의 소수 중 하나인 경우 함수는 소수임을 나타내기 위해 `description` 끝에 텍스트를 추가합니다. 그런 다음 `fallthrough` 키워드를 사용해서 `default` 케이스에 "떨어지게" 만듭니다. `default` 케이스는 설명 끝에 몇가지 텍스트를 추가하고 `switch` 구문은 완료됩ㄴ다.

*Unless the value of `integerToDescribe` is in the list of known prime numbers, it isn’t matched by the first `switch` case at all. Because there are no other specific cases, `integerToDescribe` is matched by the `default` case.*

`integerToDescribe`의 값이 알려진 소수 목록에 없는 한 첫번째 switch케이스와 전혀 일치하지 않습니다. 다른 특별한 케이스가 없기 때문에 `integerToDescribe`은 `default` 케이스와 일치합니다.

*After the `switch` statement has finished executing, the number’s description is printed using the `print(_:separator:terminator:)` function. In this example, the number `5` is correctly identified as a prime number.*

switch문 실행이 끝나면 `print(_:separator:terminator:)` 함수를 사용해서 번호 셜명이 출력됩니다. 이 예시에서는, 숫자 `5`가 소수로 정확하게 식별됩니다.

> *NOTE*
> 
> *The `fallthrough` keyword doesn’t check the case conditions for the `switch` case that it causes execution to fall into. The `fallthrough` keyword simply causes code execution to move directly to the statements inside the next case (or `default` case) block, as in C’s standard `switch` statement behavior.*
> 
> `fallthrough` 키워드는 실행을 유발하는 `switch` 케이스의 실행 조건을 체크하지 않습니다. `fallthrough` 키워드는 C의 표준 `switch`문 동작에서와 같이 코드 실행을 다음 케이스 (혹은 `default` 케이스) 블록 내의 구문으로 직접 이동시킵니다.



### *Labeled Statements : 레이블이 달린 구문*

*In Swift, you can nest loops and conditional statements inside other loops and conditional statements to create complex control flow structures. However, loops and conditional statements can both use the `break` statement to end their execution prematurely. Therefore, it’s sometimes useful to be explicit about which loop or conditional statement you want a `break` statement to terminate. Similarly, if you have multiple nested loops, it can be useful to be explicit about which loop the `continue` statement should affect.*

Swift에서 루프 및 조건문을 다른 루프 및 조건문 내부에 중첩해서 제어 흐름 구조를 만들 수 있습니다. 그러나 루프와 조건문은 모두 `break` 구문을 사용해서 실행을 조기에 종료할 수 있습니다. 따라서, `break` 구문을 종료할 루프 혹은 조건문에 대해 명시적으로 설명하는 것이 유용할 수 있습니다. 마찬가지로 중첩 루프가 여러개 있는 경우 `continue` 구문이 어떤 루프에 영향을 미치는지 명시적으로 설명하는 것이 유용할 수 있습니다.

*To achieve these aims, you can mark a loop statement or conditional statement with a statement label. With a conditional statement, you can use a statement label with the `break` statement to end the execution of the labeled statement. With a loop statement, you can use a statement label with the `break` or `continue` statement to end or continue the execution of the labeled statement.*

이러한 목적을 달성하기 위해 루프문 혹은 조건문을 구문 레이블로 표시할 수 있습니다. 조건문의 경우 `break` 문과 함께 구문 레이블을 사용해서 레이블이 지정된 구문의 실행을 끝낼 수 있습니다. 루프문을 사용하는 경우 `break` 혹은 `continue`문과 함께 구문 레이블을 사용해서 레이블이 지정된 구문의 실행을 종료하거나 계속할 수 있습니다.

*A labeled statement is indicated by placing a label on the same line as the statement’s introducer keyword, followed by a colon. Here’s an example of this syntax for a `while` loop, although the principle is the same for all loops and `switch` statements:*

레이블이 지정된 구문소개자는 키워드와 동일한 줄에 레이블을 배치한 다음 콜론을 표시합니다. 다음은 `while` 루프에 대한 이 구문은 예시이지만, 원리는 모든 루프와 `switch` 문에 대해 동일합니다.

```swift
label name: while condition {
    statements
}
```

*The following example uses the `break` and `continue` statements with a labeled `while` loop for an adapted version of the Snakes and Ladders game that you saw earlier in this chapter. This time around, the game has an extra rule:*

다음 예제는 이 장의 앞부분에서 본 뱀과 사다리 게임의 각색 버전에 대해 `while` 루프가 있는 `break` 및 `continue` 문을 사용합니다. 이번에는 게임이 추가 규칙을 가집니다 :

- *To win, you must land exactly on square 25.*
  
  이기기 위해서는 정확히 25 사각형에 착륙해야합니다. 

*If a particular dice roll would take you beyond square 25, you must roll again until you roll the exact number needed to land on square 25.*

만약 특정 주사위 굴림이 당신을 사각형 25를 넘어서게 한다면, 당신은 사각형 25에 착륙하는데 필요한 정확한 숫자를 굴릴 때까지 다시 굴려야 합니다. 

*The game board is the same as before.*

게임 보드는 이전과 같습니다.

![](https://docs.swift.org/swift-book/_images/snakesAndLadders_2x.png)

*The values of `finalSquare`, `board`, `square`, and `diceRoll` are initialized in the same way as before:*

 `finalSquare`, `board`, `square`, 그리고 `diceRoll`의 값은 이전과 동일한 방식으로 초기화됩니다.

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

*This version of the game uses a `while` loop and a `switch` statement to implement the game’s logic. The `while` loop has a statement label called `gameLoop` to indicate that it’s the main game loop for the Snakes and Ladders game.*

이 버전의 게임은 게임의 로직을 구현하기 위해 `while` 루프와 `switch` 구문을 사용합니다. `while` 루프에는 `gameLoop`라고 불리는 메인 게임이 뱀과 사다리 게임이라는 것을 가리키는 레이블이 달린 구문이 있습니다. 

*The `while` loop’s condition is `while square != finalSquare`, to reflect that you must land exactly on square 25.*

while 루프의 조건은  `while square != finalSquare`로 정확히 25에 착지해야 함을 나타냅니다.

```swift
gameLoop: while square != finalSquare {
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    switch square + diceRoll {
    case finalSquare:
        // diceRoll will move us to the final square, so the game is over
        break gameLoop
    case let newSquare where newSquare > finalSquare:
        // diceRoll will move us beyond the final square, so roll again
        continue gameLoop
    default:
        // this is a valid move, so find out its effect
        square += diceRoll
        square += board[square]
    }
}
print("Game over!")
```

*The dice is rolled at the start of each loop. Rather than moving the player immediately, the loop uses a `switch` statement to consider the result of the move and to determine whether the move is allowed:*

주사위는 각 루프의 시작 부분에서 굴립니다. 루프는 플레이어를 즉시 이동시키는 대신, switch 구문을 사용해서 이동의 결과를 고려하고 이동이 허용되는지 여부를 결정합니다.

- *If the dice roll will move the player onto the final square, the game is over. The `break gameLoop` statement transfers control to the first line of code outside of the `while` loop, which ends the game.*
  
  주사위 굴림이 플레이어를 최종 사각형으로 이동시키면 게임은 종료됩니다. `break gameLoop` 구문은 제어권을 `while` 루프 밖의 코드의 첫번째 줄로 이전해서 게임을 종료합니다.

- *If the dice roll will move the player beyond the final square, the move is invalid and the player needs to roll again. The `continue gameLoop` statement ends the current `while` loop iteration and begins the next iteration of the loop.*
  
  주사위 굴림이 플레이어를 최종 사각형 너머로 이동시킬 경우, 이동은 무효이며 플레이어는 주사위를 다시 굴려야 합니다. `continue gameLoop`문은 현재의 `while` 루프문의 순환을 끝내고 루프의 다음 반복을 시작합니다.

- *In all other cases, the dice roll is a valid move. The player moves forward by `diceRoll` squares, and the game logic checks for any snakes and ladders. The loop then ends, and control returns to the `while` condition to decide whether another turn is required.*
  
  다른 모든 경우에는, 주사위 굴리기가 유효한 동작입니다. 플레이어는 `diceRoll`의 사각형보다 앞으로 이동하고 게임 로직은 뱀과 사다리가 있는지 확인합니다. 그런 다음 루프가 종료되고 제어는 다시 회전이 필요한지 여부를 결정하기 위해 `while` 상태로 돌아갑니다.

> *NOTE*
> 
> *If the `break` statement above didn’t use the `gameLoop` label, it would break out of the `switch` statement, not the `while` statement. Using the `gameLoop` label makes it clear which control statement should be terminated.*
> 
> 위의 `break` 구문이 `gameLoop` 레이블을 사용하지 않았다면 `while` 구문이 아니라 `switch` 문을 탈출했을 것입니다. `gameLoop` 레이블을 사용하면 어떤 제어문을 종료해야 하는지를 명확하게 합니다.
> 
> *It isn’t strictly necessary to use the `gameLoop` label when calling `continue gameLoop` to jump to the next iteration of the loop. there’s only one loop in the game, and therefore no ambiguity as to which loop the `continue` statement will affect. However, there’s no harm in using the `gameLoop` label with the `continue` statement. Doing so is consistent with the label’s use alongside the `break` statement and helps make the game’s logic clearer to read and understand.*
> 
> 다음 루프의 반복으로 점프하는`continue gameLoop`를 호출할 때 `gameLoop`를 반드시 사용할 필요는 없습닏. 게임에는 루프가 하나밖에 없기 때문에 `continue` 구문이 루프에 어떤 영향을 미칠지에 대한 모호성은 없습니다. 하지만 이 `gameLoop`를 `continue` 문과 함께 사용하는 것은 해롭지 않습니다. 이는 레이블이 break 구문과 함께 사용하는 것과 일치하며, 게임의 로직을 읽고 이해하는데 도움이 됩니다.


