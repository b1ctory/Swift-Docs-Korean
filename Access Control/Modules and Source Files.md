## *Modules and Source Files*

*Swift’s access control model is based on the concept of modules and source files.*

*A module is a single unit of code distribution — a framework or application that’s built and shipped as a single unit and that can be imported by another module with Swift’s `import` keyword.*

*Each build target (such as an app bundle or framework) in Xcode is treated as a separate module in Swift. If you group together aspects of your app’s code as a stand-alone framework — perhaps to encapsulate and reuse that code across multiple applications — then everything you define within that framework will be part of a separate module when it’s imported and used within an app, or when it’s used within another framework.*

*A source file is a single Swift source code file within a module (in effect, a single file within an app or framework). Although it’s common to define individual types in separate source files, a single source file can contain definitions for multiple types, functions, and so on.*
