### Context
웹 페이지의 성능은 사용자 경험(UX) 및 검색 엔진 최적화(SEO)와 직결됩니다. 이를 객관적으로 평가하고 개선하기 위해 구글에서 제공하는 도구인 Lighthouse와 성능 지표인 Core Web Vitals에 대해 이해하고 활용하는 것은 필수적입니다.

### Core
Lighthouse는 웹 페이지의 성능, 접근성, SEO 등을 종합적으로 진단하는 자동화 도구입니다. 이 도구는 내부적으로 웹의 핵심 사용자 경험 지표인 Core Web Vitals(CWV)를 측정합니다.

* 주요 Core Web Vitals 지표:
    * LCP (Largest Contentful Paint): 가장 큰 콘텐츠가 화면에 렌더링되기까지 걸리는 시간 (로드 성능)
    * INP (Interaction to Next Paint): 사용자의 상호작용 후 반응까지 걸리는 시간 (반응성)
    * CLS (Cumulative Layout Shift): 시각적 요소의 안정성 정도 (시각적 안정성)

* Lighthouse 사용법 (Chrome DevTools):
    * Chrome에서 평가하려는 페이지 접속
    * F12 (개발자 도구) 오픈
    * Lighthouse 탭으로 이동
    * 모드(Navigation/Timespan/Snapshot) 선택 후 페이지 로드 분석 실행

```bash
# Lighthouse CLI를 활용한 실행 예시
npm install -g lighthouse
lighthouse https://example.com --view
```

### Insight
Lighthouse는 실습 환경에서 성능을 측정하는 '실험실 데이터(Lab Data)'를 제공하며, Core Web Vitals는 실제 사용자의 데이터를 기반으로 하는 '현장 데이터(Field Data)'와 결합했을 때 가장 큰 시너지를 냅니다. Lighthouse에서 제공하는 제안사항을 하나씩 해결하는 것만으로도 웹 서비스의 성능을 비약적으로 높일 수 있으며, 이는 곧 구글 검색 결과 순위 향상으로 이어집니다.

**출처:** [Lighthouse Overview](https://developer.chrome.com/docs/lighthouse/overview), [Core Web Vitals](https://web.dev/articles/vitals)