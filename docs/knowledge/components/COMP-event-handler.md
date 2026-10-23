---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/app/event/
components: []
id: COMP-event-handler
links: {}
owners:
- role:tech-lead
provenance:
  created_by: kn-new
  sources_of_knowledge: []
related: []
status: active
summary: 렌더링 생명주기에 훅을 삽입한다. 참조 삽입·잘못된 참조·메서드 예외 등 이벤트를 가로채 로깅·변환·예외 처리를 커스터마이징할 수
  있다.
title: 이벤트 핸들러 (Event Handler)
type: component
---

## 역할

Spring의 `ApplicationEventPublisher`처럼 렌더링 중 발생하는 이벤트(참조값 삽입, null 참조, 메서드 예외)에 핸들러를 등록해 동작을 커스터마이징한다. `EventCartridge`로 여러 핸들러를 묶어 컨텍스트에 첨부한다.

## 주요 클래스·인터페이스

| 클래스/인터페이스 | 역할 |
|---|---|
| `EventHandler` | 이벤트 핸들러 마커 인터페이스 |
| `ReferenceInsertionEventHandler` | `$var` 값이 출력 스트림에 삽입되기 직전에 호출. 값 변환·이스케이프 용도 |
| `InvalidReferenceEventHandler` | null 또는 없는 참조 접근 시 호출. 로깅·기본값 대체 용도 |
| `MethodExceptionEventHandler` | Java 메서드 호출 중 예외 발생 시 호출. 예외 무시·재throw 결정 |
| `IncludeEventHandler` | `#include`·`#parse` 경로 변환·접근 제어 용도 |
| `EventCartridge` | 여러 `EventHandler`를 묶어 `Context`에 첨부 |
| `EventHandlerUtil` | 런타임에서 핸들러 체인 실행 유틸 |

## 다른 컴포넌트와의 관계

- 사용자 코드 → `EventCartridge` → `VelocityContext`: 핸들러 등록
- `Template` 렌더링 → `EventHandlerUtil`: 이벤트 발생 시 핸들러 체인 순회
- `DirectiveEngine` (`#include`/`#parse`) → `IncludeEventHandler`: 경로 처리 위임

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2021-02-25: Rebased what I could from PR #2 'Add generics parameters and remove unnecesary c… (74644012)
- 2019-09-08 [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916): Add a second effect for the debugging flag runtime.log.track_location: display V… (5782c4cf)
- 2019-06-05 [VELOCITY-915](https://issues.apache.org/jira/browse/VELOCITY-915): [engine][VELOCITY-915] Add new backward compatibility flags to mimic 1.7 behavio… (e1e49487)
- 2019-03-11: [engine] javadoc and indentation fixes (cff1b533)
<!-- kn:generated:end -->