## *Preventing Overrides*

*You can prevent a method, property, or subscript from being overridden by marking it as final. Do this by writing the `final` modifier before the method, property, or subscript’s introducer keyword (such as `final var`, `final func`, `final class func`, and `final subscript`).*

*Any attempt to override a final method, property, or subscript in a subclass is reported as a compile-time error. Methods, properties, or subscripts that you add to a class in an extension can also be marked as final within the extension’s definition.*

*You can mark an entire class as final by writing the `final` modifier before the `class` keyword in its class definition (`final class`). Any attempt to subclass a final class is reported as a compile-time error.*


