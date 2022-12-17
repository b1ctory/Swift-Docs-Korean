## *While Loops*

*A `while` loop performs a set of statements until a condition becomes `false`. These kinds of loops are best used when the number of iterations isn’t known before the first iteration begins. Swift provides two kinds of `while` loops:*

- *`while` evaluates its condition at the start of each pass through the loop.*

- *`repeat`-`while` evaluates its condition at the end of each pass through the loop.*

### *While*

*A `while` loop starts by evaluating a single condition. If the condition is `true`, a set of statements is repeated until the condition becomes `false`.*

*Here’s the general form of a `while` loop:*

```swift
while condition {
    statements
}
```

*This example plays a simple game of Snakes and Ladders (also known as Chutes and Ladders):*

![](https://docs.swift.org/swift-book/_images/snakesAndLadders_2x.png)

*The rules of the game are as follows:*

- *The board has 25 squares, and the aim is to land on or beyond square 25.*

- *The player’s starting square is “square zero”, which is just off the bottom-left corner of the board.*

- *Each turn, you roll a six-sided dice and move by that number of squares, following the horizontal path indicated by the dotted arrow above.*

- *If your turn ends at the bottom of a ladder, you move up that ladder.*

- *If your turn ends at the head of a snake, you move down that snake.*

*The game board is represented by an array of `Int` values. Its size is based on a constant called `finalSquare`, which is used to initialize the array and also to check for a win condition later in the example. Because the players start off the board, on “square zero”, the board is initialized with 26 zero `Int` values, not 25.*

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
```

*Some squares are then set to have more specific values for the snakes and ladders. Squares with a ladder base have a positive number to move you up the board, whereas squares with a snake head have a negative number to move you back down the board.*

```swift
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
```

*Square 3 contains the bottom of a ladder that moves you up to square 11. To represent this, `board[03]` is equal to `+08`, which is equivalent to an integer value of `8` (the difference between `3` and `11`). To align the values and statements, the unary plus operator (`+i`) is explicitly used with the unary minus operator (`-i`) and numbers lower than `10` are padded with zeros. (Neither stylistic technique is strictly necessary, but they lead to neater code.)*

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

*After rolling the dice, the player moves forward by `diceRoll` squares. It’s possible that the dice roll may have moved the player beyond square 25, in which case the game is over. To cope with this scenario, the code checks that `square` is less than the `board` array’s `count` property. If `square` is valid, the value stored in `board[square]` is added to the current `square` value to move the player up or down any ladders or snakes.*

> *NOTE*
> 
> *If this check isn’t performed, `board[square]` might try to access a value outside the bounds of the `board` array, which would trigger a runtime error.*

*The current `while` loop execution then ends, and the loop’s condition is checked to see if the loop should be executed again. If the player has moved on or beyond square number `25`, the loop’s condition evaluates to `false` and the game ends.*

*A `while` loop is appropriate in this case, because the length of the game isn’t clear at the start of the `while` loop. Instead, the loop is executed until a particular condition is satisfied.*

### *Repeat-While*

*The other variation of the `while` loop, known as the `repeat`-`while` loop, performs a single pass through the loop block first, before considering the loop’s condition. It then continues to repeat the loop until the condition is `false`.*

> *NOTE*
> 
> *The `repeat`-`while` loop in Swift is analogous to a `do`-`while` loop in other languages.*

*Here’s the general form of a `repeat`-`while` loop:*

```swift
repeat {
    statements
} while condition
```

*Here’s the Snakes and Ladders example again, written as a `repeat`-`while` loop rather than a `while` loop. The values of `finalSquare`, `board`, `square`, and `diceRoll` are initialized in exactly the same way as with a `while` loop.*

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

*In this version of the game, the first action in the loop is to check for a ladder or a snake. No ladder on the board takes the player straight to square 25, and so it isn’t possible to win the game by moving up a ladder. Therefore, it’s safe to check for a snake or a ladder as the first action in the loop.*

*At the start of the game, the player is on “square zero”. `board[0]` always equals `0` and has no effect.*

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

*The loop’s condition (`while square < finalSquare`) is the same as before, but this time it’s not evaluated until the end of the first run through the loop. The structure of the `repeat`-`while` loop is better suited to this game than the `while` loop in the previous example. In the `repeat`-`while` loop above, `square += board[square]` is always executed immediately after the loop’s `while` condition confirms that `square` is still on the board. This behavior removes the need for the array bounds check seen in the `while` loop version of the game described earlier.*
