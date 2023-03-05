### *Characteristics of Memory Access : 메모리 엑세스 특징*

- *At least one is a write access or a nonatomic access.*
  
  적어도 하나는 쓰기 액세스 또는 비원자 액세스입니다.

- *They access the same location in memory.*
  
  메모리의 동일한 위치에 액세스합니다.

- *Their durations overlap.*
  
  기간이 겹칩니다.

*The difference between a read and write access is usually obvious: a write access changes the location in memory, but a read access doesn’t. The location in memory refers to what is being accessed — for example, a variable, constant, or property. The duration of a memory access is either instantaneous or long-term.*

읽기 액세스와 쓰기 액세스의 차이는 일반적으로 분명합니다: 쓰기 액세스는 메모리의 위치를 변경하지만 읽기 액세스는 변경하지 않습니다. 메모리의 위치는 액세스 중인 항목(예: 변수, 상수 또는 프로퍼티)을 나타냅니다. 메모리 액세스 기간은 순간적이거나 장기적입니다.

*An operation is atomic if it uses only C atomic operations; otherwise it’s nonatomic. For a list of those functions, see the `stdatomic(3)` man page.*

C 원자 연산만 사용하는 연산은 원자적입니다; 그렇지 않으면 비원자적입니다. 이러한 함수 목록은 `stdatomic(3)` 매뉴얼 페이지를 참조하세요.

*An access is instantaneous if it’s not possible for other code to run after that access starts but before it ends. By their nature, two instantaneous accesses can’t happen at the same time. Most memory access is instantaneous. For example, all the read and write accesses in the code listing below are instantaneous:*

액세스가 시작된 후 종료되기 전에 다른 코드를 실행할 수 없는 경우 즉시 액세스할 수 있습니다. 본질적으로, 두 개의 순간 액세스는 동시에 발생할 수 없습니다. 대부분의 메모리 액세스는 순간적입니다. 예를 들어, 아래 코드 목록의 모든 읽기 및 쓰기 액세스는 순간적입니다:

```swift
func oneMore(than number: Int) -> Int {
    return number + 1
}

var myNumber = 1
myNumber = oneMore(than: myNumber)
print(myNumber)
// Prints "2"
```

*However, there are several ways to access memory, called long-term accesses, that span the execution of other code. The difference between instantaneous access and long-term access is that it’s possible for other code to run after a long-term access starts but before it ends, which is called overlap. A long-term access can overlap with other long-term accesses and instantaneous accesses.*

그러나 다른 코드의 실행에 걸쳐 있는 장기 액세스라고 하는 메모리에 액세스하는 몇 가지 방법이 있습니다. 순간 액세스와 장기 액세스의 차이점은 장기 액세스가 시작된 후에 종료되기 전에 다른 코드가 실행될 수 있다는 것입니다. 이를 오버랩이라고 합니다. 장기 액세스는 다른 장기 액세스 및 순간 액세스와 중복될 수 있습니다.

*Overlapping accesses appear primarily in code that uses in-out parameters in functions and methods or mutating methods of a structure. The specific kinds of Swift code that use long-term accesses are discussed in the sections below.*

중복 액세스는 주로 구조체의 함수와 메서드 또는 변환 메서드에서 인아웃 매개 변수를 사용하는 코드에 나타납니다. 장기 액세스를 사용하는 특정 유형의 Swift 코드는 아래 절에서 설명합니다.
