## *Tasks and Task Groups*

*A task is a unit of work that can be run asynchronously as part of your program. All asynchronous code runs as part of some task. The `async`-`let` syntax described in the previous section creates a child task for you. You can also create a task group and add child tasks to that group, which gives you more control over priority and cancellation, and lets you create a dynamic number of tasks.*

*Tasks are arranged in a hierarchy. Each task in a task group has the same parent task, and each task can have child tasks. Because of the explicit relationship between tasks and task groups, this approach is called structured concurrency. Although you take on some of the responsibility for correctness, the explicit parent-child relationships between tasks lets Swift handle some behaviors like propagating cancellation for you, and lets Swift detect some errors at compile time.*

```swift
await withTaskGroup(of: Data.self) { taskGroup in
    let photoNames = await listPhotos(inGallery: "Summer Vacation")
    for name in photoNames {
        taskGroup.addTask { await downloadPhoto(named: name) }
    }
}
```

*For more information about task groups, see [`TaskGroup`](https://developer.apple.com/documentation/swift/taskgroup).*

### *Unstructured Concurrency*

*In addition to the structured approaches to concurrency described in the previous sections, Swift also supports unstructured concurrency. Unlike tasks that are part of a task group, an unstructured task doesn’t have a parent task. You have complete flexibility to manage unstructured tasks in whatever way your program needs, but you’re also completely responsible for their correctness. To create an unstructured task that runs on the current actor, call the [`Task.init(priority:operation:)`](https://developer.apple.com/documentation/swift/task/3856790-init) initializer. To create an unstructured task that’s not part of the current actor, known more specifically as a detached task, call the [`Task.detached(priority:operation:)`](https://developer.apple.com/documentation/swift/task/3856786-detached) class method. Both of these operations return a task that you can interact with—for example, to wait for its result or to cancel it.*

```swift
let newPhoto = // ... some photo data ...
let handle = Task {
    return await add(newPhoto, toGalleryNamed: "Spring Adventures")
}
let result = await handle.value
```

*For more information about managing detached tasks, see [`Task`](https://developer.apple.com/documentation/swift/task).*

### *Task Cancellation*

*Swift concurrency uses a cooperative cancellation model. Each task checks whether it has been canceled at the appropriate points in its execution, and responds to cancellation in whatever way is appropriate. Depending on the work you’re doing, that usually means one of the following:*

- *Throwing an error like `CancellationError`*

- *Returning `nil` or an empty collection*

- *Returning the partially completed work*

*To check for cancellation, either call [`Task.checkCancellation()`](https://developer.apple.com/documentation/swift/task/3814826-checkcancellation), which throws `CancellationError` if the task has been canceled, or check the value of [`Task.isCancelled`](https://developer.apple.com/documentation/swift/task/3814832-iscancelled) and handle the cancellation in your own code. For example, a task that’s downloading photos from a gallery might need to delete partial downloads and close network connections.*

*To propagate cancellation manually, call [`Task.cancel()`](https://developer.apple.com/documentation/swift/task/3851218-cancel).*


