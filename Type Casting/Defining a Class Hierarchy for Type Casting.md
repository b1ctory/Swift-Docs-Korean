## *Defining a Class Hierarchy for Type Casting : 타입 캐스팅을 위한 클래스 계층 정의*

*You can use type casting with a hierarchy of classes and subclasses to check the type of a particular class instance and to cast that instance to another class within the same hierarchy. The three code snippets below define a hierarchy of classes and an array containing instances of those classes, for use in an example of type casting.*

클래스 및 하위 클래스의 계층 구조와 함께 타입 캐스팅을 사용하여 특정 클래스 인스턴스의 타입을 확인하고 해당 인스턴스를 동일한 계층 내의 다른 클래스로 캐스팅할 수 있습니다. 타입캐스팅 예시에서 사용하기 위한 아래의 세 가지 코드 조각은 클래스의 계층과 해당 클래스의 인스턴스를 포함하는 배열을 정의합니다. 

*The first snippet defines a new base class called `MediaItem`. This class provides basic functionality for any kind of item that appears in a digital media library. Specifically, it declares a `name` property of type `String`, and an `init name` initializer. (It’s assumed that all media items, including all movies and songs, will have a name.)*

첫 번째 조각은 `MediaItem`이라는 새로운 기본 클래스를 정의합니다. 이 클래스는 디지털 미디어 라이브러리에 나타나는 모든 종류의 항목에 대한 기본 기능을 제공합니다. 구체적으로 `String` 타입의 `name` 프로퍼티와 `init name` 이니셜라이저를 선언합니다. (모든 영화와 노래를 포함한 모든 미디어 항목에 이름이 있을 것으로 가정됩니다

```swift
class MediaItem {
    var name: String
    init(name: String) {
        self.name = name
    }
}
```

*The next snippet defines two subclasses of `MediaItem`. The first subclass, `Movie`, encapsulates additional information about a movie or film. It adds a `director` property on top of the base `MediaItem` class, with a corresponding initializer. The second subclass, `Song`, adds an `artist` property and initializer on top of the base class:*

다음 조각은 `MediaItem`의 두 하위 클래스를 정의합니다. 첫 번째 서브클래스인 `Movie`는 영화나 필름에 대한 추가 정보를 담고 있습니다. 기본 `MediaItem` 클래스 위에 해당 이니셜라이저를 사용하여 `director` 프로퍼티를 추가합니다. 두 번째 하위 클래스인 `Song`은 기본 클래스 위에 `artist` 프로퍼티와 이니셜라이저를 추가합니다:

```swift
class Movie: MediaItem {
    var director: String
    init(name: String, director: String) {
        self.director = director
        super.init(name: name)
    }
}

class Song: MediaItem {
    var artist: String
    init(name: String, artist: String) {
        self.artist = artist
        super.init(name: name)
    }
}
```

*The final snippet creates a constant array called `library`, which contains two `Movie` instances and three `Song` instances. The type of the `library` array is inferred by initializing it with the contents of an array literal. Swift’s type checker is able to deduce that `Movie` and `Song` have a common superclass of `MediaItem`, and so it infers a type of `[MediaItem]` for the `library` array:*

마지막 스니펫은 두 개의 `Movie` 인스턴스와 세 개의 `Song` 인스턴스를 포함하는 `library`라는 상수 배열을 만듭니다. `library` 배열의 타입은 배열 리터럴의 내용으로 초기화하여 추론합니다. Swift의 유형 검사기는 `Movie`와 `Song`이 공통적으로 `MediaItem`이라는 슈퍼 클래스를 가지고 있다고 추론할 수 있으므로 `library` 배열에 대한 `[MediaItem]`의 타입을 추론할 수 있습니다:

```swift
let library = [
    Movie(name: "Casablanca", director: "Michael Curtiz"),
    Song(name: "Blue Suede Shoes", artist: "Elvis Presley"),
    Movie(name: "Citizen Kane", director: "Orson Welles"),
    Song(name: "The One And Only", artist: "Chesney Hawkes"),
    Song(name: "Never Gonna Give You Up", artist: "Rick Astley")
]
// the type of "library" is inferred to be [MediaItem]
```

*The items stored in `library` are still `Movie` and `Song` instances behind the scenes. However, if you iterate over the contents of this array, the items you receive back are typed as `MediaItem`, and not as `Movie` or `Song`. In order to work with them as their native type, you need to check their type, or downcast them to a different type, as described below.*

`library`에 저장된 항목은 뒤에서는 여전히 `Movie`와 `Song`인스턴스 입니다. 그러나 이 배열의 내용을 반복할 경우 반환되는 항목은 `Movie`나 `Song`이 아닌 `MediaItem`으로 입력됩니다. 원시 타입으로 작업하려면 아래 설명된 대로 타입을 확인하거나 다른 타입으로 다운캐스트해야 합니다.


