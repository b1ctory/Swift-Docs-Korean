## *Checking Type : 타입 체크*

*Use the type check operator (`is`) to check whether an instance is of a certain subclass type. The type check operator returns `true` if the instance is of that subclass type and `false` if it’s not.*

타입 체크 연산자(`is`)를 사용하여 인스턴스가 특정 하위 클래스의 타입인지 확인합니다. 타입 검사 연산자는 인스턴스가 해당 하위 클래스 타입이면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.

*The example below defines two variables, `movieCount` and `songCount`, which count the number of `Movie` and `Song` instances in the `library` array:*

아래 예제에서는 `library` 배열에 있는 `Movie` 과 `Song` 인스턴스의 수를 계산하는 두 변수인 `movieCount` 와 `songCount`를 정의합니다:

```swift
var movieCount = 0
var songCount = 0

for item in library {
    if item is Movie {
        movieCount += 1
    } else if item is Song {
        songCount += 1
    }
}

print("Media library contains \(movieCount) movies and \(songCount) songs")
// Prints "Media library contains 2 movies and 3 songs"
```

*This example iterates through all items in the `library` array. On each pass, the `for`-`in` loop sets the `item` constant to the next `MediaItem` in the array.*

이 예는 `library` 배열의 모든 항목에서 반복됩니다. 각 패스에서 `for` -`in` 루프는 `item`상수를 배열의 다음 `MediaItem`으로 설정합니다.

*`item is Movie` returns `true` if the current `MediaItem` is a `Movie` instance and `false` if it’s not. Similarly, `item is Song` checks whether the item is a `Song` instance. At the end of the `for`-`in` loop, the values of `movieCount` and `songCount` contain a count of how many `MediaItem` instances were found of each type.*

`item is Movie`는 현재 `MediaItem`이 `Movie` 인스턴스이면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다. 마찬가지로 `item is Song`은 아이템이 `Song` 인스턴스인지 여부를 확인합니다. `for`-`in` 루프의 끝에 있는 `movieCount`와 `songCount`의 값에는 각 타입에서 발견된 `MediaItem` 인스턴스 수를 나타내는 카운트가 포함됩니다.
