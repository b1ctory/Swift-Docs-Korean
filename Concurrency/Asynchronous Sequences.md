## *Asynchronous Sequences : 비동기 시퀀스*

*The `listPhotos(inGallery:)` function in the previous section asynchronously returns the whole array at once, after all of the array’s elements are ready. Another approach is to wait for one element of the collection at a time using an asynchronous sequence. Here’s what iterating over an asynchronous sequence looks like:*

 `listPhotos(inGallery:)` 함수는 배열의 모든 요소가 준비된 후에 전체 배열을 한 번에 비동기식으로 반환합니다. 또 다른 접근 방식은 비동기 시퀀스를 사용하여 한 번에 하나의 컬렉션 요소를 대기하는 것입니다. 다음은 비동기 시퀀스를 반복하는 방법입니다:

```swift
import Foundation

let handle = FileHandle.standardInput
for try await line in handle.bytes.lines {
    print(line)
}
```

*Instead of using an ordinary `for`-`in` loop, the example above writes `for` with `await` after it. Like when you call an asynchronous function or method, writing `await` indicates a possible suspension point. A `for`-`await`-`in` loop potentially suspends execution at the beginning of each iteration, when it’s waiting for the next element to be available.*

위의 예에서는 일반적인 `for`-`in` 루프를 사용하는 대신 `for` 뒤에 `await`을 씁니다. 비동기 함수나 메서드를 호출할 때와 마찬가지로 `await`이라고 쓰면 가능한 중단점을 나타냅니다. `for`-`await`-`in` 루프는 잠재적으로 각 반복의 시작 부분에서 실행을 중단합니다. 이때 다음 요소를 사용할 수 있게 되기를 기다리고 있습니다.

*In the same way that you can use your own types in a `for`-`in` loop by adding conformance to the [`Sequence`](https://developer.apple.com/documentation/swift/sequence) protocol, you can use your own types in a `for`-`await`-`in` loop by adding conformance to the [`AsyncSequence`](https://developer.apple.com/documentation/swift/asyncsequence) protocol.*

[Sequence](https://developer.apple.com/documentation/swift/sequence) 프로토콜에 적합성을 추가하여 `for`-`in` 루프에서 자신의 타입을 사용할 수 있는 것과 마찬가지로, [AsyncSequence](https://developer.apple.com/documentation/swift/asyncsequence) 프로토콜에 적합성을 추가하여  `for`-`await`-`in` 루프에서 자신의 타입을 사용할 수 있습니다.
