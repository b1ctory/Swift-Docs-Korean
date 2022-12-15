## *Performing Set Operations : 집합 작업 수행*

*You can efficiently perform fundamental set operations, such as combining two sets together, determining which values two sets have in common, or determining whether two sets contain all, some, or none of the same values.*

두 집합을 함께 결합하거나 두 집합이 공통적으로 갖는 값을 결정하거나, 두 집합에 동일한 값이 모두 포함되는지 일부 포함되지 않는지 확인하는 등의 기본적인 집합 작업을 효율적으로 수행할 수 있습니다.

### *Fundamental Set Operations : 기본 집합 운영*

*The illustration below depicts two sets—`a` and `b`—with the results of various set operations represented by the shaded regions.*

아래 그림은 음영 영역으로 표현되는 다양한 집합 연산의 결과와 함께 두 집합인 `a`와 `b`를 보여줍니다.

*![](https://docs.swift.org/swift-book/_images/setVennDiagram_2x.png)*

- *Use the `intersection(_:)` method to create a new set with only the values common to both sets.*
  
  `intersection(_:)` 메서드를 사용해서 두 집합에 공통된 값만 사용해서 새 집합을 만듭니다.

- *Use the `symmetricDifference(_:)` method to create a new set with values in either set, but not both.*
  
  `symmetricDifference(_:)` 메서드를 사용해서 두 집합 중 하나에 값을 포함하되 둘 다 포함하지 않는 새 집합을 만듭니다.

- *Use the `union(_:)` method to create a new set with all of the values in both sets.*
  
  `union(_:)` 메서드를 사용해서 두 집합의 모든 값을 사용해서 새 집합을 만듭니다.

- *Use the `subtracting(_:)` method to create a new set with values not in the specified set.*
  
  `subtracting(_:)` 메서드를 사용해서 지정된 집합에 없는 값으로 새 집합을 만듭니다.

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

### *Set Membership and Equality : 집합 멤버십과 동등성*

*The illustration below depicts three sets—`a`, `b` and `c`—with overlapping regions representing elements shared among sets. Set `a` is a superset of set `b`, because `a` contains all elements in `b`. Conversely, set `b` is a subset of set `a`, because all elements in `b` are also contained by `a`. Set `b` and set `c` are disjoint with one another, because they share no elements in common.*

아래 그림은 집합 간에 공유되는 요소를 나타내는 겹치는 영역이 있는 `a`,`b` 그리고 `c` 의 세 집합을 보여준다. `a`는 `b`의 모든 요소를 포함하기 때문에 집합 `a`는 집합 `b`의 초집합이다. 반대로, 집합 `b`는 집합 `a`의 부분집합이다. 집합 `b`와 집합 `c`는 공통된 요소를 공유하지 않기 때문에 서로 분리되어 있다.

![](https://docs.swift.org/swift-book/_images/setEulerDiagram_2x.png)

- *Use the “is equal” operator (`==`) to determine whether two sets contain all of the same values.*
  
  "is equal" 연산자 (`==`)를 사용해서 두 집합이 동일한 값을 모두 포함하는지 여부를 확인합니다.

- *Use the `isSubset(of:)` method to determine whether all of the values of a set are contained in the specified set.*
  
  `isSubset(of:)`메서드를 사용해서 집합의 모든 값이 지정된 집합에 포함되어 있는지 확인합니다.

- *Use the `isSuperset(of:)` method to determine whether a set contains all of the values in a specified set.*
  
  `isSuperset(of:)` 메서드를 사용해서 집합이 지정된 집합의 모든 값을 포함하는지 여부를 확인합니다.

- *Use the `isStrictSubset(of:)` or `isStrictSuperset(of:)` methods to determine whether a set is a subset or superset, but not equal to, a specified set.*
  
   `isStrictSubset(of:)` 혹은 `isStrictSuperset(of:)` 메서드를 사용해서 집합이 지정된 집합과 동일하지는 않지만 부분 집합인지 초집합인지 확인합니다.

- *Use the `isDisjoint(with:)` method to determine whether two sets have no values in common.*
  
  `isDisjoint(with:)`메서드를 사용해서 두 집합에 공통값이 없는지 확인합니다.

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
