## *Required Initializers : 필수 이니셜라이저*

*Write the `required` modifier before the definition of a class initializer to indicate that every subclass of the class must implement that initializer:*

클래스의 모든 하위 클래스가 해당 이니셜라이저를 구현해야 함을 나타내기 위해 클래스 이니셜라이저 정의 앞에 `required` 수식자를 작성합니다:

```swift
class SomeClass {
    required init() {
        // initializer implementation goes here
    }
}
```

*You must also write the `required` modifier before every subclass implementation of a required initializer, to indicate that the initializer requirement applies to further subclasses in the chain. You don’t write the `override` modifier when overriding a required designated initializer:*

또한 필수 이니셜라이저의 모든 하위 클래스 구현 전에 `required` 수식어를 작성하여 이니셜라이저 요구 사항이 체인의 추가 하위 클래스에 적용됨을 표시해야 합니다. 필수 지정된 초기화기를 재정의할 때는 `override` 수식어를 쓰지 않습니다:

```swift
class SomeSubclass: SomeClass {
    required init() {
        // subclass implementation of the required initializer goes here
    }
}
```

> *NOTE*
> 
> *You don’t have to provide an explicit implementation of a required initializer if you can satisfy the requirement with an inherited initializer.*
> 
> 상속된 이니셜라이저로 요구 사항을 충족할 수 있다면 필요한 이니셜라이저의 명시적인 구현을 제공할 필요가 없습니다.
