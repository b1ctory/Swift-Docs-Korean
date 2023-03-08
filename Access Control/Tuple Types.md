### *Tuple Types : 튜플 타입*

*The access level for a tuple type is the most restrictive access level of all types used in that tuple. For example, if you compose a tuple from two different types, one with internal access and one with private access, the access level for that compound tuple type will be private.*

튜플 타입에 대한 액세스 레벨은 해당 튜플에 사용되는 모든 타입 중에서 가장 제한적인 액세스 레벨입니다. 예를 들어, 내부 액세스 권한이 있는 타입과 프라이빗 액세스 권한이 있는 타입의 두 가지 타입에서 튜플을 구성하는 경우 복합 튜플 타입의 액세스 수준은 프라이빗이 됩니다.

> *Note*
> 
> *Tuple types don’t have a standalone definition in the way that classes, structures, enumerations, and functions do. A tuple type’s access level is determined automatically from the types that make up the tuple type, and can’t be specified explicitly.*
> 
> 튜플 타입에는 클래스, 구조체, 열거형 및 함수와 같은 독립형 정의가 없습니다. 튜플 타입의 접근 레벨은 튜플 타입을 구성하는 타입에서 자동으로 결정되며 명시적으로 지정할 수 없습니다.
