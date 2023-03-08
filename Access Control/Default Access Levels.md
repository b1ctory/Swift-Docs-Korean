### *Default Access Levels : 기본 엑세스 레벨*

*All entities in your code (with a few specific exceptions, as described later in this chapter) have a default access level of internal if you don’t specify an explicit access level yourself. As a result, in many cases you don’t need to specify an explicit access level in your code.*

직접 명시적 액세스 레벨을 지정하지 않은 경우 코드의 모든 엔티티(이 장의 뒷부분에 설명된 몇 가지 특정 예외 제외)는 기본 액세스 레벨이 내부입니다. 따라서 대부분의 경우 코드에 명시적인 액세스 수준을 지정할 필요가 없습니다.

### *Access Levels for Single-Target Apps : 단일 타겟 애플리케이션의 액세스 수준*

*When you write a simple single-target app, the code in your app is typically self-contained within the app and doesn’t need to be made available outside of the app’s module. The default access level of internal already matches this requirement. Therefore, you don’t need to specify a custom access level. You may, however, want to mark some parts of your code as file private or private in order to hide their implementation details from other code within the app’s module.*

단순 단일 타겟 앱을 작성할 때, 앱의 코드는 일반적으로 앱 내에 자체 포함되어 있으므로 앱 모듈 외부에서 사용할 필요가 없습니다. 내부의 기본 액세스 레벨이 이미 이 요구 사항과 일치합니다. 따라서 사용자 정의 접근 단계를 지정할 필요가 없습니다. 그러나 앱 모듈 내의 다른 코드로부터 구현 세부 정보를 숨기기 위해 코드의 일부를 파일 프라이빗 혹은 프라이빗으로 표시할 수 있습니다.

### *Access Levels for Frameworks : 프레임워크에 대한 엑세스 레벨*

*When you develop a framework, mark the public-facing interface to that framework as open or public so that it can be viewed and accessed by other modules, such as an app that imports the framework. This public-facing interface is the application programming interface (or API) for the framework.*

프레임워크를 개발할 때는 프레임워크를 가져오는 앱과 같은 다른 모듈에서 보고 액세스할 수 있도록 해당 프레임워크에 대한 공용 인터페이스를 열림 또는 퍼블릭으로 표시하십시오. 이 공용 인터페이스는 프레임워크를 위한 API(애플리케이션 프로그래밍 인터페이스)입니다.

> *Note*
> 
> *Any internal implementation details of your framework can still use the default access level of internal, or can be marked as private or file private if you want to hide them from other parts of the framework’s internal code. You need to mark an entity as open or public only if you want it to become part of your framework’s API.*
> 
> 프레임워크의 내부 구현 세부 정보는 여전히 내부의 기본 액세스 수준을 사용할 수 있으며, 프레임워크 내부 코드의 다른 부분으로부터 숨기려면 프라이빗 또는 파일 프라이빗으로 표시할 수 있습니다. 엔티티를 프레임워크 API의 일부로 지정하려는 경우에만 공개 또는 공개로 표시해야 합니다.

### *Access Levels for Unit Test Targets : 장치 테스트 대상에 대한 액세스 레벨*

*When you write an app with a unit test target, the code in your app needs to be made available to that module in order to be tested. By default, only entities marked as open or public are accessible to other modules. However, a unit test target can access any internal entity, if you mark the import declaration for a product module with the `@testable` attribute and compile that product module with testing enabled.*

유닛 테스트 타겟을 사용하여 앱을 작성할 때 테스트를 위해 해당 모듈에서 앱의 코드를 사용할 수 있어야 합니다. 기본적으로 열려 있거나 공용으로 표시된 엔티티만 다른 모듈에 액세스할 수 있습니다. 그러나 제품 모듈에 대한 import 선언을 `@testable` 프로퍼티로 표시하고 테스트가 활성화된 상태에서 해당 제품 모듈을 컴파일하면 장치 테스트 대상이 모든 내부 엔티티에 액세스할 수 있습니다.
