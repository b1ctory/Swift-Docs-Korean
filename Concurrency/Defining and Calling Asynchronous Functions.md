## *Defining and Calling Asynchronous Functions : 비동기 함수 정의와 호출*

*An asynchronous function or asynchronous method is a special kind of function or method that can be suspended while it’s partway through execution. This is in contrast to ordinary, synchronous functions and methods, which either run to completion, throw an error, or never return. An asynchronous function or method still does one of those three things, but it can also pause in the middle when it’s waiting for something. Inside the body of an asynchronous function or method, you mark each of these places where execution can be suspended.*

비동기 함수 또는 비동기 메서드는 실행 도중 일시 중단될 수 있는 특수한 종류의 함수 또는 메서드입니다. 이는 완료될 때까지 실행되거나 오류를 발생시키거나 다시 돌아오지 않는 일반적인 동기화 기능 및 방법과는 대조적입니다. 비동기 함수 또는 메서드는 여전히 이 세 가지 중 하나를 수행하지만, 무언가를 기다리고 있을 때 중간에 일시 중지할 수도 있습니다. 비동기 함수 또는 메서드의 본문 안에서 실행이 일시 중단될 수 있는 각 위치를 표시합니다.

*To indicate that a function or method is asynchronous, you write the `async` keyword in its declaration after its parameters, similar to how you use `throws` to mark a throwing function. If the function or method returns a value, you write `async` before the return arrow (`->`). For example, here’s how you might fetch the names of photos in a gallery:*

어떤 함수나 메서드가 비동기임을 나타내려면 해당 함수의 매개 변수 뒤에 `async` 키워드를 쓰십시오. `throws` 를 사용하여 함수를 표시하는 방법과 유사합니다. 함수나 메서드가 값을 반환하는 경우 반환 화살표(`->`) 앞에 `async`라고 적습니다. 예를 들어, 갤러리에서 사진 이름을 가져오는 방법은 다음과 같습니다.

```swift
func listPhotos(inGallery name: String) async -> [String] {
    let result = // ... some asynchronous networking code ...
    return result
}
```

*For a function or method that’s both asynchronous and throwing, you write `async` before `throws`.*

비동기식이면서 던지기식인 함수나 메서드는 `throws` 앞에 `async`라고 적습니다.

*When calling an asynchronous method, execution suspends until that method returns. You write `await` in front of the call to mark the possible suspension point. This is like writing `try` when calling a throwing function, to mark the possible change to the program’s flow if there’s an error. Inside an asynchronous method, the flow of execution is suspended only when you call another asynchronous method—suspension is never implicit or preemptive—which means every possible suspension point is marked with `await`.*

비동기 메서드를 호출할 때는 해당 메서드가 반환될 때까지 실행이 일시 중단됩니다. 호출지점 앞에 `await`라고 적으면 정지 지점을 표시할 수 있습니다. 이는 던지기 함수를 호출할 때 `try`를 쓰는 것과 같습니다. 오류가 있을 경우 프로그램 흐름에 변경 가능성을 표시합니다. 비동기식 메서드 내에서 실행 흐름은 다른 비동기식 메서드(서스펜션은 절대 암시적이거나 선제적이지 않음)를 호출할 때만 중단됩니다. 즉, 가능한 모든 서스펜션 포인트가 `await`로 표시됩니다.

*For example, the code below fetches the names of all the pictures in a gallery and then shows the first picture:*

예를 들어, 아래 코드는 갤러리에 있는 모든 사진의 이름을 가져온 다음 첫 번째 사진을 표시합니다:

```swift
let photoNames = await listPhotos(inGallery: "Summer Vacation")
let sortedNames = photoNames.sorted()
let name = sortedNames[0]
let photo = await downloadPhoto(named: name)
show(photo)
```

*Because the `listPhotos(inGallery:)` and `downloadPhoto(named:)` functions both need to make network requests, they could take a relatively long time to complete. Making them both asynchronous by writing `async` before the return arrow lets the rest of the app’s code keep running while this code waits for the picture to be ready.*

 `listPhotos(inGallery:)`와 `downloadPhoto(named:)` 함수는 모두 네트워크 요청을 수행해야 하므로 완료하는 데 비교적 오랜 시간이 걸릴 수 있습니다. 리턴 화살표 앞에 `async`를 써서 둘 다 비동기화하면 이 코드가 사진이 준비될 때까지 기다리는 동안 앱의 나머지 코드가 계속 실행됩니다.

*To understand the concurrent nature of the example above, here’s one possible order of execution:*

위 예제의 동시 특성을 이해하기 위해 가능한 실행 순서는 다음과 같습니다:

1. *The code starts running from the first line and runs up to the first `await`. It calls the `listPhotos(inGallery:)` function and suspends execution while it waits for that function to return.*
   
   코드는 첫 번째 줄부터 실행되기 시작하여 첫 번째 `await`까지 실행됩니다. 그것은 `listPhotos(inGallery:)` 함수를 실행하고 해당 함수가 다시 돌아오기를 기다리는 동안 실행을 일시 중단합니다.

2. *While this code’s execution is suspended, some other concurrent code in the same program runs. For example, maybe a long-running background task continues updating a list of new photo galleries. That code also runs until the next suspension point, marked by `await`, or until it completes.*
   
   이 코드의 실행이 일시 중단되는 동안 동일한 프로그램의 다른 일부 코드가 동시에 실행됩니다. 예를 들어, 장기간 실행되는 백그라운드 태스크가 새 사진 갤러리 목록을 계속 업데이트할 수 있습니다. 이 코드는 또한 `await`로 표시된 다음 중단 지점까지 또는 완료될 때까지 실행됩니다.

3. *After `listPhotos(inGallery:)` returns, this code continues execution starting at that point. It assigns the value that was returned to `photoNames`.*
   
    `listPhotos(inGallery:)` 반환된 후, 이 코드는 해당 지점부터 실행을 계속합니다. 반환된 값을 `photoNames`로 할당합니다.

4. *The lines that define `sortedNames` and `name` are regular, synchronous code. Because nothing is marked `await` on these lines, there aren’t any possible suspension points.*
   
    `sortedNames` 과 `name`을 정의하는 라인은 일반적인 동기 코드입니다. 이들 노선에는 `await`라고 표시된 것이 없기 때문에 정지 지점이 없습니다.

5. *The next `await` marks the call to the `downloadPhoto(named:)` function. This code pauses execution again until that function returns, giving other concurrent code an opportunity to run.*
   
   다음 `await`는  `downloadPhoto(named:)` 함수에 대한 호출을 표시합니다. 이 코드는 해당 함수가 반환될 때까지 실행을 다시 일시 중지하여 다른 동시 코드를 실행할 수 있는 기회를 제공합니다.

6. *After `downloadPhoto(named:)` returns, its return value is assigned to `photo` and then passed as an argument when calling `show(_:)`.*
   
   `downloadPhoto(named:)`가 반환된 후 반환 값이 `photo`에 할당된 다음 `show(_:)`를 호출할 때 인수로 전달됩니다.

*The possible suspension points in your code marked with `await` indicate that the current piece of code might pause execution while waiting for the asynchronous function or method to return. This is also called yielding the thread because, behind the scenes, Swift suspends the execution of your code on the current thread and runs some other code on that thread instead. Because code with `await` needs to be able to suspend execution, only certain places in your program can call asynchronous functions or methods:*

`await`로 표시된 코드에서 발생할 수 있는 중단점은 비동기 함수 또는 메서드가 반환될 때까지 기다리는 동안 현재 코드 조각이 실행을 일시 중지할 수 있음을 나타냅니다. 이를 스레드 생성이라고도 하는데, 배경에서는 Swift가 현재 스레드에서 코드 실행을 일시 중단하고 대신 해당 스레드에서 다른 코드를 실행하기 때문입니다. `await`가 있는 코드는 실행을 중단할 수 있어야 하므로 프로그램의 특정 위치에서만 비동기 함수나 메서드를 호출할 수 있습니다:

- *Code in the body of an asynchronous function, method, or property.*
  
  비동기 함수, 메서드 또는 프로퍼티의 본문에 있는 코드입니다.

- *Code in the static `main()` method of a structure, class, or enumeration that’s marked with `@main`.*
  
  `@main`으로 표시된 구조체, 클래스 또는 열거형의 정적 `main()` 메서드의 코드입니다.

- *Code in an unstructured child task, as shown in [Unstructured Concurrency](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html#ID643) below.*
  
  아래 [링크]에 나와 있는 것처럼 구조화되지 않은 자식 작업의 코드입니다.

*Code in between possible suspension points runs sequentially, without the possibility of interruption from other concurrent code. For example, the code below moves a picture from one gallery to another.*

가능한 지연 지점 사이의 코드는 다른 동시 코드의 중단 없이 순차적으로 실행됩니다. 예를 들어, 아래 코드는 한 갤러리에서 다른 갤러리로 사진을 이동합니다.

```swift
let firstPhoto = await listPhotos(inGallery: "Summer Vacation")[0]
add(firstPhoto toGallery: "Road Trip")
// At this point, firstPhoto is temporarily in both galleries.
remove(firstPhoto fromGallery: "Summer Vacation")
```

*There’s no way for other code to run in between the call to `add(_:toGallery:)` and `remove(_:fromGallery:)`. During that time, the first photo appears in both galleries, temporarily breaking one of the app’s invariants. To make it even clearer that this chunk of code must not have `await` added to it in the future, you can refactor that code into a synchronous function:*

`add(_:toGallery:)`와 `remove(_:fromGallery:)` 호출 사이에 다른 코드가 실행될 수 있는 방법이 없습니다. 이 기간 동안 첫 번째 사진이 두 갤러리에 모두 나타나 앱의 불변량 중 하나를 일시적으로 깨뜨립니다. 이 코드 덩어리에 앞으로 `await`가 추가되지 않아야 한다는 것을 더욱 명확히 하기 위해 해당 코드를 동기 함수로 리팩터링할 수 있습니다.

```swift
func move(_ photoName: String, from source: String, to destination: String) {
    add(photoName, to: destination)
    remove(photoName, from: source)
}
// ...
let firstPhoto = await listPhotos(inGallery: "Summer Vacation")[0]
move(firstPhoto, from: "Summer Vacation", to: "Road Trip")
```

*In the example above, because the `move(_:from:to:)` function is synchronous, you guarantee that it can never contain possible suspension points. In the future, if you try to add concurrent code to this function, introducing a possible suspension point, you’ll get compile-time error instead of introducing a bug.*

위의 예에서 `move(_:from:to:)` 함수는 동기식이므로 가능한 지연 지점을 포함할 수 없음을 보장합니다. 앞으로 이 함수에 동시 코드를 추가하여 일시 중단 가능성이 있는 지점을 도입하려고 하면 버그를 도입하는 대신 컴파일 타임 오류가 발생합니다.

> *NOTE*
> 
> *The [`Task.sleep(until:tolerance:clock:)`](https://developer.apple.com/documentation/swift/task/sleep(until:tolerance:clock:)) method is useful when writing simple code to learn how concurrency works. This method does nothing, but waits at least the given number of nanoseconds before it returns. Here’s a version of the `listPhotos(inGallery:)` function that uses `sleep(until:tolerance:clock:)` to simulate waiting for a network operation:*
> 
>  [`Task.sleep(until:tolerance:clock:)`](https://developer.apple.com/documentation/swift/task/sleep(until:tolerance:clock:)) 메서드는 단순 코드를 작성하여 동시성이 작동하는 방식을 배울 때 유용합니다. 이 메서드는 아무 작업도 수행하지 않지만 지정된 나노초 시간 동안 기다렸다가 다시 시작합니다. 다음은 `sleep(until:tolerance:clock:)`을 사용하여 네트워크 작업 대기를 시뮬레이션하는`listPhotos(inGallery:)` 함수 버전입니다.
> 
> ```swift
> func listPhotos(inGallery name: String) async throws -> [String] {
>     try await Task.sleep(until: .now + .seconds(2), clock: .continuous)
>     return ["IMG001", "IMG99", "IMG0404"]
> }
> ```
