## *Type Safety and Type Inference : 타입 안전 및 타입 추론*

*Swift is a type-safe language. A type safe language encourages you to be clear about the types of values your code can work with. If part of your code requires a `String`, you can’t pass it an `Int` by mistake.*

스위프트는 타입에 안전한 언어입니다. 타입에 안전한 언어를 사용하면 코드가 작동할 수 있는 값의 유형을 명확하게 파악할 수 있습니다. 코드의 일부에 String이 필요한 경우 실수로 Int를 전달할 수 없습니다.



*Because Swift is type safe, it performs type checks when compiling your code and flags any mismatched types as errors. This enables you to catch and fix errors as early as possible in the development process.*

Swift가 타입에 안전한 언어이기 때문에, 코드를 컴파일 할 때 유형 검사를 수행하고 일치하지 않는 유형을 오류로 플래그를 지정합니다. 이것은 개발 단계에서 되도록 빠르게 오류를 잡아내고 고치는 것을 가능하게 합니다.



*Type-checking helps you avoid errors when you’re working with different types of values. However, this doesn’t mean that you have to specify the type of every constant and variable that you declare. If you don’t specify the type of value you need, Swift uses type inference to work out the appropriate type. Type inference enables a compiler to deduce the type of a particular expression automatically when it compiles your code, simply by examining the values you provide.*

타입 검사는 다른 타입의 값으로 작업할 때 오류를 방지하는데 도움이 됩니다.그러나 이것은 선언하는 모든 상수나 변수의 타입을 지정해야 하는 것은 아닙니다.만약 필요한 값의 유형을 지정하지 않으면, Swift는 타입 추론을 사용하여 적절한 유형을 계산합니다. 타입 추론을 통해 코드를 컴파일할 때 단순히 제공하는 값을 검사함으로써 특정 표현식의 형식을 자동으로 추론할 수 있습니다.



*Because of type inference, Swift requires far fewer type declarations than languages such as C or Objective-C. Constants and variables are still explicitly typed, but much of the work of specifying their type is done for you.*

타입 추론 때문에 Swift는 C나 Objective-C와 같은 언어보다 훨씬 적은 타입 선언을 요구합니다. 상수와 변수는 여전히 타입을 명시하지만, 해당 유형을 지정하는 작업의 대부분은 사용자에 의해 수행됩니다.



*Type inference is particularly useful when you declare a constant or variable with an initial value. This is often done by assigning a literal value (or literal) to the constant or variable at the point that you declare it. (A literal value is a value that appears directly in your source code, such as `42` and `3.14159` in the examples below.)*

타입 추론은 상수 혹은 변수를 초기값으로 선언할 때 특히 유용합니다. 이것은 종종 당신이 선언하는 지점의 상수나 변수의 리터럴값 (혹은 리터럴)을 할당함으로써 이루어집니다. (리터럴 값은 아래의 예시에서 42와 3.14159와 같이 소스코드에 직접 나타나는 값입니다.)



*For example, if you assign a literal value of `42` to a new constant without saying what type it is, Swift infers that you want the constant to be an `Int`, because you have initialized it with a number that looks like an integer:*

예를 들면, 당신이 42라는 리터럴 값을 타입을 지정하지 않은 새로운 상수에 할당할 경우, 당신이 정수처럼 보이는 숫자로 값을 초기화했기 때문에 Swift는 당신이 상수가 Int 값이 되기를 원한다고 추론합니다.



```swift
let meaningOfLife = 42
// meaningOfLife is inferred to be of type Int
```

*Likewise, if you don’t specify a type for a floating-point literal, Swift infers that you want to create a `Double`:*

이와 마찬가지로 부동 소수점 리터럴에 대한 유형을 지정하지 않으면 Swift는 당신이 Double을 생성할 것임을 추론합니다.

```swift
let pi = 3.14159
// pi is inferred to be of type Double
```

*Swift always chooses `Double` (rather than `Float`) when inferring the type of floating-point numbers.*

Swift는 부동소수점 숫자를 추론할 때 항상 (Float 보다는) Double을 선택합니다

*If you combine integer and floating-point literals in an expression, a type of `Double` will be inferred from the context:*

만약 당신이 표현식에서 정수와 부동소수점 리터럴에 대한 타입을 지정하지 않으면 다음과 같은 맥락에서 Double 타입이 추론됩니다.

```swift
let anotherPi = 3 + 0.14159
// anotherPi is also inferred to be of type Double
```

*The literal value of `3` has no explicit type in and of itself, and so an appropriate output type of `Double` is inferred from the presence of a floating-point literal as part of the addition.*

3이라는 리터럴 값은 그 자체로 명시적인 타입을 가지고 있지 않으므로 적절한 출력 타입인 Double은 덧셈의 일부로서 부동소수점 리터럴의 존재로부터 추론됩니다.
