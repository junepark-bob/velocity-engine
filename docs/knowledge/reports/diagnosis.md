# 최초 진단 리포트 — Apache Velocity Engine

**생성일**: 2026-10-20  
**대상 저장소**: apache/velocity-engine (fork: junepark-bob/velocity-engine)  
**모듈 범위**: velocity-engine-core  
**생성 도구**: kn v0.1 / /kn:init 스킬

---

## 1. 요약

| 항목 | 값 |
|---|---|
| 지식 항목 수 | 21개 (아키텍처 1 · 컴포넌트 8 · 피처 10 · 결정 1 · 가이드 1) |
| kn lint 오류 | **0건** (경고 0건) |
| 소스 파일 수 | 213개 (velocity-engine-core/src/main/java) |
| 테스트 파일 수 | 171개 |
| 생성된 외부 링크 | 2건 |
| kn generate (git-log) | 실행 완료 (로그 없음 — 신규 fork로 커밋 없음) |
| 소요 시간 (A1) | 약 15분 (scan → 항목 생성 → 내용 보강 → lint 통과) |

---

## 2. 항목별 현황

### 아키텍처

| ID | 제목 | 상태 |
|---|---|---|
| ARCH-velocity-engine-core | Velocity Engine Core 아키텍처 | active |

### 컴포넌트 (8개)

| ID | 제목 | 핵심 요약 |
|---|---|---|
| COMP-runtime-engine | RuntimeInstance 런타임 엔진 | 엔진 생명주기·설정 관리, Spring ApplicationContext 대응 |
| COMP-template-engine | VelocityEngine · Template | 공개 API 진입점, 템플릿 파싱·렌더링 |
| COMP-parser | JavaCC 기반 VTL 파서 | Parser.jjt → 빌드 타임 파서 생성, ParserPool로 풀 관리 |
| COMP-directive-engine | VTL 지시어 엔진 | #foreach #if #set #macro 등 11개 내장 지시어 |
| COMP-resource-loader | 리소스 로더 체인 | File · Classpath · URL · String 로더, 캐시 포함 |
| COMP-introspection | IntrospectionManager | 리플렉션 기반 Java 객체 프로퍼티 접근 (OGNL 미사용) |
| COMP-context-api | VelocityContext / Context | 키-값 데이터 컨테이너, 체인·중첩 지원 |
| COMP-event-handler | EventHandlerUtil | 렌더링 생명주기 훅 (참조삽입·예외·로그) |

### 피처 (10개)

| ID | 제목 |
|---|---|
| FEAT-template-rendering | VTL 템플릿 렌더링 |
| FEAT-variable-resolution | 변수 참조 해석 |
| FEAT-foreach-directive | #foreach 컬렉션 반복 |
| FEAT-if-directive | #if 조건 분기 |
| FEAT-string-interpolation | 큰따옴표 내 변수 보간 |
| FEAT-file-resource-loading | 파일시스템 리소스 로딩 |
| FEAT-classpath-resource-loading | 클래스패스 리소스 로딩 |
| FEAT-macro-definition | #macro 재사용 블록 정의 |
| FEAT-spring-integration | Spring VelocityEngineFactoryBean |
| FEAT-custom-parser | 파서 특수문자 커스터마이징 |

### 결정 (1개)

| ID | 제목 |
|---|---|
| ADR-javacc-parser | ADR: JavaCC 기반 파서 채택 |

### 가이드 (1개)

| ID | 제목 |
|---|---|
| GUIDE-velocity-context-best-practices | VelocityContext 사용 모범 사례 |

---

## 3. 진단 소견

### 발견된 구조적 특징

1. **파서 커스터마이징 지원** (ADR-javacc-parser): JavaCC 기반 `.jjt` 파일이 `src/main/parser/`에 있고 빌드 타임 생성 구조. Markdown 생성 등 `#` 충돌 케이스가 실 운영에서 발생할 수 있으며, `$` 변경은 2.5부터 deprecated.

2. **스레드 안전성 주의점** (GUIDE): `VelocityContext`는 스레드 비안전. 요청별 신규 인스턴스 필요. Spring MVC 뷰 레이어 통합 시 특히 주의.

3. **모듈 분리** (ARCH): core / scripting(JSR-223) / spring6 / spring5(레거시) / examples 로 분리. Spring 5 레거시 모듈은 별도 유지 중.

### [PoC 제약]

- `kn generate --source git-log` 구역이 모든 피처/컴포넌트에 삽입됐으나, fork 저장소 특성상 커밋 이력이 없어 내용이 비어 있음. 실제 저장소 적용 시 자동 채워짐.
- 외부 링크(Confluence·JIRA 연동)는 Day 9(F4)에서 추가 예정.
- 코드 커버리지 수치(A3)는 별도 `mvn jacoco:report` 실행 필요 — 이번 진단에서는 테스트 파일 171개 / 소스 213개로 추정만 기록.

---

## 4. 메트릭 (A 시리즈)

| 메트릭 | 값 | 비고 |
|---|---|---|
| A1 최초 파악 시간 | ~15분 | scan → 항목생성 → 내용보강 → lint 0건 |
| A3 테스트 파일 수 | 171개 / 소스 213개 | jacoco 미실행, 수치는 추정 |
| A4 외부 링크 수 | 2건 | 지식 지도 내 https 링크 |
| A6 토큰/비용 | 측정 중 | Claude Code 크레딧 소모량은 Portal 콘솔에서 확인 |

---

*이 리포트는 `kn`이 자동 생성한 초기 진단이며, 사람이 검토·보완해야 합니다.*
