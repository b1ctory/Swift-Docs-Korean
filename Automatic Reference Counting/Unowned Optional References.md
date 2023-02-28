### *Unowned Optional References*

*You can mark an optional reference to a class as unowned. In terms of the ARC ownership model, an unowned optional reference and a weak reference can both be used in the same contexts. The difference is that when you use an unowned optional reference, you’re responsible for making sure it always refers to a valid object or is set to `nil`.*

*Here’s an example that keeps track of the courses offered by a particular department at a school:*

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

*Here’s an example of using these classes:*

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

*![](https://docs.swift.org/swift-book/images/unownedOptionalReference@2x.png)*

*An unowned optional reference doesn’t keep a strong hold on the instance of the class that it wraps, and so it doesn’t prevent ARC from deallocating the instance. It behaves the same as an unowned reference does under ARC, except that an unowned optional reference can be `nil`.*

*Like non-optional unowned references, you’re responsible for ensuring that `nextCourse` always refers to a course that hasn’t been deallocated. In this case, for example, when you delete a course from `department.courses` you also need to remove any references to it that other courses might have.*

> *Note*
> 
> *The underlying type of an optional value is `Optional`, which is an enumeration in the Swift standard library. However, optionals are an exception to the rule that value types can’t be marked with `unowned`.*
> 
> *The optional that wraps the class doesn’t use reference counting, so you don’t need to maintain a strong reference to the optional.*
