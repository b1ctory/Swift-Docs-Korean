# *Subscripts : 서브스크립트*

*Classes, structures, and enumerations can define subscripts, which are shortcuts for accessing the member elements of a collection, list, or sequence. You use subscripts to set and retrieve values by index without needing separate methods for setting and retrieval. For example, you access elements in an `Array` instance as `someArray[index]` and elements in a `Dictionary` instance as `someDictionary[key]`.*

클래스, 구조체 및 열거형은 컬렉션, 리스트 또는 시퀀스의 멤버 요소에 액세스하기 위한 바로 가기인 첨자를 정의할 수 있습니다. 서브스크립트를 사용하여 별도의 설정 및 검색 방법 없이 인덱스별로 값을 설정하고 검색할 수 있습니다. 예를 들어 `Array` 인스턴스의 요소는 `someArray[index]`로 액세스하고 `Dictionary` 인스턴스의 요소는 `someDictionary[key]`로 액세스합니다.

*You can define multiple subscripts for a single type, and the appropriate subscript overload to use is selected based on the type of index value you pass to the subscript. Subscripts aren’t limited to a single dimension, and you can define subscripts with multiple input parameters to suit your custom type’s needs.*

하나의 타입에 대해 여러 개의 서브스크립트를 정의할 수 있으며, 서브스크립트에 전달하는 인덱스 값의 유형에 따라 사용할 적절한 서브스크립트 오버로드가 선택됩니다. 서브스크립트는 단일 차원으로 제한되지 않으며 사용자 정의 타입의 필요에 따라 여러 입력 매개 변수를 사용하여 첨자를 정의할 수 있습니다.


