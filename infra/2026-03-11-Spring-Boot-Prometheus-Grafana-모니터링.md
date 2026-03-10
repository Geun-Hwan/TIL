### Context
분산 환경의 마이크로서비스 아키텍처(MSA)에서 애플리케이션의 상태를 실시간으로 추적하고 성능 병목을 탐지하는 것은 필수적입니다. Spring Boot 기반 환경에서 시스템 메트릭과 비즈니스 지표를 효율적으로 수집, 저장, 시각화하기 위해 Prometheus와 Grafana 조합을 표준적으로 사용합니다.

### Core
Spring Boot 애플리케이션에 Micrometer를 통합하여 Prometheus로 메트릭을 노출하는 설정은 다음과 같습니다.

* **의존성 추가 (build.gradle)**
```gradle
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-actuator'
    implementation 'io.micrometer:micrometer-registry-prometheus'
}
```

* **설정 파일 (application.yml)**
```yaml
management:
  endpoints:
    web:
      exposure:
        include: prometheus, health, info
  metrics:
    tags:
      application: ${spring.application.name}
```

* **아키텍처 흐름**
1. Spring Boot Actuator가 Micrometer를 통해 애플리케이션 메트릭을 노출
2. Prometheus 서버가 `/actuator/prometheus` 엔드포인트를 주기적으로 Pulling(데이터 수집)
3. Grafana가 Prometheus를 데이터 소스(Data Source)로 지정하여 쿼리(PromQL)를 실행 및 시각화

### Insight
Prometheus는 시계열 데이터(Time-series data) 저장에 최적화된 엔진이며, Grafana는 이를 바탕으로 운영자가 직관적으로 시스템 상태를 파악할 수 있는 대시보드를 제공합니다. 실무에서는 JVM 메모리 사용량, HTTP 요청 처리 시간(Latency), 에러율 등을 주요 지표로 추적합니다. 특히 Prometheus의 Pull 방식은 대상 서버가 증가해도 데이터 수집 부하를 중앙 서버에서 제어할 수 있는 장점이 있으나, 짧은 주기의 이벤트 수집에는 신중한 설계가 필요합니다.

**출처:** [Spring Boot Actuator: Production-ready features](https://docs.spring.io/spring-boot/reference/actuator/index.html), [Prometheus Overview](https://prometheus.io/docs/introduction/overview/)