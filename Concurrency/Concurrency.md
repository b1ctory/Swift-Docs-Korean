# *Concurrency*

*Swift has built-in support for writing asynchronous and parallel code in a structured way. Asynchronous code can be suspended and resumed later, although only one piece of the program executes at a time. Suspending and resuming code in your program lets it continue to make progress on short-term operations like updating its UI while continuing to work on long-running operations like fetching data over the network or parsing files. Parallel code means multiple pieces of code run simultaneously—for example, a computer with a four-core processor can run four pieces of code at the same time, with each core carrying out one of the tasks. A program that uses parallel and asynchronous code carries out multiple operations at a time; it suspends operations that are waiting for an external system, and makes it easier to write this code in a memory-safe way.*

*The additional scheduling flexibility from parallel or asynchronous code also comes with a cost of increased complexity. Swift lets you express your intent in a way that enables some compile-time checking—for example, you can use actors to safely access mutable state. However, adding concurrency to slow or buggy code isn’t a guarantee that it will become fast or correct. In fact, adding concurrency might even make your code harder to debug. However, using Swift’s language-level support for concurrency in code that needs to be concurrent means Swift can help you catch problems at compile time.*

*The rest of this chapter uses the term concurrency to refer to this common combination of asynchronous and parallel code.*

> *NOTE*
> 
> *If you’ve written concurrent code before, you might be used to working with threads. The concurrency model in Swift is built on top of threads, but you don’t interact with them directly. An asynchronous function in Swift can give up the thread that it’s running on, which lets another asynchronous function run on that thread while the first function is blocked. When an asynchronous function resumes, Swift doesn’t make any guarantee about which thread that function will run on.*

*Although it’s possible to write concurrent code without using Swift’s language support, that code tends to be harder to read. For example, the following code downloads a list of photo names, downloads the first photo in that list, and shows that photo to the user:*

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


