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

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->

## 상세 문서

<!-- kn:generated:start source=links -->
- [VelocityCommaIfNeeded](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730686) — reference
<!-- kn:generated:end -->