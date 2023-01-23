# *Optional Chaining : 옵셔널 체이닝*

*Optional chaining is a process for querying and calling properties, methods, and subscripts on an optional that might currently be `nil`. If the optional contains a value, the property, method, or subscript call succeeds; if the optional is `nil`, the property, method, or subscript call returns `nil`. Multiple queries can be chained together, and the entire chain fails gracefully if any link in the chain is `nil`.*

옵셔널 체이닝은 현재 `nil`일 수 있는 옵셔널에서 프로퍼티, 메서드 및 서브스크립트를 쿼리하고 호출하는 프로세스입니다. 옵셔널에 값이 포함되어 있으면 프로퍼티, 메서드 또는 서브스크립트 호출이 성공하고, 옵셔널이 `nil`이면 프로퍼티, 메서드 또는 서브스크립트 호출이 `nil`을 반환합니다. 여러 쿼리를 함께 연결할 수 있으며 체인의 링크가 `nil`이면 전체 체인이 정상적으로 실패합니다.

> *NOTE*
> 
> *Optional chaining in Swift is similar to messaging `nil` in Objective-C, but in a way that works for any type, and that can be checked for success or failure.*
> 
> Swift의 옵셔널 체이닝은 Objective-C의 메세징 `nil`과 비슷하지만 모든 타입에 적용되며 성공 여부를 확인할 수 있습니다.


