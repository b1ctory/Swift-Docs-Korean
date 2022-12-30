## *Associated Values : 관련값*

*The examples in the previous section show how the cases of an enumeration are a defined (and typed) value in their own right. You can set a constant or variable to `Planet.earth`, and check for this value later. However, it’s sometimes useful to be able to store values of other types alongside these case values. This additional information is called an associated value, and it varies each time you use that case as a value in your code.*

이전 섹션의 예는 열거형의 경우 자체적으로 정의된 값 (그리고 타입) 이 어떻게 되는지 보여줍니다. 상수 혹은 변수를 `Planet.earth` 로 설정하고 나중에 이 값을 확인할 수 있습니다. 그러나 이러한 경우 값과 함께 다른 타입의 값을 저장할 수 있는 것이 유용할 수 있습니다. 이 추가 정보를 관련된 값이라고 하며 코드에서 값으로 사용할 때마다 다릅니다.

*You can define Swift enumerations to store associated values of any given type, and the value types can be different for each case of the enumeration if needed. Enumerations similar to these are known as discriminated unions, tagged unions, or variants in other programming languages.*

지정된 타입의 관련 값을 저장하도록 Swift 열거형을 정의할 수 있으며, 필요한 경우 열거의 케이스마다 값 타입이 다를 수 있습니다. 이와 유사한 열거형을 다른 프로그래밍 언어에서는 구분 결합, 태그 결합 혹은 변형이라고 합니다.

*For example, suppose an inventory tracking system needs to track products by two different types of barcode. Some products are labeled with 1D barcodes in UPC format, which uses the numbers `0` to `9`. Each barcode has a number system digit, followed by five manufacturer code digits and five product code digits. These are followed by a check digit to verify that the code has been scanned correctly:*

예를 들어, 재고 추적 시스템에서 두가지 바코드 유형 별로 제품을 추적해야 한다고 가정합니다. 일부 제품에는 UPC 형식의 1D 바코드가 부착되어 있으며 숫자 `0`에서 `9`를 사용합니다. 각 바코드에는 번호 시스템 숫자와 제조업체 코드 숫자 5개, 제품 코드 숫자 5개가 있습니다. 다음은 코드가 올바르게 스캔되었는지 확인하기 위한 체크 숫자입니다.

*![](https://docs.swift.org/swift-book/_images/barcode_UPC_2x.png)*

*Other products are labeled with 2D barcodes in QR code format, which can use any ISO 8859-1 character and can encode a string up to 2,953 characters long:*

다른 제품에는 QR코드 형식의 2D 바코드가 부착되어있으며, `ISO 8859-1` 문자를 사용할 수 있으며 최대 2,953자의 문자열을 인코딩할 수 있습니다.

*![](https://docs.swift.org/swift-book/_images/barcode_QR_2x.png)*

*It’s convenient for an inventory tracking system to store UPC barcodes as a tuple of four integers, and QR code barcodes as a string of any length.*

UPC 바코드를 4개의 정수로 이루어진 튜플로 저장하고 QR 코드 바코드를 임의의 길이의 문자열로 저장하면 편리합니다.

*In Swift, an enumeration to define product barcodes of either type might look like this:*

Swift에서 두가지 타입의 제품 바코드를 정의하는 열거형은 다음과 같습니다.

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```

*This can be read as:*

이것은 이렇게 읽힐 수 있습니다.

*“Define an enumeration type called `Barcode`, which can take either a value of `upc` with an associated value of type (`Int`, `Int`, `Int`, `Int`), or a value of `qrCode` with an associated value of type `String`.”*

"연관된 값 (`Int`, `Int`, `Int`, `Int`) 또는 연관된 값이 `String`인 `qrCode` 값을 사용할 수 있는 `Barcode`라는 열거형을 정의합니다."

*This definition doesn’t provide any actual `Int` or `String` values—it just defines the type of associated values that `Barcode` constants and variables can store when they’re equal to `Barcode.upc` or `Barcode.qrCode`.*

이 정의는 실제 `Int` 혹은 `String`값을 제공하지 않으며, `Barcode.upc` 혹은 `Barcode.qrCode`와 같을 때 `Barcode` 상수 및 변수가 저장할 수 있는 관련 값의 타입을 지정할 뿐입니다.

*You can then create new barcodes using either type:*

그런 다음 타입 중 하나를 사용해서 바코드를 생성할 수 있습니다.

```swift
var productBarcode = Barcode.upc(8, 85909, 51226, 3)
```

*This example creates a new variable called `productBarcode` and assigns it a value of `Barcode.upc` with an associated tuple value of `(8, 85909, 51226, 3)`.*

이 예에서는 `productBarcode`라는 새 변수를 생성하고 관련 튜플 값이 `(8,85909,51226,3)`인 `Barcode.upc` 값을 할당합니다.

*You can assign the same product a different type of barcode:*

같은 제품에 다른 타입의 바코드를 할당할 수 있습니다.

```swift
productBarcode = .qrCode("ABCDEFGHIJKLMNOP")
```

*At this point, the original `Barcode.upc` and its integer values are replaced by the new `Barcode.qrCode` and its string value. Constants and variables of type `Barcode` can store either a `.upc` or a `.qrCode` (together with their associated values), but they can store only one of them at any given time.*

이 때 원래의 `Barcode.upc`의 해당 정수 값이 새로운 `Barcode.qrCode`와 해당 문자열 값으로 대체됩니다. 바코드 타입의 상수 및 변수는 `.upc` 혹은 `.qrCode` (관련 값과 함께)를 저장할 수 있지만, 주어진 시간에 하나만 저장할 수 있습니다.

*You can check the different barcode types using a switch statement, similar to the example in [Matching Enumeration Values with a Switch Statement](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html#ID147). This time, however, the associated values are extracted as part of the switch statement. You extract each associated value as a constant (with the `let` prefix) or a variable (with the `var` prefix) for use within the `switch` case’s body:*

[링크]의 예와 마찬가지로 switch 문을 사용해서 다양한 바코드 유형을 확인할 수 있습니다. 그러나 이번에는 관련 값이 `Switch` 문의 일부로 추출됩니다. 각 관련 값을 `switch` 케이스의 본문 내에서 사용할 상수 (`let` 접두사와 함께) 혹은 변수 (`var` 접두사와 함께)로 추출합니다.

```swift
switch productBarcode {
case .upc(let numberSystem, let manufacturer, let product, let check):
    print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
case .qrCode(let productCode):
    print("QR code: \(productCode).")
}
// Prints "QR code: ABCDEFGHIJKLMNOP."
```

*If all of the associated values for an enumeration case are extracted as constants, or if all are extracted as variables, you can place a single `var` or `let` annotation before the case name, for brevity:*

열거형 사례에 대한 모든 관련 값이 상수로 추출되거나 변수로 추출되는 경우, 케이스 이름 옆에 단일 `var` 혹은 `let` 주석을 배치하여 간략화할 수 있습니다.

```swift
switch productBarcode {
case let .upc(numberSystem, manufacturer, product, check):
    print("UPC : \(numberSystem), \(manufacturer), \(product), \(check).")
case let .qrCode(productCode):
    print("QR code: \(productCode).")
}
// Prints "QR code: ABCDEFGHIJKLMNOP."
```
