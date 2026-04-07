### Context
분산 시스템 아키텍처를 설계할 때 메시지 브로커(Message Broker) 선택은 매우 중요하다. 특히 RabbitMQ와 Apache Kafka는 가장 대중적으로 사용되는 도구이나, 설계 철학과 작동 방식에서 극명한 차이를 보인다. 어떤 상황에서 무엇을 선택해야 할지 기술적 의사결정 기준을 정리한다.

### Core
* RabbitMQ (메시지 지향 미들웨어, MOM)
  * 구조: 스마트 브로커/덤 컨슈머 모델. 브로커가 메시지 라우팅 로직(Exchange, Queue, Binding)을 처리한다.
  * 특징: 복잡한 라우팅 규칙(Routing Key, Header, Topic) 지원. 메시지 전달 보장과 즉각적인 배달에 최적화되어 있다.
  * 코드 스니펫 (Python Pika 예시):
```python
# RabbitMQ 메시지 발행 (직접 라우팅)
channel.basic_publish(exchange='logs', routing_key='error', body='Critical Error!')
```

* Apache Kafka (분산 이벤트 스트리밍 플랫폼)
  * 구조: 덤 브로커/스마트 컨슈머 모델. 브로커는 데이터 저장(Append-only log)만 담당하며, 컨슈머가 처리 위치(Offset)를 관리한다.
  * 특징: 높은 처리량(Throughput), 데이터 영속성(Persistence), 리플레이 가능성. 이벤트 소싱 및 실시간 데이터 스트리밍에 적합하다.
  * 코드 스니펫 (Python Kafka-python 예시):
```python
# Kafka 메시지 발행
producer.send('user-events', value={'user_id': 123, 'action': 'login'})
```

### Insight
* 선정 전략
  * RabbitMQ: 복잡한 라우팅이 필요하거나, 애플리케이션 간의 작업 단위 비동기 처리가 필요할 때 사용한다. 트랜잭션 보장이 중요하거나 서비스 간 결합도를 낮추는 용도에 적합하다.
  * Kafka: 대용량 로그 수집, 이벤트 스트리밍, 실시간 데이터 분석(Data Pipeline)이 필요할 때 사용한다. 데이터의 보존 기간이 길고 여러 컨슈머가 동일한 데이터를 여러 번 읽어야 하는 경우 Kafka가 압도적이다.
* 기술적 팁
  * 지연 시간(Latency)이 매우 중요한 실시간 알림 서비스라면 RabbitMQ가 유리하다.
  * 처리량(Throughput)이 중요하고 데이터 유실 없이 대규모 분석이 필요하다면 Kafka를 선택하라.
  * Kafka는 운영 난이도(Zookeeper/KRaft 관리 등)가 높으므로 규모에 맞는 도구를 선정하는 것이 비용 효율적이다.

**출처:** [RabbitMQ vs Kafka: Which to Choose?](https://www.rabbitmq.com/blog/2023/09/22/rabbitmq-vs-kafka), [Apache Kafka Documentation](https://kafka.apache.org/documentation/)