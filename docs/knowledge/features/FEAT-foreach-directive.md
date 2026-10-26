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
    synced_at: '2026-10-26T12:00:35+00:00'
    synced_hash: sha256:bc20a8b03d69f6eaa15472baa51d595b9e5cc2172d933f8da7a6d3772c18d121
    synced_version: 4
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
  code_fingerprint: sha256:7230837eee4e82f36c44a878b1167382918fd6766435132799c30c0bd4c713ac
  created_by: kn-new
  fingerprint_commit: 8dd49ad1
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

## 반복 상한과 경고 (맥락)

`directive.foreach.max_loops`를 1 이상으로 두면 그 횟수에서 반복이 멈추고 나머지 항목은 출력되지 않는다. 예전에는 이 잘림이 아무 흔적 없이 일어나, 운영팀이 출력이 잘린 줄 모르고 장애 분석이 늦어진 일이 있었다. 그래서 상한 때문에 항목이 남은 채 끝나면 템플릿 이름·줄·열과 상한값을 담은 WARN 로그를 `#foreach` 실행당 한 번 남긴다(`#break`로 멈춘 경우는 제외).

기본값(무제한)과 상한에서 멈추는 동작 자체는 기존 템플릿 호환성 때문에 바꾸지 않았다. 로그는 렌더링 전체 기준 중복 제거가 아니라서 같은 템플릿을 반복 렌더링하면 그만큼 남는다. 설정 키 계약은 [CTR-runtime-properties](../contracts/CTR-runtime-properties.md).

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

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2024-02-16 [VELOCITY-977](https://issues.apache.org/jira/browse/VELOCITY-977): Upgrade Java Compiler Compiler to Version 7.0.13 (86cfcf41)
- 2022-06-18: Fix a funny typo (304a5397)
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2019-09-08 [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916): Add a second effect for the debugging flag runtime.log.track_location: display V… (5782c4cf)
- 2019-03-11: [engine] javadoc and indentation fixes (cff1b533)
- 연결된 JIRA: [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776), [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797), [VELOCITY-903](https://issues.apache.org/jira/browse/VELOCITY-903), [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916), [VELOCITY-977](https://issues.apache.org/jira/browse/VELOCITY-977)
<!-- kn:generated:end -->