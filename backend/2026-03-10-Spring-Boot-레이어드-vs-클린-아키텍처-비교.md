### Context
Spring Boot 프로젝트를 설계할 때 전통적인 레이어드 아키텍처(Layered Architecture)와 로버트 C. 마틴이 제안한 클린 아키텍처(Clean Architecture) 사이에서 어떤 구조를 선택할지 고민하는 경우가 많습니다. 두 아키텍처의 핵심 차이와 의존성 관리 원칙을 정리합니다.

### Core
* 레이어드 아키텍처(Layered Architecture)
  * 구조: 보통 Controller - Service - Repository의 3계층으로 구성됩니다.
  * 의존성 방향: 하향식(Top-down) 의존 구조를 가집니다. Controller -> Service -> Repository 순으로 데이터 흐름이 고정되어 있습니다.
  * 특징: 구현이 단순하고 직관적이지만, 데이터베이스(DB) 변경이 비즈니스 로직에 영향을 주기 쉽습니다.

* 클린 아키텍처(Clean Architecture)
  * 구조: 중심에 엔티티(Entity)와 유스케이스(Use Case)를 두고, 외부 계층(프레임워크, DB, UI)이 이를 감싸는 원형 구조입니다.
  * 의존성 방향: 의존성 역전 원칙(DIP, Dependency Inversion Principle)을 적용하여, 항상 안쪽으로만 의존하도록 설계합니다. 내부 계층은 외부 계층에 대해 전혀 알지 못합니다.
  * 특징: 특정 프레임워크나 데이터베이스 기술로부터 비즈니스 로직을 완벽하게 격리합니다.

### Insight
레이어드 아키텍처는 초기 개발 속도가 빠르고 학습 곡선이 낮다는 장점이 있으나, 프로젝트 규모가 커질수록 데이터베이스 의존성이 비즈니스 로직까지 침범하여 유지보수가 어려워질 수 있습니다. 반면 클린 아키텍처는 초기 설정이 복잡하고 보일러플레이트(Boilerplate) 코드가 늘어나는 단점이 있지만, 테스트 용이성과 기술 변경에 대한 유연성이 매우 높습니다. 

* 기술적 견해: 소규모 프로토타입이나 단순 CRUD 앱은 레이어드 아키텍처가 효율적이며, 복잡한 비즈니스 로직을 장기간 유지보수해야 하는 엔터프라이즈급 서비스라면 클린 아키텍처 도입을 적극 고려해야 합니다.

**출처:** [Clean Architecture Overview](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html), [Dependency Inversion Principle](https://www.baeldung.com/solid-principles)