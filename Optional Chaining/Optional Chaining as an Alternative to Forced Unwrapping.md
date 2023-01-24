## *Optional Chaining as an Alternative to Forced Unwrapping : 강제 언래핑의 대안으로 옵셔널 체이닝 사용*

*You specify optional chaining by placing a question mark (`?`) after the optional value on which you wish to call a property, method or subscript if the optional is non-`nil`. This is very similar to placing an exclamation point (`!`) after an optional value to force the unwrapping of its value. The main difference is that optional chaining fails gracefully when the optional is `nil`, whereas forced unwrapping triggers a runtime error when the optional is `nil`.*

옵셔널이 nil이 아닌 경우 프로퍼티, 메서드 또는 서브스크립트를 호출할 옵셔널 값 뒤에 물음표(`?`)를 붙여 옵셔널 체인을 지정합니다. 이는 옵셔널 값 뒤에 느낌표(`!`)를 배치하여 값의 강제 언래 것과 매우 유사합니다. 주요 차이점은 옵셔널 체인이 옵셔널이 `nil`일 때 정상적으로 실패하는 반면 강제 언래핑은 옵셔널이 `nil`일 때 런타임 오류를 트리거한다는 것입니다.

*To reflect the fact that optional chaining can be called on a `nil` value, the result of an optional chaining call is always an optional value, even if the property, method, or subscript you are querying returns a non-optional value. You can use this optional return value to check whether the optional chaining call was successful (the returned optional contains a value), or didn’t succeed due to a `nil` value in the chain (the returned optional value is `nil`).*

옵셔널 체인이 `nil` 값에서 호출될 수 있다는 사실을 반영하기 위해, 쿼리 중인 프로퍼티, 메서드 또는 서브스크립트가 옵셔널이 아닌 값을 반환하더라도 옵셔널 체인 호출의 결과는 항상 옵셔널 값입니다. 이 옵셔널 반환 값을 사용하여 옵셔널 체인 호출이 성공했는지(반환된 옵셔널에는 값이 포함됨), 체인의 `nil` 값 때문에 실패했는지(반환된 옵셔널 값은 `nil`)를 확인할 수 있습니다.

*Specifically, the result of an optional chaining call is of the same type as the expected return value, but wrapped in an optional. A property that normally returns an `Int` will return an `Int?` when accessed through optional chaining.*

특히, 옵셔널 체이닝 호출의 결과는 예상 반환 값과 동일한 타입이지만 옵셔널로 포장됩니다. 일반적으로 `Int`를 반환하는 프로퍼티는 옵셔널 체이닝을 통해 접근할때 `Int?` 를 반환합니다. 

*The next several code snippets demonstrate how optional chaining differs from forced unwrapping and enables you to check for success.*

다음 몇 가지 코드 스니펫에서는 옵셔널 체이닝이 강제 언래핑과 어떻게 다른지 보여주며 성공 여부를 확인할 수 있습니다.

*First, two classes called `Person` and `Residence` are defined:*

먼저 `Person`과 `Residence`라는 두 가지 클래스가 정의됩니다:

```swift
class Person {
    var residence: Residence?
}

class Residence {
    var numberOfRooms = 1
}
```

*`Residence` instances have a single `Int` property called `numberOfRooms`, with a default value of `1`. `Person` instances have an optional `residence` property of type `Residence?`.*

`Residence` 인스턴스에는 기본값이 `1`인 `numberOfRooms`라는 단일 `Int` 프로퍼티가 있습니다. `Person` 인스턴스에는 `Residence?` 타입의 옵셔널 `residence` 프로퍼티가 있습니다.

*If you create a new `Person` instance, its `residence` property is default initialized to `nil`, by virtue of being optional. In the code below, `john` has a `residence` property value of `nil`:*

새 `Person` 인스턴스를 만들면 옵셔널이기 때문에 해당 `residence` 프로퍼티가 기본적으로 `nil`로 초기화됩니다. 아래 코드에서 `john`은 `residence` 프로퍼티 값이 `nil`입니다:

```swift
let john = Person()
```

*If you try to access the `numberOfRooms` property of this person’s `residence`, by placing an exclamation point after `residence` to force the unwrapping of its value, you trigger a runtime error, because there’s no `residence` value to unwrap:*

이 사람의 `residence`의 `numberOfRooms` 프로퍼티에 액세스하려고 할 때 `residence` 뒤에 느낌표를 붙여 해당 값을 강제로 언래핑하면 다음과 같은 `residence` 값이 없기 때문에 런타임 오류가 발생합니다:

```swift
let roomCount = john.residence!.numberOfRooms
// this triggers a runtime error
```

*The code above succeeds when `john.residence` has a non-`nil` value and will set `roomCount` to an `Int` value containing the appropriate number of rooms. However, this code always triggers a runtime error when `residence` is `nil`, as illustrated above.*

위의 코드는 `john.residence`가 `nil`이 아닌 값을 가질 때 성공하고 `roomCount`를 적절한 방 수를 포함하는 `Int`값으로 설정합니다. 그러나 이 코드는 위에서 설명한 바와 같이 `residence`가 `nil`일 때 항상 런타임 오류를 트리거합니다.

*Optional chaining provides an alternative way to access the value of `numberOfRooms`. To use optional chaining, use a question mark in place of the exclamation point:*

옵셔널 체이닝은 `numberOfRooms` 값에 액세스할 수 있는 대체 방법을 제공합니다. 옵셔널 체이닝을 사용하려면 느낌표 대신 물음표를 사용합니다:

```swift
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "Unable to retrieve the number of rooms."
```

*This tells Swift to “chain” on the optional `residence` property and to retrieve the value of `numberOfRooms` if `residence` exists.*

이것은 Swift에게 옵셔널 `residence` 프로퍼티를 "체인"하고 '레지던스'가 존재하는 경우 'numberOfRooms' 값을 검색하도록 지시합니다.

*Because the attempt to access `numberOfRooms` has the potential to fail, the optional chaining attempt returns a value of type `Int?`, or “optional `Int`”. When `residence` is `nil`, as in the example above, this optional `Int` will also be `nil`, to reflect the fact that it was not possible to access `numberOfRooms`. The optional `Int` is accessed through optional binding to unwrap the integer and assign the non-optional value to the `roomCount` constant.*

`numberOfRooms`에 액세스하려는 시도는 실패할 가능성이 있으므로 옵셔널 체이닝 시도는 타입 `Int?` 또는 "옵셔널 `Int`"의 값을 반환합니다. 위의 예와 같이 `residence`가 `nil`인 경우 이 옵셔널 `Int`도 `nil`이 되어 `numberOfRooms`에 액세스할 수 없었다는 사실을 반영합니다. 옵셔널 `Int`는 옵셔널 바인딩을 통해 액세스하여 정수를 언래핑하고 옵셔널이 아닌 값을 `roomCount` 상수에 할당합니다.

*Note that this is true even though `numberOfRooms` is a non-optional `Int`. The fact that it’s queried through an optional chain means that the call to `numberOfRooms` will always return an `Int?` instead of an `Int`.*

`numberOfRooms`가 옵셔널이 아닌 `Int`인 경우에도 마찬가지입니다. 옵셔널 체이닝을 통해 조회된다는 것은 `numberOfRooms` 호출이 항상 `Int`대신에 `Int?`를 반환한다는 것을 의미합니다.

*You can assign a `Residence` instance to `john.residence`, so that it no longer has a `nil` value:*

`Residence` 인스턴스를 `john.residence`에 할당하여 더 이상 `nil` 값을 갖지 않도록 할 수 있습니다:

```swift
john.residence = Residence()
```

*`john.residence` now contains an actual `Residence` instance, rather than `nil`. If you try to access `numberOfRooms` with the same optional chaining as before, it will now return an `Int?` that contains the default `numberOfRooms` value of `1`:*

이제 `john.residence`는 `nil`이 아닌 실제 `Residence` 인스턴스를 포함합니다. 이전과 동일한 옵셔널 체이닝으로 `numberOfRooms`에 액세스하려고 하면 이제 `Int?`가 반환됩니다. 여기에는 기본 `numberOfRooms` 값인 `1`이 포함됩니다:

```swift
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "John's residence has 1 room(s)."
```
