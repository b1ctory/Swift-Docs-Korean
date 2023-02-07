## *Subscripts*

*Extensions can add new subscripts to an existing type. This example adds an integer subscript to Swift’s built-in `Int` type. This subscript `[n]` returns the decimal digit `n` places in from the right of the number:*

- *`123456789[0]` returns `9`*

- *`123456789[1]` returns `8`*

*…and so on:*

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

```swift
746381295[9]
// returns 0, as if you had requested:
0746381295[9]
```
