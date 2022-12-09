## *Range Operators*

*Swift includes several range operators, which are shortcuts for expressing a range of values.*

### *Closed Range Operator*

*The closed range operator (`a...b`) defines a range that runs from `a` to `b`, and includes the values `a` and `b`. The value of `a` must not be greater than `b`.*

*The closed range operator is useful when iterating over a range in which you want all of the values to be used, such as with a `for`-`in` loop:*

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

### *Half-Open Range Operator*

*The half-open range operator (`a..<b`) defines a range that runs from `a` to `b`, but doesn’t include `b`. It’s said to be half-open because it contains its first value, but not its final value. As with the closed range operator, the value of `a` must not be greater than `b`. If the value of `a` is equal to `b`, then the resulting range will be empty.*

*Half-open ranges are particularly useful when you work with zero-based lists such as arrays, where it’s useful to count up to (but not including) the length of the list:*

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

### *One-Sided Ranges*

*The closed range operator has an alternative form for ranges that continue as far as possible in one direction—for example, a range that includes all the elements of an array from index 2 to the end of the array. In these cases, you can omit the value from one side of the range operator. This kind of range is called a one-sided range because the operator has a value on only one side. For example:*

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

```swift
for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```

*One-sided ranges can be used in other contexts, not just in subscripts. You can’t iterate over a one-sided range that omits a first value, because it isn’t clear where iteration should begin. You can iterate over a one-sided range that omits its final value; however, because the range continues indefinitely, make sure you add an explicit end condition for the loop. You can also check whether a one-sided range contains a particular value, as shown in the code below.*

```swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```
