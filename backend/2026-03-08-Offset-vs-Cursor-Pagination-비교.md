### Context
웹 API 개발 시 대용량 데이터를 효율적으로 조회하기 위한 페이지네이션(Pagination) 전략은 필수적입니다. 일반적으로 사용되는 Offset 방식과 성능 최적화를 위해 도입되는 Cursor 기반 방식을 비교하고 기술적 특성을 정리합니다.

### Core
* **Offset Pagination**
  * `LIMIT`과 `OFFSET` SQL 구문을 사용하여 구현합니다.
  * 예시: `SELECT * FROM posts ORDER BY created_at DESC LIMIT 10 OFFSET 100;`
  * 동작 방식: 지정된 OFFSET만큼 레코드를 건너뛰고 LIMIT만큼 데이터를 가져옵니다.

* **Cursor (Keyset) Pagination**
  * 특정 컬럼(보통 고유한 인덱스, ID 또는 타임스탬프)의 마지막 값을 '커서'로 사용합니다.
  * 예시: `SELECT * FROM posts WHERE created_at < '2026-03-08 10:00:00' ORDER BY created_at DESC LIMIT 10;`
  * 동작 방식: 이전 조회 결과의 마지막 요소를 기준으로 그 이후(또는 이전) 데이터만 스캔합니다.

### Insight
* **Offset Pagination**은 특정 페이지로 즉시 이동(예: 50페이지로 이동)할 수 있다는 장점이 있으나, `OFFSET` 값이 커질수록 DB는 건너뛰어야 할 데이터까지 모두 읽어야 하므로 성능이 급격히 저하됩니다(Deep Paging 문제).
* **Cursor Pagination**은 고유 키를 사용하여 바로 탐색하므로 데이터셋 크기에 상관없이 일정한 성능(O(1) 혹은 O(log N))을 보장합니다. 다만, 특정 페이지로 바로 점프하는 기능은 구현하기 어렵고 정렬 기준이 고유해야 한다는 제약이 있습니다.
* 실무에서는 데이터의 일관성과 성능을 고려하여 무한 스크롤(Infinite Scroll) 환경에서는 Cursor 방식을, 특정 페이지 접근이 중요한 UI에서는 Offset 방식을 선택합니다.

**출처:** [Pagination: Offset vs. Cursor](https://use-the-index-luke.com/no-offset), [Efficient Pagination in SQL](https://www.postgresql.org/docs/current/queries-limit.html)