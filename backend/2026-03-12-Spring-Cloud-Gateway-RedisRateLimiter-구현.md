### Context
서버의 인증, 인가, 라우팅 로직을 수행하기 전, 특정 IP에서 유입되는 과도한 요청(브루트 포스, DDoS 등)을 조기에 차단하여 리소스를 보호할 필요가 있습니다. Spring Cloud Gateway(SCG)는 요청이 애플리케이션의 핵심 비즈니스 로직에 도달하기 전에 Rate Limiting(속도 제한)을 적용하여 이러한 요청을 효과적으로 필터링할 수 있습니다.

### Core
Spring Cloud Gateway에서 가장 권장되는 방식은 Redis 기반의 `RedisRateLimiter`를 사용하는 것입니다. 이는 토큰 버킷(Token Bucket) 알고리즘을 기반으로 요청량을 제어합니다.

* 의존성 설정 (build.gradle)
```groovy
implementation 'org.springframework.cloud:spring-cloud-starter-gateway'
implementation 'org.springframework.boot:spring-boot-starter-data-redis-reactive'
```

* 설정 (application.yml)
```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: request-ratelimiting-route
          uri: lb://service-name
          predicates:
            - Path=/api/**
          filters:
            - name: RequestRateLimiter
              args:
                redis-rate-limiter.replenishRate: 10 # 초당 허용 요청 수
                redis-rate-limiter.burstCapacity: 20 # 순간 허용 가능한 최대 버스트 요청 수
                key-resolver: "#{@remoteAddrKeyResolver}" # IP 기반 식별
```

* 키 추출 전략 구현 (Java)
```java
@Configuration
public class RateLimiterConfig {
    @Bean
    public KeyResolver remoteAddrKeyResolver() {
        return exchange -> Mono.just(exchange.getRequest().getRemoteAddress().getAddress().getHostAddress());
    }
}
```

### Insight
* Rate Limiting은 기술적 방어선 중 가장 앞단에 위치해야 합니다. SCG는 비차단(Non-blocking) 방식으로 동작하므로 Redis와의 통신 오버헤드를 최소화하면서 높은 성능을 유지합니다.
* `replenishRate`와 `burstCapacity`를 서비스 특성에 맞게 조정하는 것이 핵심입니다. 일반적인 API라면 작게, 데이터 전송이 빈번한 API라면 버스트 용량을 크게 설정해야 합니다.
* 운영 환경에서는 `RedisRateLimiter`가 Redis 연결 장애 시 요청을 어떻게 처리할지(fail-open/fail-closed) 정책을 결정해야 합니다. 기본적으로는 허용하는 정책을 따르지만, 보안이 중요하다면 커스텀 `RateLimiter`를 구현해야 할 수도 있습니다.

**출처:** [Spring Cloud Gateway Reference Documentation](https://docs.spring.io/spring-cloud-gateway/reference/spring-cloud-gateway/requestratelimiter-gatewayfilter-factory.html)