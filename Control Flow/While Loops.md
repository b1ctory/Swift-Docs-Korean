## *While Loops*

*A `while` loop performs a set of statements until a condition becomes `false`. These kinds of loops are best used when the number of iterations isn’t known before the first iteration begins. Swift provides two kinds of `while` loops:*

`while` 루프는 조건이 `false`가 될 때까지 일련의 구문을 수행합니다. 이러한 종류의 루프는 첫 번째 반복이 시작되기 전에 반복 횟수를 알 수 없을 때 가장 잘 사용됩니다. Swift는 두 종류의 `while` 루프를 제공합니다.

- *`while` evaluates its condition at the start of each pass through the loop.*
  
  `while` 루프를 통과할 때 시작마다 상태를 평가합니다.

- *`repeat`-`while` evaluates its condition at the end of each pass through the loop.*
  
  `repeat`-`while`은 루프가 통과할 때 끝마다 상태를 평가합니다.

### *While*

*A `while` loop starts by evaluating a single condition. If the condition is `true`, a set of statements is repeated until the condition becomes `false`.*

`while`루프는 단일 조건을 평가하는 것으로 시작합니다. 조건이 `true`이면 조건이 `false`가 될 때까지 일련의 구문이 반복됩니다.

*Here’s the general form of a `while` loop:*

다음은 `while` 루프의 일반적인 형태입니다.

```swift
while condition {
    statements
}
```

*This example plays a simple game of Snakes and Ladders (also known as Chutes and Ladders):*

다음 예제에서는 뱀사다리라는 간단한 게임 (Chutes and Ladders 라고도 알려진)을 플레이합니다.

![](https://docs.swift.org/swift-book/_images/snakesAndLadders_2x.png)

*The rules of the game are as follows:*

게임의 규칙은 다음과 같습니다.

- *The board has 25 squares, and the aim is to land on or beyond square 25.*
  
  보드는 25개의 정사각형을 가지고 있으며, 목표는 25개의 정사각형 이상에 착륙하는 것입니다.

- *The player’s starting square is “square zero”, which is just off the bottom-left corner of the board.*
  
  플레이어의 출발 사각형은 “square zero”로 보드의 왼쪽 하단 모서리에 있습니다.

- *Each turn, you roll a six-sided dice and move by that number of squares, following the horizontal path indicated by the dotted arrow above.*
  
  회전할 때마다 당신은 여섯 면의 주사위를 굴리고 위에 점선 화살표로 표시된 수평 경로를 따라 그 정사각형 수만큼 움직입니다.

- *If your turn ends at the bottom of a ladder, you move up that ladder.*
  
  만약 당신의 차례가 사다리의 맨 아래에서 끝나면 당신은 그 사다리를 올라갑니다.

- *If your turn ends at the head of a snake, you move down that snake.*
  
  만약 당신의 차례가 뱀 머리에서 끝나면, 그 뱀 아래로 내려갑니다.

*The game board is represented by an array of `Int` values. Its size is based on a constant called `finalSquare`, which is used to initialize the array and also to check for a win condition later in the example. Because the players start off the board, on “square zero”, the board is initialized with 26 zero `Int` values, not 25.*

게임 보드는 `Int` 값의 배열로 표시됩니다. 크기는 배열을 초기화하고 예제의 뒷부분에서 승리 조건을 확인하는데 사용되는 `finalSquare`라는 상수를 기반으로 합니다. 플레이어는 square zero에서 보드를 시작하기 때문에 보드는 25가 아닌 26개의 0인 `Int`값으로 초기화됩니다.

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
```

*Some squares are then set to have more specific values for the snakes and ladders. Squares with a ladder base have a positive number to move you up the board, whereas squares with a snake head have a negative number to move you back down the board.*

그런 다음 일부 사각형은 뱀과 사다리에 대해 더 구체적인 값을 갖도록 설정됩니다. 사다리의 밑면이 있는 사각형은 보드 위로 이동하는 양수를 가지고 있는 반면, 뱀 머리가 있는 사각형은 보드 아래로 이동하는 음수를 가지고 있습니다. 

```swift
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
```

*Square 3 contains the bottom of a ladder that moves you up to square 11. To represent this, `board[03]` is equal to `+08`, which is equivalent to an integer value of `8` (the difference between `3` and `11`). To align the values and statements, the unary plus operator (`+i`) is explicitly used with the unary minus operator (`-i`) and numbers lower than `10` are padded with zeros. (Neither stylistic technique is strictly necessary, but they lead to neater code.)*

사각형 3에는 사각형 11까지 이동하는 사다리의 바닥이 포함되어 있습니다. 이를 표현하기 위해 `board[03]`는 `+08`과 같으며 이는 `8` (`3`과 `11` 사이)의 정수값과 같습니다. 값과 구문을 정렬하기 위해 단항 더하기 연산자 (`+i`)는 단항 빼기 연산자 (`-i`)와 함께 명시적으로 사용되고 `10`보다 작은 숫자는 `0`으로 패딩됩니다. (두 가지 스타일 기법 모두 엄격하기 필요하지는 않지만, 더 깔끔한 코드로 이어집니다.)

```swift
var square = 0
var diceRoll = 0
while square < finalSquare {
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
    if square < board.count {
        // if we're still on the board, move up or down for a snake or a ladder
        square += board[square]
    }
}
print("Game over!")
```

*The example above uses a very simple approach to dice rolling. Instead of generating a random number, it starts with a `diceRoll` value of `0`. Each time through the `while` loop, `diceRoll` is incremented by one and is then checked to see whether it has become too large. Whenever this return value equals `7`, the dice roll has become too large and is reset to a value of `1`. The result is a sequence of `diceRoll` values that’s always `1`, `2`, `3`, `4`, `5`, `6`, `1`, `2` and so on.*

위의 예는 주사위 굴리기에 매우 간단한 접근법을 사용합니다. 임의의 숫자를 생성하는 대신 `diceRoll` 값 `0`으로 시작합니다. `while` 루프를 통과할 때마다 `diceRoll` 이 1씩 증가한다음 너무 커졌는지 확인합니다. 이 반환값이 `7`이 될 때마다 주사위 굴림이 너무 커져서 값이 `1`로 재설정됩니다. 결과는 항상  `1`, `2`, `3`, `4`, `5`, `6`, `1`, `2` 등인 일련의 `diceRoll` 값입니다.

*After rolling the dice, the player moves forward by `diceRoll` squares. It’s possible that the dice roll may have moved the player beyond square 25, in which case the game is over. To cope with this scenario, the code checks that `square` is less than the `board` array’s `count` property. If `square` is valid, the value stored in `board[square]` is added to the current `square` value to move the player up or down any ladders or snakes.*

주사위를 굴린 후 플레이어는 `diceRoll`의 제곱만큼 앞으로 이동합니다. 주사위 굴림이 플레이어를 제곱 25 이상으로 이동시켰을 가능성이 있으며, 이 경우 게임이 종료됩니다. 이 시나리오에 대처하기 위해 코드는 `square`가 `board` 배열의 `count` 속성보다 작은지 확인합니다. `square`가 유효하면 `board[square]` 에 저장된 값이 현재 `square` 값에 추가되어 플레이어가 사다리나 뱀을 위아래로 움직일 수 있습니다.

> *NOTE*
> 
> *If this check isn’t performed, `board[square]` might try to access a value outside the bounds of the `board` array, which would trigger a runtime error.*
> 
> 이 검사를 수행하지 않으면 `board[square]`가 `board` 배열의 범위 밖에 있는 값에 엑세스하려고 할 수 있으므로 런타임 오류가 트리거됩니다.

*The current `while` loop execution then ends, and the loop’s condition is checked to see if the loop should be executed again. If the player has moved on or beyond square number `25`, the loop’s condition evaluates to `false` and the game ends.*

현재의 `while` 루프 실행이 종료되고 루프 상태가 다시 실행되어야 하는지 확인합니다. 플레이어가 제곱수 `25` 이상으로 이동하면 루프 상태가 `거짓`으로 평가되고 게임이 종료됩니다.

*A `while` loop is appropriate in this case, because the length of the game isn’t clear at the start of the `while` loop. Instead, the loop is executed until a particular condition is satisfied.*

이 경우 `while` 루프는 `while` 루프의 시작 부분에서 게임의 길이가 명확하지 않기 때문에 적절합니다. 대신, 루프는 특정 조건이 충족될 때까지 실행됩니다.

### *Repeat-While*

*The other variation of the `while` loop, known as the `repeat`-`while` loop, performs a single pass through the loop block first, before considering the loop’s condition. It then continues to repeat the loop until the condition is `false`.*

`while` 루프의 다른 변형인 `repeat`-`while` 루프는 루프의 조건을 고려하기 전에 먼저 루프 블록을 통과합니다. 그런 다음 조건이 `false`가 될 때까지 루프를 계속 반복합니다.

> *NOTE*
> 
> *The `repeat`-`while` loop in Swift is analogous to a `do`-`while` loop in other languages.*
> 
> Swift의 `repeat`-`while` 문은 다른 언어의 `do`-`while` 루프와 유사합니다.

*Here’s the general form of a `repeat`-`while` loop:*

다음은 `repeat`-`while` 루프의 일반적인 형태입니다.

```swift
repeat {
    statements
} while condition
```

*Here’s the Snakes and Ladders example again, written as a `repeat`-`while` loop rather than a `while` loop. The values of `finalSquare`, `board`, `square`, and `diceRoll` are initialized in exactly the same way as with a `while` loop.*

여기에 다시 `while` 루프가 아니라 `repeat`-`while` 루프로 쓰여진 뱀과 사다리의 예시가 있습니다. `finalSquare`, `board`, `square` 그리고 `diceRoll` 의 값은 `while` 루프와 정확히 같은 방식으로 초기화됩니다.

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

*In this version of the game, the first action in the loop is to check for a ladder or a snake. No ladder on the board takes the player straight to square 25, and so it isn’t possible to win the game by moving up a ladder. Therefore, it’s safe to check for a snake or a ladder as the first action in the loop.*

이 버전의 게임에서 루프의 첫 번째 동작은 사다리나 뱀을 확인하는 것입니다. 보드의 어떤 사다리도 플레이어를 사각형 25로 곧장 데려가지 않기 때문에 사다리를 올라감으로써 게임에서 이길 수 없습니다. 따라서 루프의 첫번째 동작으로 뱀이나 사다리를 확인하는 것이 안전합니다.

*At the start of the game, the player is on “square zero”. `board[0]` always equals `0` and has no effect.*

게임을 시작할 때 플레이어는 "square zero"에 있으며 `board[0]`는 항상 0과 같으며 아무 효과도 없습니다. 

```swift
repeat {
    // move up or down for a snake or ladder
    square += board[square]
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
} while square < finalSquare
print("Game over!")
```

*After the code checks for snakes and ladders, the dice is rolled and the player is moved forward by `diceRoll` squares. The current loop execution then ends.*

코드과 뱀과 사다리를 확인한 후 주사위를 굴리고 플레이어는 `diceRoll` 사각형 앞으로 이동합니다. 그러면 현재 루프 실행이 종료됩니다.

*The loop’s condition (`while square < finalSquare`) is the same as before, but this time it’s not evaluated until the end of the first run through the loop. The structure of the `repeat`-`while` loop is better suited to this game than the `while` loop in the previous example. In the `repeat`-`while` loop above, `square += board[square]` is always executed immediately after the loop’s `while` condition confirms that `square` is still on the board. This behavior removes the need for the array bounds check seen in the `while` loop version of the game described earlier.*

루프의 조건 (`while square < finalSquare`)은 이전과 동일하지만, 이번에는 루프를 통과하는 첫번째 런이 끝날때까지 평가되지 않습니다. 앞의 예에서 말한 `while` 루프보다 `repeat`-`while` 루프의 구조가 이 게임에 더 적합합니다. 위의 `repeat`-`while` 루프에서 `square += board[square]`는 루프의 `while` 조건이 `square`이 아직 보드 위에 있다는 것을 확인한 즉시 실행됩니다. 이 동작은 앞에서 설명한 게임의 `while` 루프 버전에서 볼 수 있는 배열 경게 체크의 필요성을 제거합니다.
