# *Collection Types*

*Swift provides three primary collection types, known as arrays, sets, and dictionaries, for storing collections of values. Arrays are ordered collections of values. Sets are unordered collections of unique values. Dictionaries are unordered collections of key-value associations.*

*![](https://docs.swift.org/swift-book/_images/CollectionTypes_intro_2x.png)*

*Arrays, sets, and dictionaries in Swift are always clear about the types of values and keys that they can store. This means that you can’t insert a value of the wrong type into a collection by mistake. It also means you can be confident about the type of values you will retrieve from a collection.*

> *NOTE*
> 
> *Swift’s array, set, and dictionary types are implemented as generic collections. For more about generic types and collections, see [Generics](https://docs.swift.org/swift-book/LanguageGuide/Generics.html).*

## *Mutability of Collections*

*If you create an array, a set, or a dictionary, and assign it to a variable, the collection that’s created will be mutable. This means that you can change (or mutate) the collection after it’s created by adding, removing, or changing items in the collection. If you assign an array, a set, or a dictionary to a constant, that collection is immutable, and its size and contents can’t be changed.*

> *NOTE*
> 
> *It’s good practice to create immutable collections in all cases where the collection doesn’t need to change. Doing so makes it easier for you to reason about your code and enables the Swift compiler to optimize the performance of the collections you create.*
