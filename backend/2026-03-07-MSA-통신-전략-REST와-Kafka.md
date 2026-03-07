### Context
마이크로서비스 아키텍처(MSA) 환경에서 서비스 간 통신 방식의 선택은 시스템의 가용성과 결합도에 큰 영향을 미칩니다. 동기식 통신(REST)은 즉각적인 응답이 필요할 때 유리하지만, 장애 전파의 위험이 있습니다. 반면 비동기식 메시지 브로커(Kafka)는 높은 처리량과 결합도 분리에 탁월하지만, 복잡도가 증가합니다. 각 상황에 맞는 전략적 선택과 에러 처리 기준을 정리합니다.

### Core
* REST (Synchronous)
  * 구조: Request-Response 모델.
  * 특징: 구현이 단순하며, 즉각적인 결과 확인이 가능.
  * 에러 처리: 서킷 브레이커(Circuit Breaker) 패턴을 통해 장애 서비스와의 차단 및 재시도(Retry) 정책 적용.
* Kafka (Asynchronous)
  * 구조: Producer-Broker-Consumer 모델.
  * 특징: 높은 처리량과 결합도 최소화, 서비스 간 의존성 분리.
  * 에러 처리: DLQ(Dead Letter Queue)를 활용하여 처리에 실패한 메시지를 별도 적재하고, 이후 재처리하거나 분석하여 시스템 안정성 확보.

### Insight
MSA에서 REST는 서비스 간 의존성이 낮고 즉각적인 응답이 필수인 경우에 적합하며, Kafka는 대용량 트래픽 처리나 이벤트 기반의 비동기 작업이 필요한 환경에서 강력한 도구가 됩니다. 시스템의 안정성을 위해서는 REST 통신 시 서킷 브레이커를 통한 장애 전파 차단, Kafka 사용 시에는 DLQ를 통한 실패 메시지 관리 체계 구축이 필수적입니다.

**출처:** [Microservices Communication Patterns](https://microservices.io/patterns/communication-patterns.html), [Kafka Best Practices](https://kafka.apache.org/documentation/), [Resilience4j Circuit Breaker](https://resilience4j.readme.io/)