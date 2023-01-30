## *Asynchronous Sequences*

*The `listPhotos(inGallery:)` function in the previous section asynchronously returns the whole array at once, after all of the array’s elements are ready. Another approach is to wait for one element of the collection at a time using an asynchronous sequence. Here’s what iterating over an asynchronous sequence looks like:*

```swift
import Foundation

let handle = FileHandle.standardInput
for try await line in handle.bytes.lines {
    print(line)
}
```

*Instead of using an ordinary `for`-`in` loop, the example above writes `for` with `await` after it. Like when you call an asynchronous function or method, writing `await` indicates a possible suspension point. A `for`-`await`-`in` loop potentially suspends execution at the beginning of each iteration, when it’s waiting for the next element to be available.*

*In the same way that you can use your own types in a `for`-`in` loop by adding conformance to the [`Sequence`](https://developer.apple.com/documentation/swift/sequence) protocol, you can use your own types in a `for`-`await`-`in` loop by adding conformance to the [`AsyncSequence`](https://developer.apple.com/documentation/swift/asyncsequence) protocol.*
