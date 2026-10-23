---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Block.java
components: []
id: FEAT-if-directive
links:
  confluence:
  - instance: apache
    page_id: '120730641'
    page_owner: human
    role: reference
    title: IfNotNullDirective
  - instance: apache
    page_id: '120730642'
    page_owner: human
    role: reference
    title: IfNullDirective
  - instance: apache
    page_id: '120730613'
    page_owner: human
    role: reference
    title: CheckingForNull
  jira:
  - instance: apache
    key: VELOCITY-789
    relation: changed-by
  - instance: apache
    key: VELOCITY-692
    relation: changed-by
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:e7d8a688c47b804262cde1c16b9e76b07875057f6a32cc0989f642046b9b7de8
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: 'VTL 조건 분기 지시어. #if/#elseif/#else/#end로 구성되며 null·false·빈 컬렉션을 모두 false로
  평가하는 Velocity 고유 truthy 규칙을 적용한다.'
title: '#if 조건 지시어'
type: feature
---

## 목적

조건에 따라 템플릿 블록을 선택 렌더링한다. Java의 `if-else`에 해당한다.

## 동작 방식

Velocity truthy 규칙 (Java와 다름):
- `null` → false
- `Boolean.FALSE` → false
- 빈 컬렉션/배열 → false
- 빈 문자열 `""` → false
- 나머지 모두 → true (0도 true!)

## 사용 예시

```vtl
## 기본 조건
#if($user.admin)
  관리자 메뉴
#elseif($user.manager)
  매니저 메뉴
#else
  일반 메뉴
#end

## null 체크 (null은 false)
#if($optionalValue)
  $optionalValue
#end

## 비교 연산자
#if($count > 0 && $count < 100)
  유효 범위
#end
```
## 상세 문서

<!-- kn:generated:start source=links -->
- [IfNotNullDirective](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730641) — reference
- [IfNullDirective](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730642) — reference
- [CheckingForNull](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730613) — reference
- [VELOCITY-789](https://issues.apache.org/jira/browse/VELOCITY-789) — changed-by
- [VELOCITY-692](https://issues.apache.org/jira/browse/VELOCITY-692) — changed-by
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2019-03-11: [engine] javadoc and indentation fixes (cff1b533)
- 2016-12-13: [engine] optimization: use an unsynchronized string writer whenever possible (3451a6c2)
- 2016-07-22: Applied Jarkko's memory saving patch that drops Tokens while parsing. Review and… (1a4e14ef)
- 2016-07-17 [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797), [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776): [engine] keep macros in defining templates (applied reviewed patch from VELOCITY… (92d42e6f)
- 연결된 JIRA: [VELOCITY-789](https://issues.apache.org/jira/browse/VELOCITY-789), [VELOCITY-692](https://issues.apache.org/jira/browse/VELOCITY-692), [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776), [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797)
<!-- kn:generated:end -->