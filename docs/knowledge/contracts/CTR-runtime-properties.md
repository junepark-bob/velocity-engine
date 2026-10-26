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
  code_fingerprint: sha256:fde564ec4679577eb0982b8c380e664acb67d1970c57617283de54010f0d36a6
  created_by: kn-new
  fingerprint_commit: 8dd49ad1
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
- 새 키 추가 시 `RuntimeConstants.java`에 상수를 선언하고 기본값은 `velocity.properties`에 적는다.
- 이 항목의 `## 변경 이력`은 `kn generate`가 채우는 생성 구역이므로 직접 고치지 않는다. 계약 항목은 추가만 허용되므로 기존 줄을 바꾸지 않고, 규칙이 바뀌면 끝에 줄을 더하거나 새 항목을 만든다.

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2026-09-15: Deprecate parser.class property, as well as DOLLAR char customization (ae5215e8)
- 2026-09-15: Fix: #evaluate() max depth should honor directive.parse.max_depth (ae068a34)
- 2026-09-13: Deprecate mutable integer ranges (runtime.immutable_ranges = false) (614ef32d)
- 2026-09-13: Deprecate velocimacro.enable_bc_mode without replacement (9e53f0f1)
- 2026-09-10: Un-deprecate informal navigation $foo.bar, introduce ${foo ?: bar} as alternativ… (6c6e84da)
- 연결된 JIRA: [VELOCITY-542](https://issues.apache.org/jira/browse/VELOCITY-542), [VELOCITY-904](https://issues.apache.org/jira/browse/VELOCITY-904), [VELOCITY-892](https://issues.apache.org/jira/browse/VELOCITY-892), [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909), [VELOCITY-915](https://issues.apache.org/jira/browse/VELOCITY-915)
<!-- kn:generated:end -->

- 2026-10-20: 초기 계약 작성. `INPUT_ENCODING`, `MAX_NUMBER_LOOPS`, `RESOURCE_LOADERS` 등 8개 핵심 키 정의.

## 상세 문서

<!-- kn:generated:start source=links -->
- [VELOCITY-542](https://issues.apache.org/jira/browse/VELOCITY-542) — changed-by
- [VELOCITY-904](https://issues.apache.org/jira/browse/VELOCITY-904) — changed-by
- [VELOCITY-892](https://issues.apache.org/jira/browse/VELOCITY-892) — changed-by
- [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909) — changed-by
- [VELOCITY-915](https://issues.apache.org/jira/browse/VELOCITY-915) — changed-by
<!-- kn:generated:end -->

## 정정 기록

- 2026-10-23 · "호환성 정책"의 "새 키 추가 시 `RuntimeConstants.java` 상수 선언 + 이 파일 `## 변경 이력` 업데이트"를 "새 키는 `RuntimeConstants.java`에 상수를 선언하고 기본값은 `velocity.properties`에 적는다"로 고치고, `## 변경 이력`은 `kn generate`가 채우는 생성 구역이라 직접 고치지 않으며 계약 항목은 추가만 허용한다는 문장을 더했다.
- 이유: 진단(`/kn:init`)이 만든 규칙 문장이 현재 구조와 어긋났다(변경 이력은 생성 구역, 계약 항목은 추가만). 이 문장을 따르던 항목 편집이 훅에 거부되는 일이 측정에서 4건 났다.
- 근거: 이 항목의 `## 변경 이력`(`kn:generated` `source=git+jira`), `velocity-engine-core/src/main/java/org/apache/velocity/runtime/RuntimeConstants.java:80`, `velocity-engine-core/src/main/resources/org/apache/velocity/runtime/defaults/velocity.properties:38`(기본값 기록 위치 예: `directive.foreach.max_loops = -1`).
- 관련: 고객 이슈 #6(FEAT-macro-definition 설정 키 오류)과 같은 묶음의 지도 오류 정정, 델타 `D-20261023-001`.
- 계약 내용(키 이름 변경 시 deprecated 병용, 기본값은 마이너 버전에서만 변경)은 바뀌지 않았다.

## 보충 기록

- 2026-10-26 · `directive.foreach.max_loops` 상한에 닿아 `#foreach` 반복이 잘리면(남은 항목이 있고 `#break`가 아닐 때) `Foreach`가 템플릿 이름·줄·열과 상한값을 담은 WARN 로그를 `#foreach` 실행당 한 번 남긴다. 기본값(무제한)과 상한에서 멈추는 동작은 그대로다.
- 근거: `velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Foreach.java`(`render()`), 델타 `D-20261026-001`.