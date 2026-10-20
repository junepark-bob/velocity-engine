---
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/**
id: ARCH-velocity-engine-core
owners: []
provenance:
  code_fingerprint: sha256:c2c28206e2e321638333283f56effc92c7ef877568e4a8a0202cdc60ea64a076
  created_by: kn-new
  fingerprint_commit: 6f6290c3
status: active
summary: Java 기반 범용 템플릿 엔진. VTL(Velocity Template Language)을 파싱해 컨텍스트 데이터와 병합하여 텍스트를
  생성한다. RuntimeInstance가 중심 조율자 역할을 하며 파서 풀·리소스 로더·지시어 엔진이 협력한다.
title: Velocity Engine Core 아키텍처
type: architecture
---

## 목적

VTL 문법으로 작성된 템플릿 파일과 Java 객체 컨텍스트를 받아 텍스트(HTML, SQL, 코드 등)를 생성한다. 웹 MVC 뷰 레이어, 코드 생성, 이메일 본문 생성 등에 사용된다.

## 구성도

```
VelocityEngine (진입점)
    └─ RuntimeInstance (Spring의 ApplicationContext에 해당하는 중앙 조율자)
         ├─ ParserPool        : JavaCC 파서 인스턴스 풀
         ├─ ResourceManager   : 템플릿·정적 리소스 캐시 + 로더 체인
         │    └─ ResourceLoader(s): File / Classpath / URL / String / ...
         ├─ DirectiveManager  : #foreach #if #set #macro 등 지시어 등록·실행
         ├─ IntrospectionManager : 리플렉션 기반 Java 객체 프로퍼티 접근
         └─ EventHandlerUtil  : 렌더링 생명주기 훅(참조 삽입·예외·로그)
```

## 구성 요소 목록

| 컴포넌트 | 역할 |
|---|---|
| `VelocityEngine` / `Velocity` | 공개 API 진입점. Spring의 `@Service` 빈과 유사 |
| `RuntimeInstance` | 엔진 상태·설정을 보관하는 단일 런타임 컨텍스트 |
| `Template` | 파싱된 AST를 캐시하는 렌더링 단위 (Spring의 View 객체) |
| `VelocityContext` | 키-값 데이터 컨테이너. Spring Model과 동일한 역할 |
| `ParserPool` | 재진입 불가 JavaCC 파서를 풀로 관리 |
| `ResourceManager` | 템플릿 캐시와 여러 ResourceLoader 조율 |
| 지시어 엔진 | `#foreach` `#if` `#set` `#macro` 등 VTL 지시어 실행 |
| IntrospectionManager | OGNL 없이 순수 리플렉션으로 Java 객체 접근 |

## 외부 연동

- **Spring Framework**: `spring-velocity-support` 모듈이 `VelocityEngineFactoryBean`을 제공. Spring 6/7용과 Spring 5용(레거시)으로 분리.
- **JSR-223 스크립팅**: `velocity-engine-scripting` 모듈로 `ScriptEngine` API 지원.
- **Apache Commons Collections**: `ExtendedProperties` 설정 파싱.

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->