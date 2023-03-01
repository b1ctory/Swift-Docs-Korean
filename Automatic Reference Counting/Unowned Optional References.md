### *Unowned Optional References : 미소유 옵셔널 참조*

*You can mark an optional reference to a class as unowned. In terms of the ARC ownership model, an unowned optional reference and a weak reference can both be used in the same contexts. The difference is that when you use an unowned optional reference, you’re responsible for making sure it always refers to a valid object or is set to `nil`.*

클래스에 대한 옵셔널 참조를 미소유로 표시할 수 있습니다. ARC 소유권 모델 측면에서 미소유 옵셔널 참조와 약한 참조는 모두 동일한 컨텍스트에서 사용될 수 있습니다. 차이점은 미소유 옵셔널 참조를 사용할 때 항상 유효한 개체를 참조하거나 `nil`로 설정되어 있는지 확인해야 한다는 것입니다.

*Here’s an example that keeps track of the courses offered by a particular department at a school:*

다음은 학교의 특정 부서에서 제공하는 과정을 추적하는 예입니다.

```swift
class Department {
    var name: String
    var courses: [Course]
    init(name: String) {
        self.name = name
        self.courses = []
    }
}

class Course {
    var name: String
    unowned var department: Department
    unowned var nextCourse: Course?
    init(name: String, in department: Department) {
        self.name = name
        self.department = department
        self.nextCourse = nil
    }
}
```

*`Department` maintains a strong reference to each course that the department offers. In the ARC ownership model, a department owns its courses. `Course` has two unowned references, one to the department and one to the next course a student should take; a course doesn’t own either of these objects. Every course is part of some department so the `department` property isn’t an optional. However, because some courses don’t have a recommended follow-on course, the `nextCourse` property is an optional.*

`Department`는 학과에서 제공하는 각 과정에 대한 강력한 참조를 유지합니다. ARC 소유권 모델에서 부서는 해당 과정을 소유합니다. `Course`에는 두 개의 미소유 참조가 있습니다. 하나는 부서에 대한 것이고 다른 하나는 학생이 수강해야 하는 다음 과정에 대한 것입니다. 과정은 이러한 객체를 소유하지 않습니다. 모든 과정은 일부 부서의 일부이므로 `department` 프로퍼티는 옵셔널이 아닙니다. 그러나 일부 과정에는 권장 후속 과정이 없으므로 `nextCourse` 프로퍼티는 선택 사항입니다.

*Here’s an example of using these classes:*

다음은 이러한 클래스를 사용하는 예입니다.

```swift
let department = Department(name: "Horticulture")

let intro = Course(name: "Survey of Plants", in: department)
let intermediate = Course(name: "Growing Common Herbs", in: department)
let advanced = Course(name: "Caring for Tropical Plants", in: department)

intro.nextCourse = intermediate
intermediate.nextCourse = advanced
department.courses = [intro, intermediate, advanced]
```

*The code above creates a department and its three courses. The intro and intermediate courses both have a suggested next course stored in their `nextCourse` property, which maintains an unowned optional reference to the course a student should take after completing this one.*

위의 코드는 부서와 세 개의 과정을 생성합니다. 입문 과정과 중급 과정 모두 `nextCourse` 프로퍼티에 저장된  다음 추천 과정이 있으며, 이 프로퍼티는 학생이 이 과정을 완료한 후 수강해야 하는 과정에 대한 미소유 옵셔널 참조를 유지합니다.

*![](https://docs.swift.org/swift-book/images/unownedOptionalReference@2x.png)*

*An unowned optional reference doesn’t keep a strong hold on the instance of the class that it wraps, and so it doesn’t prevent ARC from deallocating the instance. It behaves the same as an unowned reference does under ARC, except that an unowned optional reference can be `nil`.*

소유되지 않은 옵셔널 참조는 래핑하는 클래스의 인스턴스를 강력하게 유지하지 않으므로 ARC가 인스턴스 할당을 해제하는 것을 막지 않습니다. 미소유 옵셔널 참조가 `nil`일 수 있다는 점을 제외하면 ARC에서 소유되지 않은 참조와 동일하게 작동합니다.

*Like non-optional unowned references, you’re responsible for ensuring that `nextCourse` always refers to a course that hasn’t been deallocated. In this case, for example, when you delete a course from `department.courses` you also need to remove any references to it that other courses might have.*

옵셔널이 아닌 미소유 참조와 마찬가지로 `nextCourse`가 항상 할당 취소되지 않은 과정을 참조하도록 해야 합니다. 이 경우 예를 들어 `department.courses`에서 과정을 삭제할 때 다른 과정에서 포함할 수 있는 모든 참조도 제거해야 합니다.

> *Note*
> 
> *The underlying type of an optional value is `Optional`, which is an enumeration in the Swift standard library. However, optionals are an exception to the rule that value types can’t be marked with `unowned`.*
> 
> 옵셔널 값의 기본 타입은 Swift 표준 라이브러리의 열거형인 `Optional`입니다. 그러나 옵셔널은 값 타입이 `unowned`로 표시될 수 없다는 규칙의 예외입니다.
> 
> *The optional that wraps the class doesn’t use reference counting, so you don’t need to maintain a strong reference to the optional.*
> 
> 클래스를 래핑하는 옵셔널은 레퍼런스 카운트를 사용하지 않으므로 옵셔널에 대한 강력한 참조를 유지할 필요가 없습니다.


