## *Tasks and Task Groups: 작업 및 작업 그룹*

*A task is a unit of work that can be run asynchronously as part of your program. All asynchronous code runs as part of some task. The `async`-`let` syntax described in the previous section creates a child task for you. You can also create a task group and add child tasks to that group, which gives you more control over priority and cancellation, and lets you create a dynamic number of tasks.*

작업은 프로그램의 일부로 비동기적으로 실행될 수 있는 작업 단위입니다. 모든 비동기 코드는 일부 작업의 일부로 실행됩니다. 이전 섹션에서 설명한  `async`-`let`구문을 사용하면 하위 작업이 생성됩니다. 또한 태스크 그룹을 생성하고 해당 그룹에 하위 태스크를 추가하여 우선 순위 및 취소를 보다 효과적으로 제어하고 동적인 수의 작업을 생성할 수 있습니다.

*Tasks are arranged in a hierarchy. Each task in a task group has the same parent task, and each task can have child tasks. Because of the explicit relationship between tasks and task groups, this approach is called structured concurrency. Although you take on some of the responsibility for correctness, the explicit parent-child relationships between tasks lets Swift handle some behaviors like propagating cancellation for you, and lets Swift detect some errors at compile time.*

작업은 계층 구조로 정렬됩니다. 태스크 그룹의 각 태스크에는 동일한 상위 태스크가 있으며 각 태스크에는 하위 태스크가 있을 수 있습니다. 작업과 작업그룹 간의 명시적인 관계 때문에 이 접근 방식을 구조화된 동시성이라고 합니다. 작업 간의 명시적인 상위-하위 관계를 통해 Swift는 사용자를 위해 취소 전파와 같은 일부 동작을 처리하고 컴파일 시 일부 오류를 탐지할 수 있습니다.

```swift
await withTaskGroup(of: Data.self) { taskGroup in
    let photoNames = await listPhotos(inGallery: "Summer Vacation")
    for name in photoNames {
        taskGroup.addTask { await downloadPhoto(named: name) }
    }
}
```

*For more information about task groups, see [`TaskGroup`](https://developer.apple.com/documentation/swift/taskgroup).*

작업 그룹에 대한 자세한 내용은 [TaskGroup]을 참조하세요.

### *Unstructured Concurrency : 구조화되지 않은 동시성*

*In addition to the structured approaches to concurrency described in the previous sections, Swift also supports unstructured concurrency. Unlike tasks that are part of a task group, an unstructured task doesn’t have a parent task. You have complete flexibility to manage unstructured tasks in whatever way your program needs, but you’re also completely responsible for their correctness. To create an unstructured task that runs on the current actor, call the [`Task.init(priority:operation:)`](https://developer.apple.com/documentation/swift/task/3856790-init) initializer. To create an unstructured task that’s not part of the current actor, known more specifically as a detached task, call the [`Task.detached(priority:operation:)`](https://developer.apple.com/documentation/swift/task/3856786-detached) class method. Both of these operations return a task that you can interact with—for example, to wait for its result or to cancel it.*

Swift는 이전 섹션에서 설명한 구조화된 동시성 접근 방식 외에도 구조화되지 않은 동시성도 지원합니다. 작업 그룹의 일부인 작업과 달리 구조화되지 않은 작업에는 상위 작업이 없습니다. 프로그램에 필요한 모든 방식으로 비정형 작업을 관리할 수 있는 완벽한 유연성을 갖추고 있지만, 정확성에 대해서도 전적으로 책임을 져야 합니다. 현재 액터에서 실행되는 비정형 작업을 생성하려면 `Task.init(priority:operation:)`를 호출하십시오. 현재 액터의 일부가 아닌 비정형 작업, 특히 분리된 작업을 만들려면 `Task.detached(priority:operation:)` 클래스 메서드를 호출하십시오. 이러한 작업은 결과를 기다리거나 취소하는 등 상호 작용할 수 있는 태스크를 반환합니다.

```swift
let newPhoto = // ... some photo data ...
let handle = Task {
    return await add(newPhoto, toGalleryNamed: "Spring Adventures")
}
let result = await handle.value
```

*For more information about managing detached tasks, see [`Task`](https://developer.apple.com/documentation/swift/task).*

분리된 작업 관리에 대한 자세한 내용은 [링크]를 참조하세요.

### *Task Cancellation: 작업 취소*

*Swift concurrency uses a cooperative cancellation model. Each task checks whether it has been canceled at the appropriate points in its execution, and responds to cancellation in whatever way is appropriate. Depending on the work you’re doing, that usually means one of the following:*

Swift 동시성은 공동취소 모델을 사용합니다. 각 태스크는 실행 시 적절한 시점에 취소되었는지 확인하고 적절한 방법으로 취소에 응답합니다. 작업에 따라 일반적으로 다음 중 하나를 의미합니다:

- *Throwing an error like `CancellationError`*
  
  `CancellationError`와 같은 오류를 던집니다.

- *Returning `nil` or an empty collection*
  
  `nil` 또는 빈 컬렉션을 반환합니다.

- *Returning the partially completed work*
  
  부분적으로 완료된 작업을 반환합니다.

*To check for cancellation, either call [`Task.checkCancellation()`](https://developer.apple.com/documentation/swift/task/3814826-checkcancellation), which throws `CancellationError` if the task has been canceled, or check the value of [`Task.isCancelled`](https://developer.apple.com/documentation/swift/task/3814832-iscancelled) and handle the cancellation in your own code. For example, a task that’s downloading photos from a gallery might need to delete partial downloads and close network connections.*

취소 여부를 확인하려면 작업이 취소된 경우 `Task.checkCancelation()` 을 호출하여 `CancellationError`를 발생시키거나 `Task.isCancelled`의 값을 확인하고 사용자 코드에 있는 취소를 처리합니다.  예를 들어 갤러리에서 사진을 다운로드하는 작업은 부분 다운로드를 삭제하고 네트워크 연결을 닫아야 할 수 있습니다.

*To propagate cancellation manually, call [`Task.cancel()`](https://developer.apple.com/documentation/swift/task/3851218-cancel).*

수동으로 취소를 전파하시려면 Task.cancel() 을 호출하세요.
