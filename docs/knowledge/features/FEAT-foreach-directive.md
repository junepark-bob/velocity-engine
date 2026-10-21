---
agreement: ''
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Foreach.java
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/ForeachScope.java
components: []
confluence: []
git_docs: []
id: FEAT-foreach-directive
jira: []
links:
  confluence:
  - instance: apache
    page_id: '120730723'
    page_owner: human
    role: reference
    title: VelocityWhitespaceGobbling
  - instance: apache
    page_id: '120730631'
    page_owner: human
    role: reference
    title: GenericVelocimacros
  jira:
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
  - instance: apache
    key: VELOCITY-903
    relation: changed-by
  - instance: apache
    key: VELOCITY-916
    relation: changed-by
  - instance: apache
    key: VELOCITY-977
    relation: changed-by
owners: []
provenance:
  code_fingerprint: sha256:6905594b4aac63e8202b5ca7c0c4ece534baece3401d4d9fb495072108eb89ce
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: 컬렉션·배열·맵·이터레이터를 순회하는 VTL 반복 지시어. $velocityCount와 $velocityHasNext 내장 변수로
  인덱스·끝 여부를 확인할 수 있다.
title: '#foreach 반복 지시어'
type: feature
---

## 목적

컬렉션(List, Set, Map, 배열, Iterator)을 순회하며 각 요소를 루프 변수에 바인딩해 블록을 반복 렌더링한다. Java의 `for-each` 루프에 해당한다.

## 동작 방식

1. `#foreach($item in $collection)` 파싱 → `Foreach` 지시어 노드 생성
2. 렌더링 시 컨텍스트에서 `$collection` 조회
3. `Iterable`, 배열, `Map.entrySet()` 중 적절한 이터레이터 선택
4. 반복마다 `$item`을 컨텍스트에 put, 블록 렌더링, 마지막에 제거
5. `$velocityCount`(1-based), `$velocityHasNext`, `$foreach.index`, `$foreach.last` 내장 제공

## 사용 예시

```vtl
## 기본 반복
#foreach($user in $users)
  $velocityCount. $user.name
#end

## 맵 순회
#foreach($entry in $config.entrySet())
  $entry.key = $entry.value
#end

## 마지막 요소 구분
#foreach($item in $list)
  $item#if($velocityHasNext), #end
#end
```

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->