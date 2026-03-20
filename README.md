# TIL (Today I Learned)

매일 학습하고 경험한 기술적 본질을 기록하는 공간입니다.
이 저장소의 모든 기록은 **AI 에이전트**를 통해 구조화되고 자동 정리됩니다.

"가짜는 기록하지 않는다"는 원칙 아래, 단순한 지식의 나열이 아닌 직접 실행하고 검증한 '진짜' 자산만을 남깁니다.

---

### 📂 지식 카테고리

<details>
  <summary style="font-size: 16px;"><strong id="n8n">n8n (전체 보기)</strong></summary>

- [2026-03-06-n8n-Slack-GitHub-TIL-자동화](n8n/2026-03-06-n8n-Slack-GitHub-TIL-자동화.md)

- [2026-03-06-n8n-Slack-멘션-정규식-제거](n8n/2026-03-06-n8n-Slack-멘션-정규식-제거.md)
  <!-- TODO: 여기에 인덱스를 추가하세요 -->
</details>
<br>

<details>
  <summary style="font-size: 16px;"><strong id="backend">Backend (전체 보기)</strong></summary>

- [2026-03-20-RESTful-API-설계-원칙](backend/2026-03-20-RESTful-API-설계-원칙.md)

- [2026-03-12-Spring-Cloud-Gateway-RedisRateLimiter-구현](backend/2026-03-12-Spring-Cloud-Gateway-RedisRateLimiter-구현.md)

- [2026-03-12-Spring-AI-RAG-품질-고도화-전략](backend/2026-03-12-Spring-AI-RAG-품질-고도화-전략.md)

- [2026-03-12-Spring-Boot-Redis-실무-활용-패턴](backend/2026-03-12-Spring-Boot-Redis-실무-활용-패턴.md)

- [2026-03-11-gRPC-마이크로서비스-통신-구축-전략](backend/2026-03-11-gRPC-마이크로서비스-통신-구축-전략.md)

- [2026-03-11-서비스-간-통신-프로토콜-비교](backend/2026-03-11-서비스-간-통신-프로토콜-비교.md)

- [2026-03-10-운영-환경을-위한-로그-전략-설계](backend/2026-03-10-운영-환경을-위한-로그-전략-설계.md)

- [2026-03-10-Spring-Boot-레이어드-vs-클린-아키텍처-비교](backend/2026-03-10-Spring-Boot-레이어드-vs-클린-아키텍처-비교.md)

- [2026-03-09-메시징-시스템과-웹플럭스-기술-비교](backend/2026-03-09-메시징-시스템과-웹플럭스-기술-비교.md)

- [2026-03-08-Offset-vs-Cursor-Pagination-비교](backend/2026-03-08-Offset-vs-Cursor-Pagination-비교.md)

- [2026-03-07-MSA-통신-전략-REST와-Kafka](backend/2026-03-07-MSA-통신-전략-REST와-Kafka.md)

- [2026-03-07-백엔드-성능-최적화-전략-비교](backend/2026-03-07-백엔드-성능-최적화-전략-비교.md)
  <!-- TODO: 여기에 인덱스를 추가하세요 -->
</details>
<br>

<details>
  <summary style="font-size: 16px;"><strong id="infra">Infrastructure (전체 보기)</strong></summary>

- [2026-03-11-Spring-Boot-Prometheus-Grafana-모니터링](infra/2026-03-11-Spring-Boot-Prometheus-Grafana-모니터링.md)

- [2026-03-07-Docker-Compose-기반-서비스-배포-및-Webhook-자동화](infra/2026-03-07-Docker-Compose-기반-서비스-배포-및-Webhook-자동화.md)
</details>
<br>

<details>
  <summary style="font-size: 16px;"><strong id="ai-agent">AI Agent (전체 보기)</strong></summary>

- [2026-03-16-클로드코드-스킬-구조-분석](ai-agent/2026-03-16-클로드코드-스킬-구조-분석.md)

- [2026-03-09-클로드코드-skills-활용-가이드](ai-agent/2026-03-09-클로드코드-skills-활용-가이드.md)
  <!-- TODO: 여기에 인덱스를 추가하세요 -->
</details>

---

### 🛠 작성 및 관리 규칙

일관성 있는 지식 자산화를 위해 다음 규칙을 엄수하며, AI 에이전트가 이를 바탕으로 문서를 생성합니다.

**명명 규칙 (Naming)**

- 형식: `YYYY-MM-DD-제목.md`
- 모든 공백은 하이픈(`-`)으로 대체하며 특수문자는 사용하지 않습니다.
- 예시: `2026-01-30-Clawdbot-프롬프트-최적화-전략.md`

**디렉토리 구조**

- `n8n/`: 워크플로우 설계 및 노드 활용 전략
- `backend/`: 서버 개발 및 데이터 처리 관련 학습 기록 (Java, Python, Database, API 등)
- `infra/`: 서버 환경 구성, 네트워크, 배포 및 운영 인프라 관련 기술 기록 (Docker, Webhook, CI/CD, Cloud 등)
- `ai-agent/`: LLM 프롬프트 설계 및 에이전트 구축

**문서 내부 양식**

- **Context**: 해결하고자 하는 문제 또는 학습 배경
- **Core**: 실제 작동하는 코드 스니펫이나 워크플로우 로직
- **Insight**: 실행 결과 확인 및 기술적 견해 (검증 데이터 포함)

---

### 🚀 AI Automation

이 저장소는 Human-in-the-Loop 모델이 적용된 n8n 기반 **AI 워크플로우**로 운영됩니다.

1. 메모 감지: 파편화된 학습 내용을 AI 에이전트가 감지합니다.

2. 지능형 정제: AI가 기술적 사실 관계를 검증하고, 표준화된 Markdown 형식으로 문서 초안을 작성합니다.

3. 인간 검토 (Human Review): 제가 초안의 내용을 직접 검토하고 수정하여 기록의 '진실성'과 '정확성'을 최종 승인합니다.

4. 자동 기록: 승인이 완료된 문서만 GitHub에 자동 커밋되며, 본 README의 인덱스가 업데이트됩니다.

단순한 기록을 넘어 학습의 질을 높이는 '기록의 지능화'를 지향합니다.
