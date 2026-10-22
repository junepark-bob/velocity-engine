---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/RuntimeInstance.java
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/RuntimeServices.java
components: []
id: COMP-runtime-engine
links:
  confluence:
  - instance: apache
    page_id: '120730657'
    page_owner: human
    role: design
    title: MonostateVelocityEngine
  - instance: apache
    page_id: '120730689'
    page_owner: human
    role: guide
    title: VelocityDocs
  jira:
  - instance: apache
    key: VELOCITY-789
    relation: changed-by
  - instance: apache
    key: VELOCITY-809
    relation: changed-by
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
  - instance: apache
    key: VELOCITY-827
    relation: changed-by
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:a5306147ddd3f0bcaf3790784bd72f5ec479271c0958f6ed200695a200456150
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: 엔진 초기화와 설정을 보관하는 중앙 조율자. Spring의 ApplicationContext에 해당하며 파서 풀·리소스 관리자·지시어
  레지스트리·인트로스펙션을 묶는다.
title: RuntimeInstance 런타임 엔진
type: component
---

## 역할

`RuntimeInstance`는 엔진 전체의 싱글턴 상태 저장소다. `VelocityEngine` 생성 시 내부적으로 생성되어 초기화된다. 설정 프로퍼티, 파서 풀, 리소스 관리자, 지시어 레지스트리, 인트로스펙션 매니저를 한 곳에서 소유한다. Spring의 `ApplicationContext`처럼 다른 컴포넌트가 의존성을 가져가는 중심점이다.

## 주요 클래스·인터페이스

| 클래스/인터페이스 | 역할 |
|---|---|
| `RuntimeInstance` | 엔진 상태 구현체. `init()` 호출로 모든 서브시스템 초기화 |
| `RuntimeServices` | 파서·리소스·인트로스펙션 등을 노출하는 내부 서비스 인터페이스 |
| `RuntimeConstants` | 설정 키 상수 모음 (Spring `@Value` key와 유사) |
| `ParserConfiguration` | JavaCC 파서의 특수문자 설정 (커스터마이징 가능) |

## 다른 컴포넌트와의 관계

- `VelocityEngine` → `RuntimeInstance`: 공개 API가 런타임 인스턴스를 래핑
- `RuntimeInstance` → `ParserPool`: 파서 인스턴스 대여·반납 조율
- `RuntimeInstance` → `ResourceManager`: 템플릿 로딩·캐싱 위임
- `RuntimeInstance` → `DirectiveManager`: `#` 지시어 등록·실행 위임
- `RuntimeInstance` → `IntrospectionManager`: Java 객체 접근 메서드 조회 위임

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->