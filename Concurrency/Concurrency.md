# *Concurrency : 동시성*

*Swift has built-in support for writing asynchronous and parallel code in a structured way. Asynchronous code can be suspended and resumed later, although only one piece of the program executes at a time. Suspending and resuming code in your program lets it continue to make progress on short-term operations like updating its UI while continuing to work on long-running operations like fetching data over the network or parsing files. Parallel code means multiple pieces of code run simultaneously—for example, a computer with a four-core processor can run four pieces of code at the same time, with each core carrying out one of the tasks. A program that uses parallel and asynchronous code carries out multiple operations at a time; it suspends operations that are waiting for an external system, and makes it easier to write this code in a memory-safe way.*

Swift는 구조화된 방식으로 비동기 및 병렬 코드를 작성할 수 있도록 내장된 지원을 가지고 있습니다. 비동기 코드는 한 번에 한 부분만 실행되지만 일시 중단했다가 나중에 다시 시작할 수 있습니다. 프로그램에서 코드를 일시 중단했다가 다시 시작하면 네트워크를 통해 데이터를 가져오거나 파일을 구문 분석하는 등 장기 실행 작업을 계속하면서 UI 업데이트와 같은 단기 작업을 계속 진행할 수 있습니다. 병렬 코드는 여러 개의 코드 조각이 동시에 실행되는 것을 의미합니다. 예를 들어, 4코어 프로세서가 있는 컴퓨터는 다음을 수행할 수 있습니다 코드 4개를 동시에 실행하고 각 코어가 작업 중 하나를 수행합니다. 병렬 및 비동기 코드를 사용하는 프로그램은 한 번에 여러 작업을 수행합니다. 이 프로그램은 외부 시스템을 기다리는 작업을 일시 중단하고 메모리에 안전한 방식으로 이 코드를 쉽게 작성할 수 있도록 합니다.

*The additional scheduling flexibility from parallel or asynchronous code also comes with a cost of increased complexity. Swift lets you express your intent in a way that enables some compile-time checking—for example, you can use actors to safely access mutable state. However, adding concurrency to slow or buggy code isn’t a guarantee that it will become fast or correct. In fact, adding concurrency might even make your code harder to debug. However, using Swift’s language-level support for concurrency in code that needs to be concurrent means Swift can help you catch problems at compile time.*

병렬 또는 비동기 코드를 통한 유연한 스케줄링을 위해 복잡성이 증가합니다. Swift를 사용하면 예를 들어 actor를 사용하여 변경 가능한 상태에 안전하게 액세스할 수 있는 등 컴파일타임 검사를 사용할 수 있는 방식으로 의도를 표현할 수 있습니다. 그러나 속도가 느리거나 버그가 많은 코드에 동시성을 추가한다고 해서 그것이 빠르거나 정확해진다는 보장은 없습니다. 실제로 동시성을 추가하면 코드를 디버깅하기가 더 어려워질 수도 있습니다. 그러나 Swift의 언어 수준 지원을 사용하여 동시에 코드를 동시에 사용하면 Swift가 컴파일 시 문제를 파악하는 데 도움이 될 수 있습니다.

*The rest of this chapter uses the term concurrency to refer to this common combination of asynchronous and parallel code.*

이 장의 나머지 부분에서는 비동기 및 병렬 코드의 일반적인 조합을 참조하기 위해 동시성이라는 용어를 사용합니다.

> *NOTE*
> 
> *If you’ve written concurrent code before, you might be used to working with threads. The concurrency model in Swift is built on top of threads, but you don’t interact with them directly. An asynchronous function in Swift can give up the thread that it’s running on, which lets another asynchronous function run on that thread while the first function is blocked. When an asynchronous function resumes, Swift doesn’t make any guarantee about which thread that function will run on.*
> 
> 동시성 코드를 작성한 적이 있다면 스레드 작업에 익숙해질 수 있습니다. Swift의 동시성 모델은 스레드 위에 구축되지만 사용자는 스레드와 직접 상호 작용하지 않습니다. Swift의 비동기 함수는 실행 중인 스레드를 포기할 수 있으므로 첫 번째 함수가 차단되는 동안 해당 스레드에서 다른 비동기 함수를 실행할 수 있습니다. 비동기 함수가 다시 시작될 때 Swift는 해당 함수가 실행될 스레드에 대해 어떠한 보증도 하지 않습니다.

*Although it’s possible to write concurrent code without using Swift’s language support, that code tends to be harder to read. For example, the following code downloads a list of photo names, downloads the first photo in that list, and shows that photo to the user:*

Swift의 언어 지원을 사용하지 않고 동시 코드를 작성할 수 있지만, 코드를 읽기가 더 어려운 경향이 있습니다. 예를 들어, 다음 코드는 사진 이름 목록을 다운로드하고 해당 목록의 첫 번째 사진을 다운로드한 다음 사용자에게 해당 사진을 표시합니다:

```swift
listPhotos(inGallery: "Summer Vacation") { photoNames in
    let sortedNames = photoNames.sorted()
    let name = sortedNames[0]
    downloadPhoto(named: name) { photo in
        show(photo)
    }
}
```

*Even in this simple case, because the code has to be written as a series of completion handlers, you end up writing nested closures. In this style, more complex code with deep nesting can quickly become unwieldy.*

이 간단한 경우에도 코드를 일련의 완료 핸들러로 작성해야 하므로 중첩 클로저를 작성하게 됩니다. 이 스타일에서는 깊은 중첩이 있는 더 복잡한 코드가 빠르게 다루기 어려워질 수 있습니다.
