## *Integers : 정수*

*Integers are whole numbers with no fractional component, such as `42` and `-23`. Integers are either signed (positive, zero, or negative) or unsigned (positive or zero).*

정수는 42나 -23처럼 분수 성분이 없는 완전한 숫자입니다. 정수는 부호가 있거나 (양수, 0, 음수) 부호가 없습니다. (양수, 0) 

*Swift provides signed and unsigned integers in 8, 16, 32, and 64 bit forms. These integers follow a naming convention similar to C, in that an 8-bit unsigned integer is of type `UInt8`,and a 32-bit signed integer is of type `Int32`. Like all types in Swift, these integer types have capitalized names.*

스위프트는 8, 16, 32 그리고 64비트의 부호 있는 정수와 부호 없는 정수를 제공합니다. 이 정수들은 8비트의 부호 없는 정수가 UInt8 형식이고 32비트의 부호 있는 정수는 Int32 형식이라는 점에서 C언어의 네이밍 컨벤션과 비슷합니다. Swift에서 모든 형식과 마찬가지로, 이런 정수형도 대문자로 된 이름을 가집니다.



### *Integer Bounds : 정수 경계*

*You can access the minimum and maximum values of each integer type with its `min` and `max` properties:*

각 정수 유형의 최소값과 최대값에 엑세스할 수 있는 속성은 min과 max 입니다.

```swift
let minValue = UInt8.min // minValue is equal to 0, and is of type UInt8
let maxValue = UInt8.max // maxValue is equal to 255, and is of type UInt8
```

*The values of these properties are of the appropriate-sized number type (such as `UInt8` in the example above) and can therefore be used in expressions alongside other values of the same type.*

이러한 속성의 값은 적절한 크기의 숫자 (위의 예시에서 UInt8 같은) 이므로 동일한 유형의 다른 값과 함께 식을 사용할 수 있습니다.



### *Int : 정수*

*In most cases, you don’t need to pick a specific size of integer to use in your code. Swift provides an additional integer type, `Int`, which has the same size as the current platform’s native word size:*

대부분의 경우, 코드에 사용할 특정 크기의 정수를 선택할 필요가 없습니다. 스위프트는 현재 플랫폼의 네이티브 글자 사이즈와 동일한 크기의 정수형 Int를 추가적으로 제공합니다. 

- *On a 32-bit platform, `UInt` is the same size as `UInt32`.*
  
  - 32비트 플랫폼에서 UInt는 UInt32와 같은 사이즈입니다.

- *On a 64-bit platform, `UInt` is the same size as `UInt64`.*
  
  - 64비트 플랫폼에서 UInt는 UInt64와 같은 사이즈입니다.

*Unless you need to work with a specific size of integer, always use `Int` for integer values in your code. This aids code consistency and interoperability. Even on 32-bit platforms, `Int` can store any value between `-2,147,483,648` and `2,147,483,647`, and is large enough for many integer ranges.*

특정 크기의 상수로 작업할 필요가 없는 경우 코드의 정수 값에는 항상 Int를 사용하세요. 이를 통해 코드의 일관성과 상호운용성이 향상됩니다. 32비트 플랫폼에서도 Int는  `-2,147,483,648` 와 `2,147,483,647` 사이의 값을 저장할 수 있으며 이는 충분히 큰 정수 범위입니다.



### *UInt*

*Swift also provides an unsigned integer type, `UInt`, which has the same size as the current platform’s native word size:*

스위프트는 또한 현재 플랫폼의 네이티브 글자 사이즈와 동일한 부호가 없는 정수 타입 UInt를 제공합니다.

- *On a 32-bit platform, `UInt` is the same size as `UInt32`.*
  
  - 32비트 플랫폼에서 UInt는 UInt32와 같은 사이즈입니다.

- *On a 64-bit platform, `UInt` is the same size as `UInt64`.*
  
  - 64비트 플랫폼에서 UInt는 UInt64와 같은 사이즈입니다.

> *NOTE*
> 
> *Use `UInt` only when you specifically need an unsigned integer type with the same size as the platform’s native word size. If this isn’t the case, `Int` is preferred, even when the values to be stored are known to be nonnegative. A consistent use of `Int` for integer values aids code interoperability, avoids the need to convert between different number types, and matches integer type inference, as described in [Type Safety and Type Inference](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID322).*
> 
> 플랫폼의 네이티브 글자 크기와 동일한 크기의 부호 없는 정수형이 특별하게 필요한 경우에만 UInt를 사용하세요. 그렇지 않으면 저장할 값이 음수가 아니더라도 Int가 더 선호(?) 됩니다. 정수값에 Int를 일관되게 사용하면 코드 상호 운용성을 돕고, 다른 숫자 유형 간에 변환할 필요가 없으며, (링크)에 설명된 것 처럼 정수 유형 추론과 일치합니다.


