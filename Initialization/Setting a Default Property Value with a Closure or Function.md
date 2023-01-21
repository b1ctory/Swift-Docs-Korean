## *Setting a Default Property Value with a Closure or Function : 클로저 혹은 함수를 이용해 기본 프로퍼티 값 셋팅*

*If a stored property’s default value requires some customization or setup, you can use a closure or global function to provide a customized default value for that property. Whenever a new instance of the type that the property belongs to is initialized, the closure or function is called, and its return value is assigned as the property’s default value.*

저장 프로퍼티의 기본값에 사용자 지정 또는 설정이 필요한 경우 클로저 또는 전역 함수를 사용하여 해당 프로퍼티에 사용자 지정된 기본값을 제공할 수 있습니다. 프로퍼티가 속한 타입의 새 인스턴스가 초기화될 때마다 클로저 또는 함수가 호출되고 해당 반환 값이 프로퍼티의 기본값으로 할당됩니다.

*These kinds of closures or functions typically create a temporary value of the same type as the property, tailor that value to represent the desired initial state, and then return that temporary value to be used as the property’s default value.*

이러한 종류의 클로저 또는 함수는 일반적으로 프로퍼티와 동일한 타입의 임시 값을 생성하고 해당 값을 원하는 초기 상태를 나타내도록 조정한 다음 프로퍼티의 기본값으로 사용할 임시 값을 반환합니다.

*Here’s a skeleton outline of how a closure can be used to provide a default property value:*

다음은 클로저를 사용하여 기본 프로퍼티 값을 제공하는 방법에 대한 개요입니다.

```swift
class SomeClass {
    let someProperty: SomeType = {
        // create a default value for someProperty inside this closure
        // someValue must be of the same type as SomeType
        return someValue
    }()
}
```

*Note that the closure’s end curly brace is followed by an empty pair of parentheses. This tells Swift to execute the closure immediately. If you omit these parentheses, you are trying to assign the closure itself to the property, and not the return value of the closure.*

클로저 끝의 곱슬곱슬한 괄호 뒤에 빈 괄호쌍이 표시됩니다. 이것은 Swift에게 즉시 클로저를 실행하라고 말합니다. 이러한 괄호를 생략하면 클로저 자체를 클로저의 반환 값이 아닌 프로퍼티에 할당하려고 합니다.

> *NOTE*
> 
> *If you use a closure to initialize a property, remember that the rest of the instance hasn’t yet been initialized at the point that the closure is executed. This means that you can’t access any other property values from within your closure, even if those properties have default values. You also can’t use the implicit `self` property, or call any of the instance’s methods.*
> 
> 클로저를 사용하여 프로퍼티를 초기화하는 경우, 나머지 인스턴스는 종료가 실행되는 시점에 아직 초기화되지 않았습니다. 즉, 클로저 내에서 다른 프로퍼티 값에 기본값이 있더라도 해당 프로퍼티 값에 액세스할 수 없습니다. 또한 암시적 `self` 속성을 사용하거나 인스턴스의 메서드를 호출할 수 없습니다.

*The example below defines a structure called `Chessboard`, which models a board for the game of chess. Chess is played on an 8 x 8 board, with alternating black and white squares.*

아래 예시는 체스 게임을 위한 보드를 모델링하는 `Chessboard`라는 구조체를 정의합니다. 체스는 8 x 8 판 위에서 흑백 사각형을 번갈아 가며 합니다.

*![../_images/chessBoard_2x.png](https://docs.swift.org/swift-book/_images/chessBoard_2x.png)*

*To represent this game board, the `Chessboard` structure has a single property called `boardColors`, which is an array of 64 `Bool` values. A value of `true` in the array represents a black square and a value of `false` represents a white square. The first item in the array represents the top left square on the board and the last item in the array represents the bottom right square on the board.*

이 게임 보드를 나타내기 위해 `Chessboard` 구조체는 64개의 Bool 값의 배열인 `boardColor`라는 단일 프로퍼티를 가집니다. 배열에서 `true` 값은 검은색 사각형을 나타내고 `false` 값은 흰색 사각형을 나타냅니다. 배열의 첫 번째 항목은 보드의 왼쪽 상단 사각형을 나타내고 배열의 마지막 항목은 보드의 오른쪽 하단 사각형을 나타냅니다.

*The `boardColors` array is initialized with a closure to set up its color values:*

`boardColors` 배열은 색상 값을 설정하기 위해 클로저로 초기화됩니다:

```swift
struct Chessboard {
    let boardColors: [Bool] = {
        var temporaryBoard: [Bool] = []
        var isBlack = false
        for i in 1...8 {
            for j in 1...8 {
                temporaryBoard.append(isBlack)
                isBlack = !isBlack
            }
            isBlack = !isBlack
        }
        return temporaryBoard
    }()
    func squareIsBlackAt(row: Int, column: Int) -> Bool {
        return boardColors[(row * 8) + column]
    }
}
```

*Whenever a new `Chessboard` instance is created, the closure is executed, and the default value of `boardColors` is calculated and returned. The closure in the example above calculates and sets the appropriate color for each square on the board in a temporary array called `temporaryBoard`, and returns this temporary array as the closure’s return value once its setup is complete. The returned array value is stored in `boardColors` and can be queried with the `squareIsBlackAt(row:column:)` utility function:*

새 `Chesboard` 인스턴스가 생성될 때마다 클로저가 실행되고 `boardColors`의 기본값이 계산되어 반환됩니다. 위의 예제에서 클로저는 `temporaryBoard`라고 하는 임시 배열에서 보드의 각 사각형에 대한 적절한 색상을 계산하고 설정하고 설정이 완료되면 이 임시 배열을 클로저의 반환 값으로 반환합니다. 반환된 배열 값은 `boardColors`에 저장되며 `squareIsBlackAt(row:column:)` 유틸리티 함수로 쿼리할 수 있습니다:

```swift
let board = Chessboard()
print(board.squareIsBlackAt(row: 0, column: 1))
// Prints "true"
print(board.squareIsBlackAt(row: 7, column: 7))
// Prints "false"
```
