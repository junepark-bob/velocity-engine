---
id: COMP-directive-engine
type: component
title: "지시어 엔진 (Directive Engine)"
status: active
summary: "#foreach #if #set #macro 등 VTL 지시어를 실행한다. 내장 지시어 외에 커스텀 지시어를 등록할 수 있어 Spring의 HandlerMapping 확장과 유사한 구조다."
aliases: []
owners: []
classification: internal
code:
  - velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/
provenance:
  created_by: kn-new
---

## 역할

VTL 파서가 `#` 로 시작하는 노드를 만나면 지시어 엔진에 위임한다. 내장 지시어(`#foreach` `#if` `#set` `#macro` `#parse` `#include` `#define` `#evaluate` `#break`)를 구현하며, `Directive` 추상 클래스를 상속해 사용자 정의 지시어를 추가할 수 있다.

## 주요 클래스·인터페이스

| 클래스 | 역할 |
|---|---|
| `Directive` | 모든 지시어의 추상 기반 클래스 |
| `Foreach` | 컬렉션·배열·맵 반복 (`#foreach`) |
| `Block` | `#if` `#elseif` `#else` `#end` 조건 분기 |
| `Macro` / `RuntimeMacro` | `#macro` 정의 및 런타임 호출 |
| `Parse` / `Include` | 외부 템플릿 파일 인클루드 |
| `Define` | 렌더링을 변수에 저장 (`#define`) |
| `Evaluate` | 문자열을 VTL로 평가 (`#evaluate`) |

## 다른 컴포넌트와의 관계

- `RuntimeInstance` → 지시어 레지스트리: 초기화 시 내장 지시어 등록
- `ParserPool` → `Directive`: 파싱 단계에서 지시어 노드 생성
- `Foreach` → `ContextAPI`: 루프 변수(`$velocityCount`, `$velocityHasNext`) 주입
- `Macro` → `ResourceManager`: `#parse`로 파일 인클루드 시 로딩 위임

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->
