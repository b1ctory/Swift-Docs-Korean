## *Defining and Calling Asynchronous Functions*

*An asynchronous function or asynchronous method is a special kind of function or method that can be suspended while it’s partway through execution. This is in contrast to ordinary, synchronous functions and methods, which either run to completion, throw an error, or never return. An asynchronous function or method still does one of those three things, but it can also pause in the middle when it’s waiting for something. Inside the body of an asynchronous function or method, you mark each of these places where execution can be suspended.*

*To indicate that a function or method is asynchronous, you write the `async` keyword in its declaration after its parameters, similar to how you use `throws` to mark a throwing function. If the function or method returns a value, you write `async` before the return arrow (`->`). For example, here’s how you might fetch the names of photos in a gallery:*

```swift
func listPhotos(inGallery name: String) async -> [String] {
    let result = // ... some asynchronous networking code ...
    return result
}
```

*For a function or method that’s both asynchronous and throwing, you write `async` before `throws`.*

*When calling an asynchronous method, execution suspends until that method returns. You write `await` in front of the call to mark the possible suspension point. This is like writing `try` when calling a throwing function, to mark the possible change to the program’s flow if there’s an error. Inside an asynchronous method, the flow of execution is suspended only when you call another asynchronous method—suspension is never implicit or preemptive—which means every possible suspension point is marked with `await`.*

*For example, the code below fetches the names of all the pictures in a gallery and then shows the first picture:*

```swift
let photoNames = await listPhotos(inGallery: "Summer Vacation")
let sortedNames = photoNames.sorted()
let name = sortedNames[0]
let photo = await downloadPhoto(named: name)
show(photo)
```

*Because the `listPhotos(inGallery:)` and `downloadPhoto(named:)` functions both need to make network requests, they could take a relatively long time to complete. Making them both asynchronous by writing `async` before the return arrow lets the rest of the app’s code keep running while this code waits for the picture to be ready.*

*To understand the concurrent nature of the example above, here’s one possible order of execution:*

1. *The code starts running from the first line and runs up to the first `await`. It calls the `listPhotos(inGallery:)` function and suspends execution while it waits for that function to return.*

2. *While this code’s execution is suspended, some other concurrent code in the same program runs. For example, maybe a long-running background task continues updating a list of new photo galleries. That code also runs until the next suspension point, marked by `await`, or until it completes.*

3. *After `listPhotos(inGallery:)` returns, this code continues execution starting at that point. It assigns the value that was returned to `photoNames`.*

4. *The lines that define `sortedNames` and `name` are regular, synchronous code. Because nothing is marked `await` on these lines, there aren’t any possible suspension points.*

5. *The next `await` marks the call to the `downloadPhoto(named:)` function. This code pauses execution again until that function returns, giving other concurrent code an opportunity to run.*

6. *After `downloadPhoto(named:)` returns, its return value is assigned to `photo` and then passed as an argument when calling `show(_:)`.*

*The possible suspension points in your code marked with `await` indicate that the current piece of code might pause execution while waiting for the asynchronous function or method to return. This is also called yielding the thread because, behind the scenes, Swift suspends the execution of your code on the current thread and runs some other code on that thread instead. Because code with `await` needs to be able to suspend execution, only certain places in your program can call asynchronous functions or methods:*

- *Code in the body of an asynchronous function, method, or property.*

- *Code in the static `main()` method of a structure, class, or enumeration that’s marked with `@main`.*

- *Code in an unstructured child task, as shown in [Unstructured Concurrency](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html#ID643) below.*

*Code in between possible suspension points runs sequentially, without the possibility of interruption from other concurrent code. For example, the code below moves a picture from one gallery to another.*

```swift
let firstPhoto = await listPhotos(inGallery: "Summer Vacation")[0]
add(firstPhoto toGallery: "Road Trip")
// At this point, firstPhoto is temporarily in both galleries.
remove(firstPhoto fromGallery: "Summer Vacation")
```

*There’s no way for other code to run in between the call to `add(_:toGallery:)` and `remove(_:fromGallery:)`. During that time, the first photo appears in both galleries, temporarily breaking one of the app’s invariants. To make it even clearer that this chunk of code must not have `await` added to it in the future, you can refactor that code into a synchronous function:*

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

> *NOTE*
> 
> *The [`Task.sleep(until:tolerance:clock:)`](https://developer.apple.com/documentation/swift/task/sleep(until:tolerance:clock:)) method is useful when writing simple code to learn how concurrency works. This method does nothing, but waits at least the given number of nanoseconds before it returns. Here’s a version of the `listPhotos(inGallery:)` function that uses `sleep(until:tolerance:clock:)` to simulate waiting for a network operation:*
> 
> ```swift
> func listPhotos(inGallery name: String) async throws -> [String] {
>     try await Task.sleep(until: .now + .seconds(2), clock: .continuous)
>     return ["IMG001", "IMG99", "IMG0404"]
> }
> ```


