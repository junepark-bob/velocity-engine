---
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/context/**
id: GUIDE-velocity-context-best-practices
owners: []
provenance:
  code_fingerprint: sha256:b8d6b704cb0aabed4439165b81a4a3fd4562f25172886cca97d416b8c073c4f4
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
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