---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/parser/node/ASTStringLiteral.java
components: []
id: FEAT-string-interpolation
links:
  confluence:
  - instance: apache
    page_id: '120730686'
    page_owner: human
    role: reference
    title: VelocityCommaIfNeeded
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:6106e5e84990297249cc2d67f60b10e33bdadfc0c9d63f12dbe25b53907f47c7
  created_by: kn-new
  fingerprint_commit: c608fcaa
  sources_of_knowledge: []
related: []
status: active
summary: 큰따옴표로 감싼 VTL 문자열 리터럴 안에서 $variable을 평가해 값을 삽입한다. 작은따옴표 문자열은 보간하지 않는다.
title: 문자열 보간 (String Interpolation)
type: feature
---

## 목적

`#set($msg = "Hello $name")` 처럼 문자열 값 안에 변수를 포함할 때 사용한다. Java의 문자열 포맷팅(`String.format`)과 유사하나 컴파일 시점 없이 런타임 평가된다.

## 동작 방식

- **큰따옴표** `"..."` → 문자열 내 `$variable` 평가(보간)
- **작은따옴표** `'...'` → 리터럴, 보간하지 않음

파서가 큰따옴표 문자열 내 `$` 기호를 별도 참조 노드로 파싱한다.

## 사용 예시

```vtl
## 큰따옴표: 보간됨
#set($greeting = "안녕하세요, $user.name 님!")
$greeting

## 작은따옴표: 리터럴
#set($literal = 'Hello $name')
$literal
## 출력: Hello $name

## 중괄호로 경계 명시
#set($tag = "<${elementName}>")
```
## 상세 문서

<!-- kn:generated:start source=links -->
- [VelocityCommaIfNeeded](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730686) — reference
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2026-09-11: Corner case: a final backslash in a double quoted string is deprecated (c9707967)
- 2024-08-23: Normalize some tab-indented source files (08211a61)
- 2024-02-16 [VELOCITY-977](https://issues.apache.org/jira/browse/VELOCITY-977): Upgrade Java Compiler Compiler to Version 7.0.13 (86cfcf41)
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2019-12-28 [VELOCITY-904](https://issues.apache.org/jira/browse/VELOCITY-904): [engine] Fix VELOCITY-904 again (ead820a5)
- 2019-09-08 [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916): Add a second effect for the debugging flag runtime.log.track_location: display VTL stacktrace on errors (5782c4cf)
- 2019-06-17 [VELOCITY-917](https://issues.apache.org/jira/browse/VELOCITY-917): [engine][VELOCITY-917] RuntimeServices shouldn't directly expose configured parser chars (b7f22362)
- 2019-05-31 [VELOCITY-917](https://issues.apache.org/jira/browse/VELOCITY-917): [engine][VELOCITY-917] Preliminary work for VTL chars config: parametrize code using target chars (10cee0a4)
- 2019-03-11: [engine] javadoc and indentation fixes (cff1b533)
- 2017-02-20: [engine] testcase and literals behavior for emptycheck=false; reference should cache emptycheck for speed (765ea383)
<!-- kn:generated:end -->