---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/app/VelocityEngine.java
- velocity-engine-core/src/main/java/org/apache/velocity/app/Velocity.java
- velocity-engine-core/src/main/java/org/apache/velocity/Template.java
components: []
id: COMP-template-engine
links:
  confluence:
  - instance: apache
    page_id: '120730640'
    page_owner: human
    role: reference
    title: HomepageTemplate
  - instance: apache
    page_id: '120730689'
    page_owner: human
    role: guide
    title: VelocityDocs
  jira:
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
  - instance: apache
    key: VELOCITY-909
    relation: changed-by
  - instance: apache
    key: VELOCITY-916
    relation: changed-by
  - instance: apache
    key: VELOCITY-958
    relation: changed-by
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:26432a7b94102f086c1b508b2e2bb1471f6d08efa175ab92c4460ec8ce1bd098
  created_by: kn-new
  fingerprint_commit: 8dd49ad1
  sources_of_knowledge: []
related: []
status: active
summary: 외부에 노출되는 공개 API 진입점. 템플릿 파싱과 VTL 컨텍스트 병합을 담당하며 Spring MVC의 ViewResolver +
  View 역할에 해당한다.
title: VelocityEngine 템플릿 엔진
type: component
---

## 역할

`VelocityEngine`은 사용자가 직접 호출하는 유일한 공개 진입점이다. `getTemplate(name)` 으로 파싱된 `Template` 객체를 가져오고, `merge(template, context, writer)` 로 텍스트를 생성한다. `Velocity` 는 정적 싱글턴 래퍼다. `Template` 은 파싱된 AST를 캐시하고 렌더링 시 `VelocityContext` 와 결합한다.

## 주요 클래스·인터페이스

| 클래스 | 역할 |
|---|---|
| `VelocityEngine` | 인스턴스 기반 API. `init()`, `getTemplate()`, `merge()`, `evaluate()` |
| `Velocity` | `VelocityEngine`의 정적 싱글턴 편의 래퍼 |
| `Template` | 파싱된 AST 보유. `merge(context, writer)` 로 출력 생성 |

## 다른 컴포넌트와의 관계

- `VelocityEngine` → `RuntimeInstance`: 내부 실행을 전부 위임
- `Template` → `ParserPool`: 최초 파싱 시 파서 인스턴스 대여
- `Template` → `ResourceLoader`: 소스 파일 읽기
- `Template.merge()` → `DirectiveEngine`: `#` 노드 실행 위임
## 상세 문서

<!-- kn:generated:start source=links -->
- [HomepageTemplate](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730640) — reference
- [VelocityDocs](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730689) — guide
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
- [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909) — changed-by
- [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916) — changed-by
- [VELOCITY-958](https://issues.apache.org/jira/browse/VELOCITY-958) — changed-by
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2026-10-20: feat: VelocityEngine.getTemplate() 인코딩 명시화 + 지식 지도 보강 (F2/F3) (0b3e1d82)
- 2022-07-25 [VELOCITY-958](https://issues.apache.org/jira/browse/VELOCITY-958): Make templates cloneable - fixes VELOCITY-958 (051f20a8)
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2021-02-25: Rebased what I could from PR #2 'Add generics parameters and remove unnecesary c… (74644012)
- 2019-09-08 [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916): Add a second effect for the debugging flag runtime.log.track_location: display V… (5782c4cf)
- 연결된 JIRA: [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776), [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797), [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909), [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916), [VELOCITY-958](https://issues.apache.org/jira/browse/VELOCITY-958)
<!-- kn:generated:end -->