---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/RuntimeConstants.java
components: []
id: CTR-runtime-properties
links:
  jira:
  - instance: apache
    key: VELOCITY-542
    relation: changed-by
  - instance: apache
    key: VELOCITY-904
    relation: changed-by
  - instance: apache
    key: VELOCITY-892
    relation: changed-by
  - instance: apache
    key: VELOCITY-909
    relation: changed-by
  - instance: apache
    key: VELOCITY-915
    relation: changed-by
owners:
- role:tech-lead
provenance:
  created_by: kn-new
  sources_of_knowledge: []
related: []
status: proposed
summary: RuntimeConstants.java에 선언된 Velocity 런타임 설정 키·기본값 계약. 키 이름 변경 및 기본값 수정 규칙을
  정의한다.
title: Velocity 런타임 설정 속성 계약
type: contract
---

<!-- append-only: 기존 내용을 고치거나 삭제하지 마세요. 끝에 추가만 허용됩니다. -->

## 대상

`RuntimeConstants.java` 에 선언된 Velocity 런타임 설정 키와 기본값.
`VelocityEngine.setProperty(key, value)` 또는 `velocity.properties` 파일로 제어한다.

## 계약 내용

<!-- kn:generated:start source=RuntimeConstants.java -->
| 설정 키 | 상수명 | 기본값 | 설명 |
|---|---|---|---|
| `resource.default_encoding` | `INPUT_ENCODING` | `UTF-8` | 템플릿 파일 기본 인코딩 |
| `directive.foreach.max_loops` | `MAX_NUMBER_LOOPS` | `-1` (무제한) | #foreach 최대 반복 횟수 |
| `directive.foreach.skip_invalid` | `SKIP_INVALID_ITERATOR` | `true` | 잘못된 이터레이터 건너뜀 여부 |
| `directive.if.empty_check` | `CHECK_EMPTY_OBJECTS` | `true` | `#if`에서 빈 객체를 false로 처리 |
| `directive.parse.max_depth` | `PARSE_DIRECTIVE_MAXDEPTH` | `10` | #parse 중첩 최대 깊이 |
| `resource.loaders` | `RESOURCE_LOADERS` | `file` | 리소스 로더 목록 |
| `resource.loader.file.cache` | `FILE_RESOURCE_LOADER_CACHE` | `false` | 파일 로더 캐시 활성화 여부 |
| `resource.manager.cache.default_size` | `RESOURCE_MANAGER_DEFAULTCACHE_SIZE` | `89` | 리소스 캐시 최대 항목 수 |
<!-- kn:generated:end -->

## 호환성 정책

- 키 이름 변경 시 최소 1 마이너 버전 간 deprecated 키 병용 지원 후 제거.
- 기본값 변경은 마이너 버전 업에서만 허용; 패치는 금지.
- 새 키 추가 시 `RuntimeConstants.java` 상수 선언 + 이 파일 `## 변경 이력` 업데이트.

## 변경 이력

- 2026-10-20: 초기 계약 작성. `INPUT_ENCODING`, `MAX_NUMBER_LOOPS`, `RESOURCE_LOADERS` 등 8개 핵심 키 정의.

## 상세 문서

<!-- kn:generated:start source=links -->
- [VELOCITY-542](https://issues.apache.org/jira/browse/VELOCITY-542) — changed-by
- [VELOCITY-904](https://issues.apache.org/jira/browse/VELOCITY-904) — changed-by
- [VELOCITY-892](https://issues.apache.org/jira/browse/VELOCITY-892) — changed-by
- [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909) — changed-by
- [VELOCITY-915](https://issues.apache.org/jira/browse/VELOCITY-915) — changed-by
<!-- kn:generated:end -->