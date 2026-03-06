### Context
n8n을 활용하여 Slack 메시지를 트리거(Trigger)로 받아 AI 에이전트가 내용을 가공하고, 이를 GitHub 저장소에 자동으로 기록하는 TIL(Today I Learned) 자동화 파이프라인을 구축함. 수동으로 관리하던 기술 기록 과정을 자동화하여 문서화 효율을 극대화하고자 함.

### Core
워크플로우는 다음과 같은 노드 구성으로 이루어짐.

* Slack Trigger: 특정 채널의 메시지 이벤트를 감지.
* AI Agent Node: 수신된 텍스트를 분석하여 지정된 TIL 마크다운(Markdown) 포맷으로 변환(데이터 구조화).
* GitHub Node: 변환된 내용을 `.md` 파일로 변환하여 지정된 저장소에 Push.
* Edit Fields (또는 Code Node): `README.md` 내부에 생성된 파일 인덱스를 업데이트하는 로직 수행.
* Slack Node: 전체 프로세스 종료 후 처리 결과를 사용자에게 알림으로 전송.

```json
{
  "workflow_description": "Slack to GitHub TIL Automation",
  "steps": [
    "Slack Trigger (Event: new_message)",
    "AI Agent (Prompt: Convert input to TIL format)",
    "GitHub (Operation: create_file)",
    "Code/Edit Fields (Logic: Update README index)",
    "Slack (Action: send_message)"
  ]
}
```

### Insight
n8n 활용의 핵심은 각 노드의 Input/Output 데이터 구조(Data Structure)를 명확히 이해하는 것임. 노드 간 전달되는 JSON 객체의 스키마를 파악하면 데이터 매핑 과정에서 발생하는 오류를 줄일 수 있음. 특히 AI Agent 노드를 중간에 배치함으로써 비정형 데이터를 구조화된 문서로 변환하는 자동화 수준을 높일 수 있었으며, 향후 루틴한 반복 작업을 워크플로우로 지속적으로 확장할 예정임.

**출처:** [n8n Docs - Workflows and Nodes](https://docs.n8n.io/getting-started/key-concepts/)