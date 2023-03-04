## *Understanding Conflicting Access to Memory : 메모리에 대한 액세스 충돌 이해*

*Access to memory happens in your code when you do things like set the value of a variable or pass an argument to a function. For example, the following code contains both a read access and a write access:*

메모리에 대한 액세스는 변수의 값을 설정하거나 함수에 인수를 전달하는 등의 작업을 수행할 때 코드에서 발생합니다. 예를 들어, 다음 코드에는 읽기 액세스와 쓰기 액세스가 모두 포함되어 있습니다:

```swift
// A write access to the memory where one is stored.
var one = 1

// A read access from the memory where one is stored.
print("We're number \(one)!")
```

*A conflicting access to memory can occur when different parts of your code are trying to access the same location in memory at the same time. Multiple accesses to a location in memory at the same time can produce unpredictable or inconsistent behavior. In Swift, there are ways to modify a value that span several lines of code, making it possible to attempt to access a value in the middle of its own modification.*

코드의 다른 부분이 동시에 메모리의 동일한 위치에 액세스하려고 할 때 메모리에 대한 액세스가 충돌할 수 있습니다. 메모리의 한 위치에 동시에 여러 번 액세스하면 예측할 수 없거나 일관성이 없는 동작이 발생할 수 있습니다. Swift에서는 코드의 여러 줄에 걸쳐 있는 값을 수정하여 자체 수정 도중에 값에 액세스할 수 있도록 하는 방법이 있습니다.

*You can see a similar problem by thinking about how you update a budget that’s written on a piece of paper. Updating the budget is a two-step process: First you add the items’ names and prices, and then you change the total amount to reflect the items currently on the list. Before and after the update, you can read any information from the budget and get a correct answer, as shown in the figure below.*

종이에 적힌 예산을 어떻게 업데이트하는지 생각해보면 비슷한 문제를 알 수 있습니다. 예산 업데이트는 두 단계로 이루어집니다: 먼저 항목의 이름과 가격을 추가한 다음 현재 목록에 있는 항목을 반영하도록 총 금액을 변경합니다. 아래 그림과 같이 업데이트 전후에 예산에서 정보를 읽고 정답을 얻을 수 있습니다.

*![](https://docs.swift.org/swift-book/images/memory_shopping@2x.png)*

*While you’re adding items to the budget, it’s in a temporary, invalid state because the total amount hasn’t been updated to reflect the newly added items. Reading the total amount during the process of adding an item gives you incorrect information.*

예산에 항목을 추가하는 동안 총 금액이 새로 추가된 항목을 반영하도록 업데이트되지 않아 일시적으로 유효하지 않은 상태입니다. 항목을 추가하는 과정에서 총 금액을 읽으면 잘못된 정보를 얻을 수 있습니다.

*This example also demonstrates a challenge you may encounter when fixing conflicting access to memory: There are sometimes multiple ways to fix the conflict that produce different answers, and it’s not always obvious which answer is correct. In this example, depending on whether you wanted the original total amount or the updated total amount, either $5 or $320 could be the correct answer. Before you can fix the conflicting access, you have to determine what it was intended to do.*

이 예에서는 메모리에 대한 액세스 충돌을 수정할 때 발생할 수 있는 문제도 보여 줍니다: 갈등을 해결하기 위한 여러 가지 방법이 있어 서로 다른 답을 만들어내기도 합니다. 어떤 답이 옳은지 항상 명확한 것은 아닙니다. 이 예에서는 원래 총 금액을 원하는지 아니면 업데이트된 총 금액을 원하는지에 따라 5달러 또는 320달러가 정답일 수 있습니다. 충돌하는 액세스를 수정하려면 먼저 액세스가 의도한 작업을 결정해야 합니다.

> *Note*
> 
> *If you’ve written concurrent or multithreaded code, conflicting access to memory might be a familiar problem. However, the conflicting access discussed here can happen on a single thread and doesn’t involve concurrent or multithreaded code.*
> 
> 동시성 또는 멀티 스레드 코드를 작성한 경우 메모리에 대한 액세스가 충돌하는 것은 익숙한 문제일 수 있습니다. 그러나 여기서 설명하는 액세스 충돌은 단일 스레드에서 발생할 수 있으며 동시성이나 멀티 스레드 코드를 포함하지 않습니다.
> 
> *If you have conflicting access to memory from within a single thread, Swift guarantees that you’ll get an error at either compile time or runtime. For multithreaded code, use [Thread Sanitizer](https://developer.apple.com/documentation/xcode/diagnosing_memory_thread_and_crash_issues_early) to help detect conflicting access across threads.*
> 
> 단일 스레드 내에서 메모리에 대한 액세스가 충돌하는 경우 Swift는 컴파일 타임 또는 런타임에 오류가 발생할 것을 보장합니다. 멀티스레드 코드의 경우 [Thread Sanitizer]를 사용하여 스레드 간에 액세스가 충돌하는 것을 탐지하세요.
