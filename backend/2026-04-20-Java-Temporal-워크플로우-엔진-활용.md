### Context
분산 시스템에서 복잡한 비즈니스 로직(예: 결제 처리, 데이터 동기화, 이메일 알림 시퀀스)을 수행할 때, 네트워크 오류나 서버 중단으로 인해 프로세스가 중간에 멈추면 데이터 불일치가 발생하기 쉽습니다. Temporal은 이러한 분산 워크플로우를 신뢰성 있게 실행하기 위한 워크플로우 오케스트레이션 엔진으로, 상태 유지(Stateful)와 내결함성(Fault-tolerance)을 보장합니다.

### Core
Temporal에서 워크플로우를 정의하려면 Workflow Interface와 구현체, 그리고 Activity Interface가 필요합니다.

*Workflow Interface 정의*
```java
@WorkflowInterface
public interface FileProcessingWorkflow {
    @WorkflowMethod
    void processFile(String fileId);
}
```

*Activity Interface 정의 (외부 호출, DB 등)*
```java
@ActivityInterface
public interface FileActivities {
    @ActivityMethod
    void downloadFile(String fileId);
    @ActivityMethod
    void uploadToCloud(String fileId);
}
```

*Workflow 구현 예시*
```java
public class FileProcessingWorkflowImpl implements FileProcessingWorkflow {
    private final FileActivities activities = Workflow.newActivityStub(FileActivities.class, ...);

    @Override
    public void processFile(String fileId) {
        activities.downloadFile(fileId);
        activities.uploadToCloud(fileId);
    }
}
```

### Insight
Temporal은 코드를 실행하는 동안 내부 상태를 지속적으로 기록(Event Sourcing)하므로, 서버가 재시작되어도 중단된 시점부터 정확히 재개할 수 있습니다. 

* 주요 특징
  * 내결함성(Fault-tolerance): 워크플로우 실행 도중 하드웨어 장애가 발생해도 워크플로우는 상태를 보존함.
  * 상태 지속성(Stateful): 장기 실행 프로세스(Long-running process)를 마치 일반적인 순차 프로그래밍처럼 작성 가능.
  * 가시성(Visibility): 진행 중인 모든 프로세스의 상태를 쿼리하고 추적 가능.

* 선정 기준
  * MSA 환경에서 여러 서비스 간의 일관성이 중요한 트랜잭션이 필요한 경우.
  * 복잡한 재시도(Retry) 로직과 타임아웃 처리가 워크플로우 전반에 걸쳐 필요한 경우.
  * 상태 추적이 불가능한 스파게티 형태의 비동기 메시지 기반 로직을 대체해야 할 때.

**출처:** [Temporal Java SDK Documentation](https://docs.temporal.io/java), [Temporal Introduction](https://docs.temporal.io/workflows)