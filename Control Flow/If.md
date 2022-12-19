### *If*

*In its simplest form, the `if` statement has a single `if` condition. It executes a set of statements only if that condition is `true`.*

가장 간단한 형태로 `if`문은 `if` 조건을 하나씩 가집니다. 조건이 true인 경우에만 구문 집합을 실행합니다.

```swift
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
}
// Prints "It's very cold. Consider wearing a scarf."
```

*The example above checks whether the temperature is less than or equal to 32 degrees Fahrenheit (the freezing point of water). If it is, a message is printed. Otherwise, no message is printed, and code execution continues after the `if` statement’s closing brace.*

위의 예제는 온도가 화씨 32도 (물의 어는점) 이하인지 여부를 확인합니다. 그렇다면 메세지가 출력됩니다. 그렇지 않으면 메세지가 출력되지 않으며 `if` 문의 닫힘 괄호 후에도 코드 실행이 계속됩니다.

*The `if` statement can provide an alternative set of statements, known as an else clause, for situations when the `if` condition is `false`. These statements are indicated by the `else` keyword.*

`if`문은 `if` 조건이 `false`인 상황에 대해 else 절로 알려진 일련의 진술을 제공할 수 있습니다. 이러한 문장은 `else` 키워드로 표시됩니다.

```swift
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// Prints "It's not that cold. Wear a t-shirt."
```

*One of these two branches is always executed. Because the temperature has increased to `40` degrees Fahrenheit, it’s no longer cold enough to advise wearing a scarf and so the `else` branch is triggered instead.*

이 두 분기 중 하나는 항상 실행됩니다. 기온이 화씨 40도까지 올라 스카프 착용을 권할 정도로 춥지 않아 `else` 브랜치가 대신 발동됩니다.

*You can chain multiple `if` statements together to consider additional clauses.*

여러개의 `if` 문을 연결해서 추가 절을 고려할 수 있습니다.

```swift
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// Prints "It's really warm. Don't forget to wear sunscreen."
```

*Here, an additional `if` statement was added to respond to particularly warm temperatures. The final `else` clause remains, and it prints a response for any temperatures that are neither too warm nor too cold.*

여기에 특히 따뜻한 온도에 대응하기 위해 추가적인 `if` 문구가 추가되었습니다. 마지막 `else` 조항이 남아있으며 너무 덥지도 춥지도 않은 온도에 대한 응답을 출력합니다.

*The final `else` clause is optional, however, and can be excluded if the set of conditions doesn’t need to be complete.*

그러나 마지막 `else` 절은 선택 사항이며, 조건 집합이 완전할 필요가 없는 경우에는 제외할 수 있습니다.

```swift
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
}
```

*Because the temperature is neither too cold nor too warm to trigger the `if` or `else if` conditions, no message is printed.*

온도가 너무 춥지도 않고 너무 따뜻하지도 않기 때문에 `if`나 `else if` 조건이 실행되지 않고, 메세지가 출력되지 않습니다.
