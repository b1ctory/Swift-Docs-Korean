## *Associated Values*

*The examples in the previous section show how the cases of an enumeration are a defined (and typed) value in their own right. You can set a constant or variable to `Planet.earth`, and check for this value later. However, it’s sometimes useful to be able to store values of other types alongside these case values. This additional information is called an associated value, and it varies each time you use that case as a value in your code.*

*You can define Swift enumerations to store associated values of any given type, and the value types can be different for each case of the enumeration if needed. Enumerations similar to these are known as discriminated unions, tagged unions, or variants in other programming languages.*

*For example, suppose an inventory tracking system needs to track products by two different types of barcode. Some products are labeled with 1D barcodes in UPC format, which uses the numbers `0` to `9`. Each barcode has a number system digit, followed by five manufacturer code digits and five product code digits. These are followed by a check digit to verify that the code has been scanned correctly:*

*![](https://docs.swift.org/swift-book/_images/barcode_UPC_2x.png)*

*Other products are labeled with 2D barcodes in QR code format, which can use any ISO 8859-1 character and can encode a string up to 2,953 characters long:*

*![](https://docs.swift.org/swift-book/_images/barcode_QR_2x.png)*

*It’s convenient for an inventory tracking system to store UPC barcodes as a tuple of four integers, and QR code barcodes as a string of any length.*

*In Swift, an enumeration to define product barcodes of either type might look like this:*

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```

*This can be read as:*

*“Define an enumeration type called `Barcode`, which can take either a value of `upc` with an associated value of type (`Int`, `Int`, `Int`, `Int`), or a value of `qrCode` with an associated value of type `String`.”*

*This definition doesn’t provide any actual `Int` or `String` values—it just defines the type of associated values that `Barcode` constants and variables can store when they’re equal to `Barcode.upc` or `Barcode.qrCode`.*

*You can then create new barcodes using either type:*

```swift
var productBarcode = Barcode.upc(8, 85909, 51226, 3)
```

*This example creates a new variable called `productBarcode` and assigns it a value of `Barcode.upc` with an associated tuple value of `(8, 85909, 51226, 3)`.*

*You can assign the same product a different type of barcode:*

```swift
productBarcode = .qrCode("ABCDEFGHIJKLMNOP")
```

*At this point, the original `Barcode.upc` and its integer values are replaced by the new `Barcode.qrCode` and its string value. Constants and variables of type `Barcode` can store either a `.upc` or a `.qrCode` (together with their associated values), but they can store only one of them at any given time.*

*You can check the different barcode types using a switch statement, similar to the example in [Matching Enumeration Values with a Switch Statement](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html#ID147). This time, however, the associated values are extracted as part of the switch statement. You extract each associated value as a constant (with the `let` prefix) or a variable (with the `var` prefix) for use within the `switch` case’s body:*

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

```swift
switch productBarcode {
case let .upc(numberSystem, manufacturer, product, check):
    print("UPC : \(numberSystem), \(manufacturer), \(product), \(check).")
case let .qrCode(productCode):
    print("QR code: \(productCode).")
}
// Prints "QR code: ABCDEFGHIJKLMNOP."
```
