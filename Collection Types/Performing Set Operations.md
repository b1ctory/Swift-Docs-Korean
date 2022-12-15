## *Performing Set Operations*

*You can efficiently perform fundamental set operations, such as combining two sets together, determining which values two sets have in common, or determining whether two sets contain all, some, or none of the same values.*

### *Fundamental Set Operations*

*The illustration below depicts two sets—`a` and `b`—with the results of various set operations represented by the shaded regions.*

*![](https://docs.swift.org/swift-book/_images/setVennDiagram_2x.png)*

- *Use the `intersection(_:)` method to create a new set with only the values common to both sets.*

- *Use the `symmetricDifference(_:)` method to create a new set with values in either set, but not both.*

- *Use the `union(_:)` method to create a new set with all of the values in both sets.*

- *Use the `subtracting(_:)` method to create a new set with values not in the specified set.*

```swift
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]

oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]
```

### *Set Membership and Equality*

*The illustration below depicts three sets—`a`, `b` and `c`—with overlapping regions representing elements shared among sets. Set `a` is a superset of set `b`, because `a` contains all elements in `b`. Conversely, set `b` is a subset of set `a`, because all elements in `b` are also contained by `a`. Set `b` and set `c` are disjoint with one another, because they share no elements in common.*

![](https://docs.swift.org/swift-book/_images/setEulerDiagram_2x.png)

- *Use the “is equal” operator (`==`) to determine whether two sets contain all of the same values.*

- *Use the `isSubset(of:)` method to determine whether all of the values of a set are contained in the specified set.*

- *Use the `isSuperset(of:)` method to determine whether a set contains all of the values in a specified set.*

- *Use the `isStrictSubset(of:)` or `isStrictSuperset(of:)` methods to determine whether a set is a subset or superset, but not equal to, a specified set.*

- *Use the `isDisjoint(with:)` method to determine whether two sets have no values in common.*

```swift
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
```


