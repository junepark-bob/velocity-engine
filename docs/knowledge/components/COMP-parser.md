---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserPool.java
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserPoolImpl.java
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserConfiguration.java
components: []
id: COMP-parser
links:
  confluence:
  - instance: apache
    page_id: '120730672'
    page_owner: human
    role: reference
    title: SilentParseInclude
  - instance: apache
    page_id: '120730656'
    page_owner: human
    role: reference
    title: MacroIssues
  - instance: vendor
    page_id: ''
    page_owner: ai
    role: reference
    synced_at: '2026-10-21T05:49:05+00:00'
    synced_hash: sha256:107b0232653a970ef06758c53552252a7ae7b7b604964c17e2beb47551321d8f
    synced_version: 2
    title: JavaCC VTL 파서 (COMP-parser)
  jira:
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
  - instance: apache
    key: VELOCITY-917
    relation: changed-by
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:fb3946f59fbd816e58dbf923f2fb4e812b6a3b9b66b7c2c103feed65be676732
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: JavaCC로 생성된 VTL 문법 파서를 풀로 관리한다. 파서는 재진입 불가라서 동시 요청마다 별도 인스턴스를 대여하고 반납하는 풀
  방식을 사용한다.
title: JavaCC VTL 파서
type: component
---

## 역할

VTL 문법을 파싱해 AST(추상 구문 트리)를 생성한다. JavaCC로 생성된 파서는 스레드 안전하지 않으므로 `ParserPool`이 일정 수의 인스턴스를 미리 생성해 두고 요청마다 대여·반납한다. `ParserConfiguration`으로 `#` `$` `*` `@` 특수문자를 바꿀 수 있다.

## 주요 클래스·인터페이스

| 클래스/인터페이스 | 역할 |
|---|---|
| `ParserPool` | 파서 인스턴스 풀 인터페이스 |
| `ParserPoolImpl` | 블로킹 큐 기반 풀 구현체 |
| `ParserConfiguration` | 파서 특수문자 설정 (커스텀 파서 지원) |

## 다른 컴포넌트와의 관계

- `RuntimeInstance` → `ParserPool`: 초기화 시 풀 생성, 파싱 시 인스턴스 대여·반납
- `Template` → `ParserPool`: 최초 로딩 시 파싱 요청
- `ParserPool` ↔ `DirectiveEngine`: 파서가 `#` 노드 인식 후 지시어 엔진에 처리 위임

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->