---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserConfiguration.java
- velocity-custom-parser-example/pom.xml
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
  code_fingerprint: sha256:0b4f496c49716148148cd1b5684054b4373dce6b72ba1e98f81950065f7f0618
  created_by: kn-new
  fingerprint_commit: 8dd49ad1
  sources_of_knowledge: []
related: []
status: active
summary: JavaCC 파서의 특수문자(# $ * @)를 빌드 시점에 바꿔 커스텀 파서를 생성하면 Markdown 등 다른 포맷과 충돌 없이
  VTL을 사용할 수 있다. 런타임 지정(parser.class)과 $ 변경은 2.5부터 deprecated다.
title: 커스텀 파서 설정
type: feature
---

## 목적

VTL 특수문자(`#` 지시어 접두사, `$` 참조 접두사, `*` 블록 주석, `@` 어노테이션)를 다른 문자로 교체한다. Markdown 문서 생성 시 `#`이 제목 문법과 충돌하는 문제를 해결한다.

## 동작 방식

특수문자는 런타임에 객체로 주입하지 않고 **빌드 시점**에 정한다.

1. 문법 파일 `velocity-engine-core/src/main/parser/Parser.jjt`가 Maven 속성 `parser.char.dollar`·`parser.char.hash`·`parser.char.at`·`parser.char.asterisk`로 각 문자를 치환해 JavaCC 파서를 생성한다(기본값 `$` `#` `@` `*`, `velocity-engine-core/pom.xml:40-43`, `Parser.jjt:221-224`).
2. 다른 문자를 쓰려면 이 속성을 바꿔 파서를 따로 생성한다. 예제 모듈은 `#`을 `@`로, `@`를 `%`로 바꾼다(`velocity-custom-parser-example/pom.xml:37-39, 56-62`). 네 문자를 모두 지정해야 하며 기본값과 같아도 적어야 한다(같은 파일 45행 주석).
3. 생성된 파서 클래스는 런타임에 `parser.class` 속성으로 지정한다(`RuntimeConstants.java:452`). 엔진은 설정된 문자를 그 파서에서 읽어 `ParserConfiguration`에 담는다(`RuntimeConstants.java:441-446`).

> **주의**: `parser.class`(런타임 지정)와 `$` 문자 변경은 Velocity 2.5부터 deprecated이고 다음 메이저 버전에서 제거 예정이다(`RuntimeConstants.java:448`).

## 사용 예시

```xml
<!-- 빌드 시점: 커스텀 파서를 생성하는 pom.xml 속성 (# → @, @ → %, Markdown 충돌 방지) -->
<parser.char.asterisk>*</parser.char.asterisk>
<parser.char.at>%</parser.char.at>
<parser.char.dollar>$</parser.char.dollar>
<parser.char.hash>@</parser.char.hash>
```

```java
// 런타임: 생성한 파서 클래스를 지정 (2.5부터 deprecated)
VelocityEngine ve = new VelocityEngine();
ve.setProperty("parser.class", "org.apache.velocity.runtime.parser.custom.CustomParser");
ve.init();
```

```vtl
## 기본 VTL (# 사용)
#foreach($item in $list)$item#end

## 커스텀 파서 (# 대신 @ 사용 시)
@foreach($item in $list)$item@end
```
## 상세 문서

<!-- kn:generated:start source=links -->
- [SilentParseInclude](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730672) — reference
- [VELOCITY-917](https://issues.apache.org/jira/browse/VELOCITY-917) — changed-by
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2019-06-17 [VELOCITY-917](https://issues.apache.org/jira/browse/VELOCITY-917): [engine][VELOCITY-917] RuntimeServices shouldn't directly expose configured pars… (b7f22362)
- 연결된 JIRA: [VELOCITY-917](https://issues.apache.org/jira/browse/VELOCITY-917)
<!-- kn:generated:end -->