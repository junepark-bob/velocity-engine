---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Foreach.java
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/ForeachScope.java
components: []
id: FEAT-foreach-directive
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
  - instance: vendor
    page_id: '1179649'
    page_owner: ai
    role: reference
    synced_at: '2026-10-21T05:49:05+00:00'
    synced_hash: sha256:8afd8da25b7c89f48e1b3fc92f344bbcc29680218af66645d23d7e900f1bf2e4
    synced_version: 2
    title: '#foreach 반복 지시어 (FEAT-foreach-directive)'
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
owners:
- role:tech-lead
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

## 상세 문서

<!-- kn:generated:start source=links -->
- [VelocityWhitespaceGobbling](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730723) — reference
- [GenericVelocimacros](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730631) — reference
- [#foreach 반복 지시어 (FEAT-foreach-directive)](https://bobphw.atlassian.net/wiki/pages/viewpage.action?pageId=1179649) — reference · kn 생성 페이지
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
- [VELOCITY-903](https://issues.apache.org/jira/browse/VELOCITY-903) — changed-by
- [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916) — changed-by
- [VELOCITY-977](https://issues.apache.org/jira/browse/VELOCITY-977) — changed-by
<!-- kn:generated:end -->