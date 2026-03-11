### Context
Spring Boot 환경에서 Redis는 단순 캐싱(Caching)을 넘어 시스템의 고가용성과 데이터 일관성을 보장하기 위한 핵심 미들웨어로 활용됩니다. 분산 환경에서 발생할 수 있는 데이터 정합성 문제, 트래픽 제어, 실시간 데이터 처리 등을 해결하기 위해 Redis의 다양한 자료구조와 기능을 실무에 적용하는 방법을 정리합니다.

### Core
* 분산 락 (Distributed Lock): 여러 서버 인스턴스가 동일 자원에 접근할 때 동시성 제어를 위해 Redisson의 RLock을 사용합니다.
  ```java
  RLock lock = redissonClient.getLock("resourceKey");
  try {
      if (lock.tryLock(10, 2, TimeUnit.SECONDS)) {
          // 비즈니스 로직 수행
      }
  } finally {
      lock.unlock();
  }
  ```

* 레이트 리미팅 (Rate Limiting): Redis의 원자적 카운터(Atomic Counter)를 이용해 API 요청 제한을 구현합니다.
  ```java
  // Redis INCR을 사용하여 호출 횟수 증가 및 만료 시간 설정
  Long count = redisTemplate.opsForValue().increment(key);
  if (count == 1) redisTemplate.expire(key, 1, TimeUnit.MINUTES);
  ```

* 랭킹 시스템 (Ranking System): Sorted Set(ZSET)의 스코어 기능을 활용하여 실시간 순위를 관리합니다.
  ```java
  // 사용자 점수 업데이트 및 1위부터 10위 조회
  redisTemplate.opsForZSet().add("leaderboard", "userId", 95.5);
  Set<ZSetOperations.TypedTuple<String>> topRank = redisTemplate.opsForZSet().reverseRangeWithScores("leaderboard", 0, 9);
  ```

* Pub/Sub 및 Stream: 마이크로서비스 간 비동기 메시지 통신을 처리합니다.
  ```java
  // 메시지 발행
  redisTemplate.convertAndSend("topicName", "messagePayload");
  ```

### Insight
Redis는 메모리 기반 저장소로서 매우 빠른 응답 속도를 제공하므로, 분산 시스템에서의 트랜잭션 오버헤드를 최소화할 수 있습니다. 특히 분산 락 사용 시 데드락(Deadlock) 발생을 방지하기 위해 반드시 TTL(Time-To-Live)을 설정하는 것이 중요합니다. 랭킹 시스템의 경우 데이터셋이 커질수록 메모리 점유율을 고려해야 하며, 메시지 처리 시 데이터 유실 방지가 중요하다면 단순 Pub/Sub 대신 메시지 영속성이 보장되는 Redis Stream 도입을 권장합니다.

**출처:** [Redisson Documentation](https://redisson.org/), [Spring Data Redis Reference](https://docs.spring.io/spring-data/redis/reference/index.html)