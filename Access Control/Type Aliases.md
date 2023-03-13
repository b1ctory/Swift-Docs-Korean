## *Type Aliases : 타입 별칭*

*Any type aliases you define are treated as distinct types for the purposes of access control. A type alias can have an access level less than or equal to the access level of the type it aliases. For example, a private type alias can alias a private, file-private, internal, public, or open type, but a public type alias can’t alias an internal, file-private, or private type.*

사용자가 정의한 모든 타입 별칭은 액세스 제어를 위해 별개의 타입으로 취급됩니다. 타입 별칭의 액세스 레벨은 별칭 타입의 액세스 레벨보다 작거나 같을 수 있습니다. 예를 들어 프라이빗 타입 별칭은 프라이빗, 파일-프라이빗, 내부, 퍼블릭 또는 열린 타입으로 별칭을 지정할 수 있지만 퍼블릭 타입 별칭은 내부, 파일-프라이빗 또는 프라이빗 타입으로 별칭을 지정할 수 없습니다.

> *Note*
> 
> *This rule also applies to type aliases for associated types used to satisfy protocol conformances.*
> 
>  이 규칙은 프로토콜 준수를 충족하는 데 사용되는 관련 타입의 타입 별칭에도 적용됩니다.


