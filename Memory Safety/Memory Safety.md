# *Memory Safety : 메모리 안전성*

*Structure your code to avoid conflicts when accessing memory.*

메모리에 액세스할 때 충돌이 발생하지 않도록 코드를 구성합니다.

*By default, Swift prevents unsafe behavior from happening in your code. For example, Swift ensures that variables are initialized before they’re used, memory isn’t accessed after it’s been deallocated, and array indices are checked for out-of-bounds errors.*

기본적으로 Swift는 코드에서 안전하지 않은 동작이 발생하는 것을 방지합니다. 예를 들어 Swift는 변수를 사용하기 전에 초기화하고, 할당 해제된 후에는 메모리에 액세스하지 않으며, 배열 인덱스의 범위 외 오류를 검사합니다.

*Swift also makes sure that multiple accesses to the same area of memory don’t conflict, by requiring code that modifies a location in memory to have exclusive access to that memory. Because Swift manages memory automatically, most of the time you don’t have to think about accessing memory at all. However, it’s important to understand where potential conflicts can occur, so you can avoid writing code that has conflicting access to memory. If your code does contain conflicts, you’ll get a compile-time or runtime error.*

Swift는 또한 메모리의 위치를 수정하는 코드가 해당 메모리에 독점적으로 액세스할 수 있도록 하여 동일한 메모리 영역에 대한 여러 액세스가 충돌하지 않도록 합니다. Swift는 메모리를 자동으로 관리하기 때문에 대부분의 경우 메모리에 액세스할 생각을 전혀 하지 않아도 됩니다. 그러나 메모리에 대한 액세스 권한이 충돌하는 코드를 작성하지 않도록 잠재적 충돌이 발생할 수 있는 위치를 이해하는 것이 중요합니다. 코드에 충돌이 있는 경우 컴파일 타임 또는 런타임 오류가 발생합니다.
