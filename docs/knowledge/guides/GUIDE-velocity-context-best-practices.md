---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/context/**
components: []
id: GUIDE-velocity-context-best-practices
links:
  confluence:
  - instance: apache
    page_id: '120730691'
    page_owner: human
    role: reference
    title: VelocityFAQ
  - instance: apache
    page_id: '120730613'
    page_owner: human
    role: reference
    title: CheckingForNull
  jira:
  - instance: apache
    key: VELOCITY-266
    relation: changed-by
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
  code_fingerprint: sha256:b8d6b704cb0aabed4439165b81a4a3fd4562f25172886cca97d416b8c073c4f4
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: VelocityContext를 안전하고 효율적으로 사용하기 위한 체인·중첩·스레드 안전성 지침.
title: VelocityContext 사용 모범 사례
type: guide
---

## 언제 쓰나

- `VelocityEngine.merge()` 또는 `Template.merge()`를 호출하기 전에 템플릿에 노출할 데이터를 담는다.
- 중첩 맥락(체인 컨텍스트)이 필요할 때: 전역 데이터는 부모, 요청별 데이터는 자식 컨텍스트에 둔다.

## 절차

1. `VelocityContext ctx = new VelocityContext();` 생성 (Spring `Model`에 해당).
2. `ctx.put("key", value);` 로 Java 객체를 등록. 키는 VTL에서 `$key`로 접근된다.
3. 체인이 필요하면 `new VelocityContext(parentCtx)` — 자식에 없는 키는 부모에서 찾는다.
4. `engine.merge(template, ctx, writer)` 호출 후 컨텍스트를 재사용하지 않는다(렌더링 도중 내부 상태 변경됨).

## 따라 할 예시

```java
VelocityEngine engine = new VelocityEngine();
engine.init();

VelocityContext ctx = new VelocityContext();
ctx.put("name", "World");
ctx.put("items", List.of("A", "B", "C"));

StringWriter sw = new StringWriter();
engine.mergeTemplate("hello.vm", "UTF-8", ctx, sw);
System.out.println(sw);
```

`hello.vm`:
```vtl
Hello $name!
#foreach($item in $items)
  - $item
#end
```

## 검증 방법

- 렌더링 결과에서 `$name`이 그대로 출력되면 컨텍스트 키 불일치 — `ctx.put("name", ...)` 확인.
- `NullPointerException` 발생 시 `$!{variable}` (조용한 참조) 사용 검토.
- 멀티스레드 환경: `VelocityContext`는 스레드 안전하지 않으므로 요청마다 새 인스턴스 생성.

## 상세 문서

<!-- kn:generated:start source=links -->
- [VelocityFAQ](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730691) — reference
- [CheckingForNull](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730613) — reference
- [VELOCITY-266](https://issues.apache.org/jira/browse/VELOCITY-266) — changed-by
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
- [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909) — changed-by
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2021-02-25: Rebased what I could from PR #2 'Add generics parameters and remove unnecesary casts' (74644012)
- 2019-03-11: [engine] javadoc and indentation fixes (cff1b533)
- 2019-03-10 [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909): [engine][VELOCITY-909] Propagate propnames changes thorough javadoc; some more related code fixes (fec80129)
- 2018-07-13: some javadoc bugs incidentally fixed (40f76190)
- 2017-01-28: [engine] full code review (foreach loops and some other problems detected by code analysis tools) (23e6d0fa)
- 2017-01-26: [engine] fix trailing whitespaces (2880a3c0)
- 2016-07-22: Applied Jarkko's memory saving patch that drops Tokens while parsing. Review and specific tests still in progress, but already functionnal. One change from the patch: String interning straregy has been made a boolean configuration property. (1a4e14ef)
- 2016-07-17 [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797), [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776): [engine] keep macros in defining templates (applied reviewed patch from VELOCITY-797, fixes VELOCITY-797 and VELOCITY-776); plus some code cleaning that was in the patch (92d42e6f)
- 2016-07-13 [VELOCITY-266](https://issues.apache.org/jira/browse/VELOCITY-266): Take advantage of the major version jump to enforce String keys in internal context API (fixes VELOCITY-266) (f576abbf)
- 연결된 JIRA: [VELOCITY-266](https://issues.apache.org/jira/browse/VELOCITY-266), [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776), [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797), [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909)
<!-- kn:generated:end -->