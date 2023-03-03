# *Memory Safety*

*Structure your code to avoid conflicts when accessing memory.*

*By default, Swift prevents unsafe behavior from happening in your code. For example, Swift ensures that variables are initialized before they’re used, memory isn’t accessed after it’s been deallocated, and array indices are checked for out-of-bounds errors.*

*Swift also makes sure that multiple accesses to the same area of memory don’t conflict, by requiring code that modifies a location in memory to have exclusive access to that memory. Because Swift manages memory automatically, most of the time you don’t have to think about accessing memory at all. However, it’s important to understand where potential conflicts can occur, so you can avoid writing code that has conflicting access to memory. If your code does contain conflicts, you’ll get a compile-time or runtime error.*
