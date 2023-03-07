## *Modules and Source Files : 모듈 및 소스 파일*

*Swift’s access control model is based on the concept of modules and source files.*

Swift의 접근 제어 모델은 모듈 및 소스 파일의 개념을 기반으로 합니다.

*A module is a single unit of code distribution — a framework or application that’s built and shipped as a single unit and that can be imported by another module with Swift’s `import` keyword.*

모듈은 코드 배포의 단일 단위입니다. 단일 단위로 빌드 및 배송되고 Swift의 `import` 키워드를 사용하여 다른 모듈에서 가져올 수 있는 프레임워크 또는 애플리케이션입니다.

*Each build target (such as an app bundle or framework) in Xcode is treated as a separate module in Swift. If you group together aspects of your app’s code as a stand-alone framework — perhaps to encapsulate and reuse that code across multiple applications — then everything you define within that framework will be part of a separate module when it’s imported and used within an app, or when it’s used within another framework.*

Xcode의 각 빌드 대상(예: 앱 번들 또는 프레임워크)은 Swift에서 별도의 모듈로 처리됩니다. 앱 코드의 여러 측면을 독립 실행형 프레임워크로 그룹화하면(아마도 여러 애플리케이션에서 해당 코드를 캡슐화하고 재사용하기 위해) 해당 프레임워크 내에서 정의하는 모든 것이 앱 내에서 가져와 사용될 때 또는 다른 프레임워크 내에서 사용될 때 별도 모듈의 일부가 됩니다. 

*A source file is a single Swift source code file within a module (in effect, a single file within an app or framework). Although it’s common to define individual types in separate source files, a single source file can contain definitions for multiple types, functions, and so on.*

소스 파일은 모듈 내의 단일 Swift 소스 코드 파일입니다(사실상 앱 또는 프레임워크 내의 단일 파일). 별도의 소스 파일에서 개별 타입을 정의하는 것이 일반적이지만 단일 소스 파일에는 여러 타입, 함수 등에 대한 정의가 포함될 수 있습니다.
