## *Substrings*

*When you get a substring from a string—for example, using a subscript or a method like `prefix(_:)`—the result is an instance of [`Substring`](https://developer.apple.com/documentation/swift/substring), not another string. Substrings in Swift have most of the same methods as strings, which means you can work with substrings the same way you work with strings. However, unlike strings, you use substrings for only a short amount of time while performing actions on a string. When you’re ready to store the result for a longer time, you convert the substring to an instance of `String`. For example:*

문자열에서 substring을 가져올 때 - 예를 들어, `prefix(_:)`와 같은 메서드를 사용할 때 - 결과는 다른 문자열이 아닌 `Substring` 의 인스턴스가 됩니다. Swift의 Substring은 대부분 문자열과 동일한 메서드를 가지고 있으며, 이는 문자열과 동일한 방식으로 Substring 작업을 할 수 있음을 의미합니다. 그러나 문자열과 달리 문자열에 대한 작업을 수행하는 동안에는 짧은 시간 동안만 substring을 사용합니다. 결과를 더 오래 저장할 준비가 되면 substring을 `String`의 인스턴스로 반환합니다. 예를 들어 :

```swift
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
let beginning = greeting[..<index]
// beginning is "Hello"

// Convert the result to a String for long-term storage.
let newString = String(beginning)
```

*Like strings, each substring has a region of memory where the characters that make up the substring are stored. The difference between strings and substrings is that, as a performance optimization, a substring can reuse part of the memory that’s used to store the original string, or part of the memory that’s used to store another substring. (Strings have a similar optimization, but if two strings share memory, they’re equal.) This performance optimization means you don’t have to pay the performance cost of copying memory until you modify either the string or substring. As mentioned above, substrings aren’t suitable for long-term storage—because they reuse the storage of the original string, the entire original string must be kept in memory as long as any of its substrings are being used.*

문자열과 마찬가지로 각 susbtring에는 susbtring을 구성하는 문자가 저장되는 메모리 영역이 있습니다. 문자열과 susbtring의 차이점은 성능 최적화로서 susbtring이 원래 문자열을 저장하는데 사용되는 메모리의 일부 혹은 다른 susbtring을 저장하는데 사용되는 메모리의 일부를 재사용할 수 있다는 것입니다. (`String`의 최적화는 비슷하지만 두 문자열이 메모리를 공유하는 경우 동일합니다.) 이러한 성능 최적화를 통해 문자열 혹은 susbtring을 수정할 때까지 메모리 복사에 대한 성능 비용을 지불할 필요가 없습니다. 위의 예시에서 언급한 바와 같이, `Substring`은 원래 문자열의 저장을 재사용하기 때문에, `Substring`이 사용되는 한 전체 문자열을 메모리에 보관해야 합니다.

*In the example above, `greeting` is a string, which means it has a region of memory where the characters that make up the string are stored. Because `beginning` is a substring of `greeting`, it reuses the memory that `greeting` uses. In contrast, `newString` is a string—when it’s created from the substring, it has its own storage. The figure below shows these relationships:*

 위의 예시에서 `greeting`은 문자열이며,  이는 문자열을 구성하는 문자가 저장되는 메모리 영역을 가지고 있음을 의미합니다. `beginning`은 `greeting`의 `substring`이기 때문에 `greeting`이 사용하는 메모리를 재사용합니다. 대조적으로 `newString`은 문자열로, substring에서 생성되면 자체 저장소가 있습니다. 아래의 그림은 이러한 관계를 보여줍니다. 

![](https://docs.swift.org/swift-book/_images/stringSubstring_2x.png)

> *NOTE*
> 
> *Both `String` and `Substring` conform to the [`StringProtocol`](https://developer.apple.com/documentation/swift/stringprotocol) protocol, which means it’s often convenient for string-manipulation functions to accept a `StringProtocol` value. You can call such functions with either a `String` or `Substring` value.*
> 
> `String`과 `Substring`은 모두 `StringProtocol` 프로토콜을 준수하는데, 이는 문자열 계산 함수가 `StringProtocol` 값을 받아들이기 편리하다는 것을 의미합니다.  `String` 혹은 `Substring` 값을 사용해서 이러한 함수를 호출할 수 있습니다.


