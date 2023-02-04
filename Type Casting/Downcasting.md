## *Downcasting : 다운캐스팅*

*A constant or variable of a certain class type may actually refer to an instance of a subclass behind the scenes. Where you believe this is the case, you can try to downcast to the subclass type with a type cast operator (`as?` or `as!`).*

특정 클래스 타입의 상수 또는 변수는 실제로 하위 클래스의 인스턴스(instance of subclass)를 의미할 수 있습니다. 이 경우 타입 캐스트 연산자(`as?` 또는 `as!`)를 사용하여 하위 클래스 타입으로 다운캐스트할 수 있습니다.

*Because downcasting can fail, the type cast operator comes in two different forms. The conditional form, `as?`, returns an optional value of the type you are trying to downcast to. The forced form, `as!`, attempts the downcast and force-unwraps the result as a single compound action.*

다운캐스팅이 실패할 수 있기 때문에 타입 캐스트 연산자는 두 가지 형태로 제공됩니다. 조건부 형식인 `as?`는 다운캐스트하려는 타입의 옵셔널 값을 반환합니다. 강제 형식인 `as!`는 다운캐스트를 시도하고 결과를 단일 복합 동작으로 강제 언래핑합니다.

*Use the conditional form of the type cast operator (`as?`) when you aren’t sure if the downcast will succeed. This form of the operator will always return an optional value, and the value will be `nil` if the downcast was not possible. This enables you to check for a successful downcast.*

다운캐스트가 성공할지 확실하지 않을 때는 타입캐스트 연산자(`as?`)의 조건부 형식을 사용합니다. 이 형식의 연산자는 항상 옵셔널 값을 반환하고 다운캐스트가 불가능한 경우 값은 `nil`이 됩니다. 이렇게 하면 성공적인 다운캐스트를 확인할 수 있습니다.

*Use the forced form of the type cast operator (`as!`) only when you are sure that the downcast will always succeed. This form of the operator will trigger a runtime error if you try to downcast to an incorrect class type.*

다운캐스트가 항상 성공할 것이 확실한 경우에만 타입 캐스트 연산자(`as!`)의 강제 형식을 사용하세요. 이 형식의 연산자는 잘못된 클래스 타입으로 다운캐스트를 시도할 경우 런타임 오류를 트리거합니다.

*The example below iterates over each `MediaItem` in `library`, and prints an appropriate description for each item. To do this, it needs to access each item as a true `Movie` or `Song`, and not just as a `MediaItem`. This is necessary in order for it to be able to access the `director` or `artist` property of a `Movie` or `Song` for use in the description.*

아래 예제는 `library` 각 `MediaItem`에 대해 반복적으로 설명하고 각 항목에 대해 적절한 설명을 인쇄합니다. 그러기 위해서는 각 아이템을 `MediaItem`이 아닌 진짜 `Movie`나 `Song`으로 접근해야 합니다. 이는 `Movie`나 `Song`의 `director`나 `artist` 아티스트 프로퍼티에 접근해 설명에 사용할 수 있도록 하기 위해 필요합니다.

*In this example, each item in the array might be a `Movie`, or it might be a `Song`. You don’t know in advance which actual class to use for each item, and so it’s appropriate to use the conditional form of the type cast operator (`as?`) to check the downcast each time through the loop:*

이 예에서는 배열의 각 아이템이 `Movie`이거나 `Song`일 수 있습니다. 각 아이템에 사용할 실제 클래스를 미리 알지 못하기 때문에 루프를 통해 매번 다운캐스트를 확인하기 위해 타입 캐스트 연산자(`as?`)의 조건부 형식을 사용하는 것이 적절합니다:

```swift
for item in library {
    if let movie = item as? Movie {
        print("Movie: \(movie.name), dir. \(movie.director)")
    } else if let song = item as? Song {
        print("Song: \(song.name), by \(song.artist)")
    }
}

// Movie: Casablanca, dir. Michael Curtiz
// Song: Blue Suede Shoes, by Elvis Presley
// Movie: Citizen Kane, dir. Orson Welles
// Song: The One And Only, by Chesney Hawkes
// Song: Never Gonna Give You Up, by Rick Astley
```

*The example starts by trying to downcast the current `item` as a `Movie`. Because `item` is a `MediaItem` instance, it’s possible that it might be a `Movie`; equally, it’s also possible that it might be a `Song`, or even just a base `MediaItem`. Because of this uncertainty, the `as?` form of the type cast operator returns an optional value when attempting to downcast to a subclass type. The result of `item as? Movie` is of type `Movie?`, or “optional `Movie`”.*

이 예는 현재의 `item`을 `Movie`로 다운캐스트하는 것으로 시작합니다. `item`은 `MediaItem` 인스턴스이기 때문에 `Movie`일 수도 있고 `Song`일 수도 있고 기본 `MediaItem`일 수도 있습니다. 이 불확실성 때문에, `as?` 타입 캐스트 연산자의 형식은 하위 클래스 형식으로 다운캐스트를 시도할 때 옵셔널 값을 반환합니다. `item as? Movie` 결과는 `Movie?` 의 타입 혹은 또는 "옵셔널 `Movie`" 타입입니다.

*Downcasting to `Movie` fails when applied to the `Song` instances in the library array. To cope with this, the example above uses optional binding to check whether the optional `Movie` actually contains a value (that is, to find out whether the downcast succeeded.) This optional binding is written “`if let movie = item as? Movie`”, which can be read as:*

라이브러리 배열의 `Song` 인스턴스에 적용하면 `Movie`로 다운캐스트가 실패합니다. 이를 해결하기 위해 위의 예에서는 옵셔널 바인딩을 사용하여 옵셔널 `Movie`에 실제로 값이 포함되어 있는지 확인합니다(즉, 다운캐스트가 성공했는지 여부를 확인합니다) 이 옵셔널 바인딩은 “`if let movie = item as? Movie`” 이라고 쓰여 있으며, 다음과 같이 읽을 수 있습니다:

*“Try to access `item` as a `Movie`. If this is successful, set a new temporary constant called `movie` to the value stored in the returned optional `Movie`.”*

`item`을 `Movie`로 접해 보세요. 성공하면 `movie`라는 새로운 임시 상수를 반환된 옵셔널인 `Movie`에 저장된 값으로 설정합니다.

*If the downcasting succeeds, the properties of `movie` are then used to print a description for that `Movie` instance, including the name of its `director`. A similar principle is used to check for `Song` instances, and to print an appropriate description (including `artist` name) whenever a `Song` is found in the library.*

다운캐스팅이 성공하면 `movie` 프로퍼티를 사용하여 `director`의 이름을 포함한 `Movie` 인스턴스에 대한 설명을 출력합니다. 비슷한 원리로 라이브러리에서 `Song`이 발견될 때마다 `Song` 인스턴스를 확인하고 적절한 설명(`artist` 이름 포함)을 출력합니다.

> *NOTE*
> 
> *Casting doesn’t actually modify the instance or change its values. The underlying instance remains the same; it’s simply treated and accessed as an instance of the type to which it has been cast.*
> 
> 캐스팅은 실제로 인스턴스를 수정하거나 값을 변경하지 않습니다. 기본 인스턴스는 그대로 유지되며, 단순히 캐스팅된 유형의 인스턴스로 처리되고 액세스됩니다.
