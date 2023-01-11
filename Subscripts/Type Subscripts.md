## *Type Subscripts : 타입 서브스크립트*

*Instance subscripts, as described above, are subscripts that you call on an instance of a particular type. You can also define subscripts that are called on the type itself. This kind of subscript is called a type subscript. You indicate a type subscript by writing the `static` keyword before the `subscript` keyword. Classes can use the `class` keyword instead, to allow subclasses to override the superclass’s implementation of that subscript. The example below shows how you define and call a type subscript:*

인스턴스 서브스크립트는 위에서 설명한 대로 특정 타입의 인스턴스에서 호출하는 서브스크립트입니다. 타입 자체에서 호출되는 서브스크립트를 정의할 수도 있습니다. 이런 종류의 서브스크립트를 타입 서브스크립트라고 합니다. 서브스크립트 키워드 앞에 `static` 키워드를 입력하여 타입 서브스크립트를 나타냅니다. 클래스는 대신 `class` 키워드를 사용하여 하위 클래스가 해당 서브스크립트의 슈퍼클래스 구현을 재정의할 수 있습니다. 아래 예제에서는 타입 서브스크립트를 정의하고 호출하는 방법을 보여 줍니다:

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
    static subscript(n: Int) -> Planet {
        return Planet(rawValue: n)!
    }
}
let mars = Planet[4]
print(mars)
```
