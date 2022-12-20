## *Control Transfer Statements*

*Control transfer statements change the order in which your code is executed, by transferring control from one piece of code to another. Swift has five control transfer statements:*

- *`continue`*

- *`break`*

- *`fallthrough`*

- *`return`*

- *`throw`*

*The `continue`, `break`, and `fallthrough` statements are described below. The `return` statement is described in [Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html), and the `throw` statement is described in [Propagating Errors Using Throwing Functions](https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html#ID510).*



### *Continue*

*The `continue` statement tells a loop to stop what it’s doing and start again at the beginning of the next iteration through the loop. It says “I am done with the current loop iteration” without leaving the loop altogether.*

*The following example removes all vowels and spaces from a lowercase string to create a cryptic puzzle phrase:*

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



### *Break*

*The `break` statement ends execution of an entire control flow statement immediately. The `break` statement can be used inside a `switch` or loop statement when you want to terminate the execution of the `switch` or loop statement earlier than would otherwise be the case.*



#### *Break in a Loop Statement*

*When used inside a loop statement, `break` ends the loop’s execution immediately and transfers control to the code after the loop’s closing brace (`}`). No further code from the current iteration of the loop is executed, and no further iterations of the loop are started.*

#### *Break in a Switch Statement*

*When used inside a `switch` statement, `break` causes the `switch` statement to end its execution immediately and to transfer control to the code after the `switch` statement’s closing brace (`}`).*

*This behavior can be used to match and ignore one or more cases in a `switch` statement. Because Swift’s `switch` statement is exhaustive and doesn’t allow empty cases, it’s sometimes necessary to deliberately match and ignore a case in order to make your intentions explicit. You do this by writing the `break` statement as the entire body of the case you want to ignore. When that case is matched by the `switch` statement, the `break` statement inside the case ends the `switch` statement’s execution immediately.*

> *NOTE*
> 
> *A `switch` case that contains only a comment is reported as a compile-time error. Comments aren’t statements and don’t cause a `switch` case to be ignored. Always use a `break` statement to ignore a `switch` case.*

*The following example switches on a `Character` value and determines whether it represents a number symbol in one of four languages. For brevity, multiple values are covered in a single `switch` case.*

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

*After the `switch` statement completes its execution, the example uses optional binding to determine whether a value was found. The `possibleIntegerValue` variable has an implicit initial value of `nil` by virtue of being an optional type, and so the optional binding will succeed only if `possibleIntegerValue` was set to an actual value by one of the `switch` statement’s first four cases.*

*Because it’s not practical to list every possible `Character` value in the example above, a `default` case handles any characters that aren’t matched. This `default` case doesn’t need to perform any action, and so it’s written with a single `break` statement as its body. As soon as the `default` case is matched, the `break` statement ends the `switch` statement’s execution, and code execution continues from the `if let` statement.*

### 

### *Fallthrough*

*In Swift, `switch` statements don’t fall through the bottom of each case and into the next one. That is, the entire `switch` statement completes its execution as soon as the first matching case is completed. By contrast, C requires you to insert an explicit `break` statement at the end of every `switch` case to prevent fallthrough. Avoiding default fallthrough means that Swift `switch` statements are much more concise and predictable than their counterparts in C, and thus they avoid executing multiple `switch` cases by mistake.*

*If you need C-style fallthrough behavior, you can opt in to this behavior on a case-by-case basis with the `fallthrough` keyword. The example below uses `fallthrough` to create a textual description of a number.*

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

*Unless the value of `integerToDescribe` is in the list of known prime numbers, it isn’t matched by the first `switch` case at all. Because there are no other specific cases, `integerToDescribe` is matched by the `default` case.*

*After the `switch` statement has finished executing, the number’s description is printed using the `print(_:separator:terminator:)` function. In this example, the number `5` is correctly identified as a prime number.*

> *NOTE*
> 
> *The `fallthrough` keyword doesn’t check the case conditions for the `switch` case that it causes execution to fall into. The `fallthrough` keyword simply causes code execution to move directly to the statements inside the next case (or `default` case) block, as in C’s standard `switch` statement behavior.*

 

### *Labeled Statements*

*In Swift, you can nest loops and conditional statements inside other loops and conditional statements to create complex control flow structures. However, loops and conditional statements can both use the `break` statement to end their execution prematurely. Therefore, it’s sometimes useful to be explicit about which loop or conditional statement you want a `break` statement to terminate. Similarly, if you have multiple nested loops, it can be useful to be explicit about which loop the `continue` statement should affect.*

*To achieve these aims, you can mark a loop statement or conditional statement with a statement label. With a conditional statement, you can use a statement label with the `break` statement to end the execution of the labeled statement. With a loop statement, you can use a statement label with the `break` or `continue` statement to end or continue the execution of the labeled statement.*

*A labeled statement is indicated by placing a label on the same line as the statement’s introducer keyword, followed by a colon. Here’s an example of this syntax for a `while` loop, although the principle is the same for all loops and `switch` statements:*

```swift
label name: while condition {
    statements
}
```

*The following example uses the `break` and `continue` statements with a labeled `while` loop for an adapted version of the Snakes and Ladders game that you saw earlier in this chapter. This time around, the game has an extra rule:*

- *To win, you must land exactly on square 25.*

*If a particular dice roll would take you beyond square 25, you must roll again until you roll the exact number needed to land on square 25.*

*The game board is the same as before.*

![](https://docs.swift.org/swift-book/_images/snakesAndLadders_2x.png)

*The values of `finalSquare`, `board`, `square`, and `diceRoll` are initialized in the same way as before:*

```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

*This version of the game uses a `while` loop and a `switch` statement to implement the game’s logic. The `while` loop has a statement label called `gameLoop` to indicate that it’s the main game loop for the Snakes and Ladders game.*

*The `while` loop’s condition is `while square != finalSquare`, to reflect that you must land exactly on square 25.*

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

- *If the dice roll will move the player onto the final square, the game is over. The `break gameLoop` statement transfers control to the first line of code outside of the `while` loop, which ends the game.*

- *If the dice roll will move the player beyond the final square, the move is invalid and the player needs to roll again. The `continue gameLoop` statement ends the current `while` loop iteration and begins the next iteration of the loop.*

- *In all other cases, the dice roll is a valid move. The player moves forward by `diceRoll` squares, and the game logic checks for any snakes and ladders. The loop then ends, and control returns to the `while` condition to decide whether another turn is required.*

> *NOTE*
> 
> *If the `break` statement above didn’t use the `gameLoop` label, it would break out of the `switch` statement, not the `while` statement. Using the `gameLoop` label makes it clear which control statement should be terminated.*
> 
> *It isn’t strictly necessary to use the `gameLoop` label when calling `continue gameLoop` to jump to the next iteration of the loop. there’s only one loop in the game, and therefore no ambiguity as to which loop the `continue` statement will affect. However, there’s no harm in using the `gameLoop` label with the `continue` statement. Doing so is consistent with the label’s use alongside the `break` statement and helps make the game’s logic clearer to read and understand.*


