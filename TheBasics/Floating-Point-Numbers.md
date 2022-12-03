## *Floating-Point Numbers : 부동 소숫점 숫자*

*Floating-point numbers are numbers with a fractional component, such as `3.14159`, `0.1`, and `-273.15`.*

부동 소숫점 숫자는 3.14159, 0.1 그리고 -273.15 같이 분수 성분이 있는 숫자이다.

*Floating-point types can represent a much wider range of values than integer types, and can store numbers that are much larger or smaller than can be stored in an `Int`. Swift provides two signed floating-point number types:*

부동소수점형은 정수형보다 훨씬 넓은 범위의 값을 나타낼 수 있으며, Int에 저장할 수 있는 것보다 훨씬 크거나 작은 숫자를 저장할 수 있습니다. 스위프트는 두가지의 부동소수점 숫자 타입을 제공합니다.

- *`Double` represents a 64-bit floating-point number.*
  
  - Double은 64비트 부동소수점 숫자를 나타냅니다.

- *`Float` represents a 32-bit floating-point* *number.*
  
  - Float은 32비트 부동소숫점 숫자를 나타냅니다.

> *NOTE*
> 
> *`Double` has a precision of at least 15 decimal digits, whereas the precision of `Float` can be as little as 6 decimal digits. The appropriate floating-point type to use depends on the nature and range of values you need to work with in your code. In situations where either type would be appropriate, `Double` is preferred.*
> 
> Double은 소수점 이하 15자리, Float은 소수점 이하 6자리의 정확성을 가집니다. 사용할 적절한 부동소수점 유형은 코드 내에서 작업해야 하는 값의 트겅과 범위에 달려있습니다. 두 가지 유형 중 하나가 적합한 상황에서는 Double이 선호됩니다.
