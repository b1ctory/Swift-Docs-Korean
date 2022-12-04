## *Numeric Type Conversion : 숫자 타입 변환*

*Use the `Int` type for all general-purpose integer constants and variables in your code, even if they’re known to be nonnegative. Using the default integer type in everyday situations means that integer constants and variables are immediately interoperable in your code and will match the inferred type for integer literal values.*

코드의 모든 범용 목적의 정수형 상수 및 변수에 대해 음이 아닌 것으로 알려져 있더라도 Int 유형을 사용하세요. 일상적인 상황에서 기본 정수 유형을 사용하면 코드에서 정수형 상수와 변수를 즉시 상호 운용할 수 있으며 정수 리터럴 값에 대한 유추 타입과 일치합니다.



*Use other integer types only when they’re specifically needed for the task at hand, because of explicitly sized data from an external source, or for performance, memory usage, or other necessary optimization. Using explicitly sized types in these situations helps to catch any accidental value overflows and implicitly documents the nature of the data being used.*

외부 소스의 명시적인 크기의 데이터 혹은 성능, 메모리 사용량 또는 기타 필요한 최적화를 위해 필요한 경우에만 다른 정수 타입을 사용하세요. 이런 상황에서 명시적으로 크기가 지정된 유형을 사용하면 돌발적인 값 오버플로우를 파악하는데 도움이 되며 사용 중인 데이터의 특성을 암시적으로 문서화할 수 있습니다.



### *Integer Conversion : 정수 변환*

*The range of numbers that can be stored in an integer constant or variable is different for each numeric type. An `Int8` constant or variable can store numbers between `-128` and `127`, whereas a `UInt8` constant or variable can store numbers between `0` and `255`. A number that won’t fit into a constant or variable of a sized integer type is reported as an error when your code is compiled:*

정수형 상수 혹은 변수에 저장할 수 있는 숫자의 범위는 각각의 숫자 타입마다 다릅니다. Int8 상수 혹은 변수는 -128 부터 127 사이의 숫자를 저장할 수 있지만 UInt8 상수 혹은 변수는 0과 255 사이의 숫자를 저장할 수 있습니다. 크기가 큰 정수 타입의 상수나 변수에 맞지 않는 숫자는 코드를 컴파일할 때 오류로 보고됩니다.

```swift
let cannotBeNegative: UInt8 = -1
// UInt8 can't store negative numbers, and so this will report an error
let tooBig: Int8 = Int8.max + 1
// Int8 can't store a number larger than its maximum value,
// and so this will also report an error
```

*Because each numeric type can store a different range of values, you must opt in to numeric type conversion on a case-by-case basis. This opt-in approach prevents hidden conversion errors and helps make type conversion intentions explicit in your code.*

각각의 숫자 타입은 서로 다른 범위의 값을 저장할 수 있으므로 사례별로 숫자 타입 변환을 선택해야 합니다. 이 옵트인 방식은 숨겨진 변환 오류를 예방하고 코드에 타입 변환 의도를 명시하도록 도와줍니다.



*To convert one specific number type to another, you initialize a new number of the desired type with the existing value. In the example below, the constant `twoThousand` is of type `UInt16`, whereas the constant `one` is of type `UInt8`. They can’t be added together directly, because they’re not of the same type. Instead, this example calls `UInt16(one)` to create a new `UInt16` initialized with the value of `one`, and uses this value in place of the original:*

특정 숫자 타입을 다른 숫자 타입으로 변환하려면 타입의 새로운 숫자를 기존 값으로 초기화합니다. 아래의 예시에서 상수 twoThousand는 UInt16 타입인 반면 상수 one은 UInt8 타입이다. 같은 종류가 아니기 때문에 그들은 직접적으로 더해질 수 없습니다. 대신, 이 예시는 UInt16(one)을 호출하여 one의 값으로  초기화된 새 UInt16을 생성하고 원본 대신 이 값을 사용합니다.



```swift
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

*Because both sides of the addition are now of type `UInt16`, the addition is allowed. The output constant (`twoThousandAndOne`) is inferred to be of type `UInt16`, because it’s the sum of two `UInt16` values.*

이제 덧셈의 양쪽이 모두 UInt16 유형이기 때문에 덧셈이 허용됩니다. 출력 상수 (towThousandAndOne)는 두 개의 UInt16 값의 합이므로 UInt16 타입으로 추론됩니다.



*`SomeType(ofInitialValue)` is the default way to call the initializer of a Swift type and pass in an initial value. Behind the scenes, `UInt16` has an initializer that accepts a `UInt8` value, and so this initializer is used to make a new `UInt16` from an existing `UInt8`. You can’t pass in any type here, however—it has to be a type for which `UInt16` provides an initializer. Extending existing types to provide initializers that accept new types (including your own type definitions) is covered in [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html).*

일부 유형은 스위프트 타입의 이니셜라이저를 호출하여 초기 값을 전달하는 기본적인 방법입니다. 배경에는 UInt16이 UInt8 값을 받아들이든 이니셜라이저가 있으므로 이 이니셜라이저는 기존 UInt8에서 새로운 UInt16을 만드는데 사용됩니다. 그러나 여기서는 UInt16이 초기화를 제공하는 타입이어야 하기 때문에 어떠한 타입도 전달할 수 없습니다. 기존 타입을 확장하여 새 타입 (사용자 정의 타입을 포함하는)을 허용하는 초기화 프로그램을 제공하는 방법은 [링크] 에서 다루고 있습니다.



### *Integer and Floating-Point Conversion : 정수와 부동소수점 변환*

*Conversions between integer and floating-point numeric types must be made explicit:*

정수와 부동소수점 숫자 타입 간의 변환은 명확해야만 합니다.

```swift
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double
```

*Here, the value of the constant `three` is used to create a new value of type `Double`, so that both sides of the addition are of the same type. Without this conversion in place, the addition would not be allowed.*

여기서 상수 three의 값은 덧셈의 양쪽이 같은 타입이 되도록 Double 타입의 새로운 값을 만드는데 사용됩니다. 이 변환이 없으면 추가가 허용되지 않습니다.



*Floating-point to integer conversion must also be made explicit. An integer type can be initialized with a `Double` or `Float` value:*

부동 소수점에서 정수로의 변환도 명시적으로 해야합니다. 정수형은 Double  혹은 Float 값으로 초기화 할 수 있습니다 :

```swift
let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int
```

*Floating-point values are always truncated when used to initialize a new integer value in this way. This means that `4.75` becomes `4`, and `-3.9` becomes `-3`.*

이러한 방식으로 새 정수 값을 초기화할 때 부동소수점 값은 항상 잘립니다. 4.75는 4가 되고 -3.9는 -3이 된다는 뜻입니다.

> *NOTE*
> 
> *The rules for combining numeric constants and variables are different from the rules for numeric literals. The literal value `3` can be added directly to the literal value `0.14159`, because number literals don’t have an explicit type in and of themselves. Their type is inferred only at the point that they’re evaluated by the compiler.*
> 
> 숫자 상수와 변수를 결합하는 규칙은 숫자 리터럴에 대한 규칙과 다릅니다. 리터럴값 3은 리터럴값 0.14159에 직접 추가할 수 있는데, 이는 숫자 리터럴 자체에 명시적인 타입이 없기 때문입니다. 그들 타입은 컴파일러에 의해 평가되는 지점에서만 추론됩니다.


