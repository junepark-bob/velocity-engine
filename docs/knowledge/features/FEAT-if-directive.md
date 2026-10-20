---
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Block.java
id: FEAT-if-directive
owners: []
provenance:
  code_fingerprint: sha256:e7d8a688c47b804262cde1c16b9e76b07875057f6a32cc0989f642046b9b7de8
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
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

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->