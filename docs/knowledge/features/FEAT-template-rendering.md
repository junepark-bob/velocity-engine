---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/app/VelocityEngine.java
components: []
id: FEAT-template-rendering
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
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:3530bc5182342fce5963b7d906c9cdd909eada4a24b9edd593de2ca33740a707
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: VTL 템플릿 파일과 VelocityContext를 병합해 최종 텍스트를 생성하는 핵심 기능. VelocityEngine.merge()가
  진입점이다.
title: VTL 템플릿 렌더링
type: feature
---

## 목적

`.vm` 템플릿 파일과 Java 객체 컨텍스트를 받아 HTML·SQL·코드·이메일 본문 등 텍스트를 생성한다. Spring MVC의 `View.render(model, response)` 에 해당한다.

## 동작 방식

1. `VelocityEngine.getTemplate("name.vm")` → `ResourceManager`가 로더 체인에서 파일 로드
2. 첫 요청에 JavaCC 파서가 VTL을 AST로 변환, `ResourceCache`에 저장
3. `Template.merge(context, writer)` 호출 → AST 노드를 순회하며 `Writer`에 출력
4. `$variable` 노드 → `Uberspector`로 컨텍스트에서 값 꺼내기
5. `#` 지시어 노드 → `DirectiveEngine` 위임

## 사용 예시

```java
VelocityEngine ve = new VelocityEngine();
ve.init();

VelocityContext ctx = new VelocityContext();
ctx.put("name", "World");

Template t = ve.getTemplate("hello.vm");
StringWriter sw = new StringWriter();
t.merge(ctx, sw);
// hello.vm: Hello $name!  →  "Hello World!"
```
## 상세 문서

<!-- kn:generated:start source=links -->
- [HomepageTemplate](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730640) — reference
- [VelocityDocs](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730689) — guide
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
- [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909) — changed-by
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2026-10-20: feat: VelocityEngine.getTemplate() 인코딩 명시화 + 지식 지도 보강 (F2/F3) (0b3e1d82)
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2019-03-15: [engine] Remove all instances of LogChute in the javadocs (bdfa47d4)
- 2019-03-11: [engine] javadoc and indentation fixes (cff1b533)
- 2019-03-06: [engine] configuration key names refactoring proposal (f31d3d3f)
- 연결된 JIRA: [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776), [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797), [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909)
<!-- kn:generated:end -->