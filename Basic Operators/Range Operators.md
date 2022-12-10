## *Range Operators : 범위연산자*

*Swift includes several range operators, which are shortcuts for expressing a range of values.*

Swift는 값의 범위를 지름길로 나타내는 여러개의 범위 연산자를 포함합니다.

### *Closed Range Operator : 닫힌 범위 연산자*

*The closed range operator (`a...b`) defines a range that runs from `a` to `b`, and includes the values `a` and `b`. The value of `a` must not be greater than `b`.*

닫힌 범위 연산자 (`a...b`)는 a에서 b까지의 범위를 정의하며, `a`와 `b`값을 포함합니다. `a`의 값은 `b`의 값보다 커서는 안됩니다.

*The closed range operator is useful when iterating over a range in which you want all of the values to be used, such as with a `for`-`in` loop:*

닫힌 범위 연산자는 `for-in` 루프와 같이 사용하려는 범위에서 모든 값을 반복할 때 유용합니다. 

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

*For more about `for`-`in` loops, see [Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html).*

`for-in` 루프에 대한 더 많은 정보는 [링크]를 확인하세요.

### *Half-Open Range Operator : 반-열림 범위 연산자*

*The half-open range operator (`a..<b`) defines a range that runs from `a` to `b`, but doesn’t include `b`. It’s said to be half-open because it contains its first value, but not its final value. As with the closed range operator, the value of `a` must not be greater than `b`. If the value of `a` is equal to `b`, then the resulting range will be empty.*

반-열림 범위 연산자 (`a..<b`)는 a에서 b까지의 범위를 정의하지만 b를 포함하지 않습니다. 첫번재 값은 포함하지만 마지막 값은 포함하지 않기 때문에 반-열림 이라고 표현합니다. 닫힌 범위 연산자와 마찬가지로 `a`의  값은 `b`보다 크면 안됩니다. `a`와 `b`의 값이 같으면, 결과 범위는 비어있습니다.

*Half-open ranges are particularly useful when you work with zero-based lists such as arrays, where it’s useful to count up to (but not including) the length of the list:*

반-열림 범위는 배열과 같은 제로베이스 목록에서 목록의 길이를 (그러나 포함하지 않는) 최대로 세는 작업을할 때 유용합니다. *~~(해석의 한계..)~~*

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```

*Note that the array contains four items, but `0..<count` only counts as far as `3` (the index of the last item in the array), because it’s a half-open range. For more about arrays, see [Arrays](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html#ID107).*

배열에는 4개의 항목이 있지만 `0..<count`는 반열림 범위 이기 때문에 3(배열에서 마지막 항목의 인덱스)까지만 계산됩니다.  배열에 대한 자세한 것은 [링크]를 참조하세요.

### *One-Sided Ranges : 단방향 범위*

*The closed range operator has an alternative form for ranges that continue as far as possible in one direction—for example, a range that includes all the elements of an array from index 2 to the end of the array. In these cases, you can omit the value from one side of the range operator. This kind of range is called a one-sided range because the operator has a value on only one side. For example:*

닫힌 범위 연산자는 가능한 한 방향으로 계속되는 범위에 대한 대체 형식을 가집니다. - 예를들어, 인덱스 2부터 배열 끝까지 배열의 모든 요소를 포함하는 범위입니다. 이런 경우, 범위 연산의 한 쪽에서 값을 생략할 수 있습니다. 연산자가 한 쪽에만 값을 가지기 때문에 이런 종류의 범위를 단방향 범위라고 합니다. 예를 들면 :

```swift
for name in names[2...] {
    print(name)
}
// Brian
// Jack

for name in names[...2] {
    print(name)
}
// Anna
// Alex
// Brian
```

*The half-open range operator also has a one-sided form that’s written with only its final value. Just like when you include a value on both sides, the final value isn’t part of the range. For example:*

반-열림 범위 연산자는 또한 최종값만 사용하여 작성된 단방향 형태를 가집니다. 양쪽에 값을 포함하는 경우와 마찬가지로 최종 값은 범위의 일부가 아닙니다.

```swift
for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```

*One-sided ranges can be used in other contexts, not just in subscripts. You can’t iterate over a one-sided range that omits a first value, because it isn’t clear where iteration should begin. You can iterate over a one-sided range that omits its final value; however, because the range continues indefinitely, make sure you add an explicit end condition for the loop. You can also check whether a one-sided range contains a particular value, as shown in the code below.*

단방향 범위는 서브스크립트에서 뿐만 아니라 다른 컨텍스트에서도 사용할 수 있습니다. 반복이 어디서 시작되어야하는지 명확하지 않기 때문에 첫번째 값을 생략하는 단방향 범위에 대해 반복할 수 없습니다. 최종 값을 생락하는 단방향 범위에 대해 반복할 수 있지만 범위가 무한적으로 계속되므로 루프에 대한 명시적인 종료 조건을 추가해야합니다. 또한 아래 코드와 같이 단방향 범위에 특정 값이 포함되어있는지 확인할 수 있습니다. 

```swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```
