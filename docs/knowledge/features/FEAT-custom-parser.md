---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserConfiguration.java
components: []
id: FEAT-custom-parser
links:
  confluence:
  - instance: apache
    page_id: '120730672'
    page_owner: human
    role: reference
    title: SilentParseInclude
  jira:
  - instance: apache
    key: VELOCITY-917
    relation: changed-by
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:c6b1a69edfdf381ed56df6741ebce24efe77120d640903a1c457de31124112e0
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: JavaCC 파서의 특수문자(# $ * @)를 변경해 Markdown 등 다른 포맷과 충돌 없이 VTL을 사용할 수 있다. ParserConfiguration으로
  설정하며 2.5+ 버전에서 $ 변경은 deprecated다.
title: 커스텀 파서 설정
type: feature
---

## 목적

VTL 특수문자(`#` 지시어 접두사, `$` 참조 접두사, `*` 블록 주석, `@` 어노테이션)를 다른 문자로 교체한다. Markdown 문서 생성 시 `#`이 제목 문법과 충돌하는 문제를 해결한다.

## 동작 방식

`ParserConfiguration` 객체로 파서 특수문자를 변경한 뒤 `RuntimeInstance`에 주입한다. 변경된 파서는 해당 엔진 인스턴스에만 적용되므로 여러 엔진을 독립 운영할 수 있다.

> **주의**: `$` 문자 변경은 Velocity 2.5부터 deprecated. 다음 메이저 버전에서 제거 예정.

## 사용 예시

```java
// # 대신 % 사용 (Markdown 생성 시 충돌 방지)
VelocityEngine ve = new VelocityEngine();
Properties p = new Properties();
p.setProperty("parser.allow_hyphen_in_identifiers", "true");
// 커스텀 파서 jar를 빌드한 뒤 런타임에 지정
p.setProperty("runtime.custom_directives",
    "com.example.CustomForeachDirective");
ve.init(p);
```

```vtl
## 기본 VTL (# 사용)
#foreach($item in $list)$item#end

## 커스텀 파서 (% 사용 시)
%foreach($item in $list)$item%end
```

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->

## 상세 문서

<!-- kn:generated:start source=links -->
- [SilentParseInclude](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730672) — reference
- [VELOCITY-917](https://issues.apache.org/jira/browse/VELOCITY-917) — changed-by
<!-- kn:generated:end -->