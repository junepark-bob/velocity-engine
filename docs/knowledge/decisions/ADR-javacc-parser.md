---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/parser/Parser.jjt
components: []
id: ADR-javacc-parser
links:
  jira:
  - instance: apache
    key: VELOCITY-789
    relation: changed-by
  - instance: apache
    key: VELOCITY-706
    relation: changed-by
  - instance: apache
    key: VELOCITY-863
    relation: changed-by
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
owners:
- role:architect
provenance:
  code_fingerprint: sha256:6d578e96fa87577e4b3e6e3b285bfbdbc7a92987c74092dc84642322c0cf84da
  created_by: kn-new
  fingerprint_commit: 85721ef9
  sources_of_knowledge: []
related: []
status: active
summary: VTL 문법 파서를 JavaCC로 구현하고, 특수문자 커스터마이징을 위한 빌드 타임 파서 재생성을 공식 지원한다.
title: 'ADR: JavaCC 기반 파서 채택'
type: decision
---

<!-- append-only: 기존 내용을 고치거나 삭제하지 마세요. 끝에 추가만 허용됩니다. -->

## 상태

채택됨 (2.x 기준. 1.x 때부터 유지)

## 맥락

Velocity는 `$variable`, `#directive`, `@reference` 등의 특수문자를 VTL 문법으로 정의해 사용한다. 파서 구현 방식에 따라 문법 확장성과 런타임 성능이 결정된다. 일부 사용처(Markdown 생성 등)에서는 `#`을 VTL 지시어 접두사 대신 다른 용도로 쓰고 싶다는 요구가 있었다.

## 결정

JavaCC(Java Compiler Compiler)를 파서 생성기로 채택한다. 문법은 `velocity-engine-core/src/main/parser/Parser.jjt`(JJTree 문법) 한 파일이고, 빌드 타임에 `javacc-maven-plugin`의 `jjtree-javacc` 목표로 Java 파서 소스를 생성한다(`velocity-engine-core/pom.xml`). `*`, `@`, `#`, `$` 특수문자는 런타임 설정이 아니라 **빌드 시점 속성**(`parser.char.asterisk`·`parser.char.at`·`parser.char.hash`·`parser.char.dollar`, `velocity-engine-core/pom.xml:40-43`, `Parser.jjt:221-224`)으로 정해 커스텀 파서를 따로 생성해 바꾼다(`velocity-custom-parser-example`). `ParserConfiguration`은 설정된 치환 문자를 담아 두는 클래스이며 엔진이 파서에서 읽어 채운다(`RuntimeConstants.java:441-446`). 단, 커스텀 파서를 런타임에 지정하는 `parser.class` 속성(`RuntimeConstants.java:452`)과 `$` 변경은 2.5에서 deprecated, 다음 메이저에서 제거 예정.

## 결과

- 긍정: 문법을 `Parser.jjt` 파일 한 곳에서 관리. 커스텀 파서 생성이 빌드 스크립트로 자동화됨.
- 부정: 파서 수정 시 JavaCC 빌드 단계가 필요. IDE에서 `.jj` 파일 직접 편집 시 별도 도구 필요.
- `$` 커스터마이징 deprecated → Markdown 출력 등 `$`를 다른 용도로 쓰는 사용처는 마이그레이션 필요.

## 대안

- **ANTLR**: 더 강력하나 Velocity 초기(2001년) 당시 JavaCC가 표준적이었고 이미 구현 완료.
- **수동 파서**: 유지보수 부담이 커 기각.

## 상세 문서

<!-- kn:generated:start source=links -->
- [VELOCITY-789](https://issues.apache.org/jira/browse/VELOCITY-789) — changed-by
- [VELOCITY-706](https://issues.apache.org/jira/browse/VELOCITY-706) — changed-by
- [VELOCITY-863](https://issues.apache.org/jira/browse/VELOCITY-863) — changed-by
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2026-09-25: Reduce the scope of the deprecated flags/features: restore ${exp|altValue}, remo… (0c461087)
- 2026-09-10: Un-deprecate informal navigation $foo.bar, introduce ${foo ?: bar} as alternativ… (6c6e84da)
- 2026-06-13 [VELOCITY-995](https://issues.apache.org/jira/browse/VELOCITY-995): VTL syntax deprecation warnings (still off by default) (0b6fa31b)
- 2026-04-24: Fix javacc warnings (3c544916)
- 2025-11-04: Add a few tests for block macros formal references (06a4a263)
- 연결된 JIRA: [VELOCITY-789](https://issues.apache.org/jira/browse/VELOCITY-789), [VELOCITY-706](https://issues.apache.org/jira/browse/VELOCITY-706), [VELOCITY-863](https://issues.apache.org/jira/browse/VELOCITY-863), [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776), [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797)
<!-- kn:generated:end -->