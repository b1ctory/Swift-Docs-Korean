## *Naming Type Parameters*

*In most cases, type parameters have descriptive names, such as `Key` and `Value` in `Dictionary<Key, Value>` and `Element` in `Array<Element>`, which tells the reader about the relationship between the type parameter and the generic type or function it’s used in. However, when there isn’t a meaningful relationship between them, it’s traditional to name them using single letters such as `T`, `U`, and `V`, such as `T` in the `swapTwoValues(_:_:)` function above.*

*Note*

*Always give type parameters upper camel case names (such as `T` and `MyTypeParameter`) to indicate that they’re a placeholder for a type, not a value.*


