### Context
REST(Representational State Transfer)는 웹의 기존 프로토콜인 HTTP를 기반으로 자원을 정의하고 자원 간의 주소를 지정하는 방법론입니다. RESTful API는 이러한 REST 아키텍처 스타일의 설계 원칙을 준수하여 구현된 API를 의미합니다.

### Core
RESTful 설계를 위한 주요 구성 요소는 다음과 같습니다.

* 자원(Resource): URI로 식별되는 모든 데이터 (예: /users/1)
* 행위(Verb): HTTP 메서드를 사용하여 자원에 대한 행위를 정의
    * GET: 자원 조회
    * POST: 자원 생성
    * PUT/PATCH: 자원 수정
    * DELETE: 자원 삭제
* 표현(Representation): 서버가 클라이언트에 응답하는 데이터 형식 (주로 JSON 또는 XML)

```http
# 사용자 조회
GET /api/v1/users/123

# 사용자 생성
POST /api/v1/users
Content-Type: application/json

{
  "name": "홍길동",
  "email": "hong@example.com"
}
```

### Insight
RESTful API의 핵심은 '자원 중심'의 설계입니다. 다음 원칙을 준수할 때 비로소 RESTful하다고 할 수 있습니다.

* 무상태성(Statelessness): 각 요청은 독립적이며 서버는 클라이언트의 상태를 저장하지 않음
* 계층화(Layered System): 클라이언트는 대상 서버가 직접 연결된 것인지 중간 서버를 거쳤는지 알 수 없음
* 균일한 인터페이스(Uniform Interface): URI를 통해 자원을 명확히 지정하고 HTTP 표준 메서드를 사용함

주의점으로는 모든 API를 반드시 RESTful하게 설계할 필요는 없다는 점입니다. 데이터 간 복잡한 관계나 실시간 스트리밍이 필요할 때는 GraphQL이나 gRPC가 더 효율적일 수 있습니다. 또한, URI에 동사를 포함하는 습관(예: /api/getUser)은 REST 철학에 반하므로 명사 위주의 자원 중심 설계가 필수적입니다.

**출처:** [REST API Tutorial](https://restfulapi.net/), [MDN Web Docs - REST](https://developer.mozilla.org/en-US/docs/Glossary/REST)