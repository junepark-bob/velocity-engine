# 구성 요소 (components)
> 자동 생성 (`kn index`). 직접 고치지 마세요. 항목 8개 · [갈래 목록](../index.md)

| ID | 제목 | 요약 |
|---|---|---|
| COMP-context-api | 컨텍스트 API (Context API) | 템플릿에 주입되는 키-값 데이터 컨테이너. |
| COMP-directive-engine | 지시어 엔진 (Directive Engine) | #foreach #if #set #macro 등 VTL 지시어를 실행한다. |
| COMP-event-handler | 이벤트 핸들러 (Event Handler) | 렌더링 생명주기에 훅을 삽입한다. |
| COMP-introspection | 인트로스펙션 (Introspection) | 리플렉션으로 Java 객체의 프로퍼티·메서드를 조회한다. |
| COMP-parser | JavaCC VTL 파서 | JavaCC로 생성된 VTL 문법 파서를 풀로 관리한다. |
| COMP-resource-loader | 리소스 로더 (Resource Loader) | 파일시스템·클래스패스·JAR·URL 등 다양한 소스에서 .vm 템플릿 파일을 로드하고 캐시한다. |
| COMP-runtime-engine | RuntimeInstance 런타임 엔진 | 엔진 초기화와 설정을 보관하는 중앙 조율자. |
| COMP-template-engine | VelocityEngine 템플릿 엔진 | 외부에 노출되는 공개 API 진입점. |
