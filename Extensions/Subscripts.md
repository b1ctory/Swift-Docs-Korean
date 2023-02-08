## *Subscripts : 서브스크립트*

*Extensions can add new subscripts to an existing type. This example adds an integer subscript to Swift’s built-in `Int` type. This subscript `[n]` returns the decimal digit `n` places in from the right of the number:*

확장은 기존 타입에 새 서브스크립트를 추가할 수 있습니다. 이 예에서는 Swift의 기본 제공 `Int` 타입에 정수 서브스크립트를 추가합니다. 이 첨자 `[n]`은 숫자 오른쪽에서 소수 자릿수 `n`을 반환합니다:

- *`123456789[0]` returns `9`*
  
  `123456789[0]` 은 `9`를 리턴합니다.

- *`123456789[1]` returns `8`*
  
  `123456789[1]`은 `8`을 리턴합니다.

*…and so on:*

등등

```swift
extension Int {
    subscript(digitIndex: Int) -> Int {
        var decimalBase = 1
        for _ in 0..<digitIndex {
            decimalBase *= 10
        }
        return (self / decimalBase) % 10
    }
}
746381295[0]
// returns 5
746381295[1]
// returns 9
746381295[2]
// returns 2
746381295[8]
// returns 7
```

*If the `Int` value doesn’t have enough digits for the requested index, the subscript implementation returns `0`, as if the number had been padded with zeros to the left:*

`Int` 값에 요청한 인덱스에 대한 숫자가 충분하지 않은 경우, 숫자가 왼쪽에 0으로 패딩된 것처럼 서브스크립트 구현은 `0`을 반환합니다.

```swift
746381295[9]
// returns 0, as if you had requested:
0746381295[9]
```
