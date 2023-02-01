## *Calling Asynchronous Functions in Parallel : 비동기 함수를 병렬로 호출*

*Calling an asynchronous function with `await` runs only one piece of code at a time. While the asynchronous code is running, the caller waits for that code to finish before moving on to run the next line of code. For example, to fetch the first three photos from a gallery, you could await three calls to the `downloadPhoto(named:)` function as follows:*

`await`을 사용하여 비동기 함수를 호출하면 한 번에 하나의 코드만 실행됩니다. 비동기 코드가 실행되는 동안 호출자는 코드가 완료될 때까지 기다렸다가 다음 코드 행을 실행합니다. 예를 들어 갤러리에서 처음 세 장의 사진을 가져오려면 다음과 같이 `downloadPhoto(named:)` 함수에 대한 세 번의 호출을 기다릴 수 있습니다:

```swift
let firstPhoto = await downloadPhoto(named: photoNames[0])
let secondPhoto = await downloadPhoto(named: photoNames[1])
let thirdPhoto = await downloadPhoto(named: photoNames[2])

let photos = [firstPhoto, secondPhoto, thirdPhoto]
show(photos)
```

*This approach has an important drawback: Although the download is asynchronous and lets other work happen while it progresses, only one call to `downloadPhoto(named:)` runs at a time. Each photo downloads completely before the next one starts downloading. However, there’s no need for these operations to wait—each photo can download independently, or even at the same time.*

이 접근 방식에는 중요한 단점이 있습니다: 다운로드가 비동기식이므로 다른 작업이 진행되는 동안에도 `downloadPhoto(named:)` 호출은 한 번에 하나만 실행됩니다. 각 사진은 다음 사진 다운로드가 시작되기 전에 완전히 다운로드됩니다. 그러나 각 사진을 개별적으로 다운로드하거나 동시에 다운로드할 수 있으므로 작업을 기다릴 필요가 없습니다.

*To call an asynchronous function and let it run in parallel with code around it, write `async` in front of `let` when you define a constant, and then write `await` each time you use the constant.*

비동기 함수를 호출하여 주변의 코드와 병렬로 실행하려면 상수를 정의할 때 `let` 앞에 `async`를 쓰고, 상수를 사용할 때마다 `await`을 적습니다.

```swift
async let firstPhoto = downloadPhoto(named: photoNames[0])
async let secondPhoto = downloadPhoto(named: photoNames[1])
async let thirdPhoto = downloadPhoto(named: photoNames[2])

let photos = await [firstPhoto, secondPhoto, thirdPhoto]
show(photos)
```

*In this example, all three calls to `downloadPhoto(named:)` start without waiting for the previous one to complete. If there are enough system resources available, they can run at the same time. None of these function calls are marked with `await` because the code doesn’t suspend to wait for the function’s result. Instead, execution continues until the line where `photos` is defined—at that point, the program needs the results from these asynchronous calls, so you write `await` to pause execution until all three photos finish downloading.*

이 예에서는 이전 호출이 완료될 때까지 기다리지 않고  `downloadPhoto(named:)`호출이 모두 시작됩니다. 사용 가능한 시스템 리소스가 충분하면 리소스를 동시에 실행할 수 있습니다. 코드가 함수의 결과를 대기하기 위해 일시 중단되지 않기 때문에 이러한 함수 호출 중 어떤 것도 `await`으로 표시되지 않습니다. 대신 `photos`가 정의된 줄까지 실행이 계속됩니다. ㅡ 이 시점에서 프로그램은 이러한 비동기 호출의 결과를 필요로 하므로 세 개의 사진이 모두 다운로드될 때까지 실행을 일시 중지하려면 `await`을 작성합니다.

*Here’s how you can think about the differences between these two approaches:*

이 두 가지 접근 방식의 차이점을 생각해 볼 수 있는 방법은 다음과 같습니다:

- *Call asynchronous functions with `await` when the code on the following lines depends on that function’s result. This creates work that is carried out sequentially.*
  
  다음 줄의 코드가 해당 함수의 결과에 따라 다를 때 `await`를 사용하여 비동기 함수를 호출합니다. 이것은 순차적으로 수행되는 작업을 만듭니다.

- *Call asynchronous functions with `async`-`let` when you don’t need the result until later in your code. This creates work that can be carried out in parallel.*
  
  코드에서 나중까지 결과가 필요하지 않을 때는 `async`-`let`을 사용하여 비동기 함수를 호출합니다. 이것은 병렬로 수행될 수 있는 작업을 만듭니다.

- *Both `await` and `async`-`let` allow other code to run while they’re suspended.*
  
   `await` 과 `async`-`let`모두 일시 중단된 상태에서 다른 코드를 실행할 수 있습니다.

- *In both cases, you mark the possible suspension point with `await` to indicate that execution will pause, if needed, until an asynchronous function has returned.*
  
  두 경우 모두 가능한 일시 중단 지점을 `await`로 표시하여 필요한 경우 비동기 함수가 돌아올 때까지 실행이 일시 중지됨을 나타냅니다.

*You can also mix both of these approaches in the same code.*

또한 이 두 가지 접근 방식을 동일한 코드로 혼합할 수 있습니다.
