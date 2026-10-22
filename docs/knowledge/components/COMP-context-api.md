---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/context/
- velocity-engine-core/src/main/java/org/apache/velocity/VelocityContext.java
components: []
id: COMP-context-api
links:
  confluence:
  - instance: apache
    page_id: '120730703'
    page_owner: human
    role: reference
    title: VelocityScriptingApi
  - instance: apache
    page_id: '120730648'
    page_owner: human
    role: reference
    title: JspVersusVelocity
  jira:
  - instance: apache
    key: VELOCITY-712
    relation: changed-by
  - instance: apache
    key: VELOCITY-266
    relation: changed-by
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:4562fef37a5f31421b11559cd7879a0aca623214cbc005f6fb8676b84099831f
  created_by: kn-new
  fingerprint_commit: eec00c57
  sources_of_knowledge: []
related: []
status: active
summary: 템플릿에 주입되는 키-값 데이터 컨테이너. Spring MVC의 Model과 동일한 역할로, VTL 변수 조회·저장·체이닝을 담당한다.
title: 컨텍스트 API (Context API)
type: component
---

## 역할

`VelocityContext`는 사용자가 `$variable`에 매핑할 Java 객체를 담는 Map 래퍼다. 내부적으로 `InternalContextAdapter`가 렌더링 중 스코프 관리·이벤트 훅·하우스키핑을 담당하며, `ChainedInternalContextAdapter`로 부모-자식 스코프 체이닝을 지원한다.

## 주요 클래스·인터페이스

| 클래스/인터페이스 | 역할 |
|---|---|
| `Context` | 사용자 API 인터페이스 (`put`, `get`, `remove`) |
| `VelocityContext` | 기본 `Context` 구현체. HashMap 기반 |
| `AbstractContext` | 체이닝·기본 구현 제공 추상 클래스 |
| `InternalContextAdapter` | 렌더링 엔진 내부용 컨텍스트 인터페이스 |
| `InternalContextAdapterImpl` | `Context` + 내부 어댑터 통합 구현 |
| `InternalEventContext` | 이벤트 핸들러 연결 인터페이스 |

## 다른 컴포넌트와의 관계

- 사용자 코드 → `VelocityContext`: 데이터 put 후 `merge()` 호출
- `Template.merge()` → `InternalContextAdapterImpl`: 렌더링 시 내부 컨텍스트로 래핑
- `DirectiveEngine` → `Context`: `#set`, `#foreach` 루프 변수 주입
- `Uberspector` → `Context`: `$obj.prop` 평가 시 객체 꺼내기

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->

## 상세 문서

<!-- kn:generated:start source=links -->
- [VelocityScriptingApi](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730703) — reference
- [JspVersusVelocity](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730648) — reference
- [VELOCITY-712](https://issues.apache.org/jira/browse/VELOCITY-712) — changed-by
- [VELOCITY-266](https://issues.apache.org/jira/browse/VELOCITY-266) — changed-by
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
<!-- kn:generated:end -->