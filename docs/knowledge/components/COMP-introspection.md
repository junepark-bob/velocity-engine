---
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/util/introspection/
id: COMP-introspection
links:
  confluence:
  - instance: apache
    page_id: '120730658'
    page_owner: human
    role: design
    title: MultiUberspect
  - instance: apache
    page_id: '120730649'
    page_owner: human
    role: reference
    title: JythonUberspect
  - instance: apache
    page_id: '120730726'
    page_owner: human
    role: reference
    title: WebappUberspector
owners:
- role:tech-lead
provenance:
  created_by: kn-new
status: active
summary: 리플렉션으로 Java 객체의 프로퍼티·메서드를 조회한다. OGNL 없이 순수 리플렉션 캐시로 $object.property 접근을
  처리하며 Spring의 BeanWrapper와 유사한 역할이다.
title: 인트로스펙션 (Introspection)
type: component
---

## 역할

VTL 표현식 `$obj.name`을 평가할 때 `obj`의 `getName()` 또는 `name` 필드를 리플렉션으로 찾는다. `ClassMap`이 클래스별 메서드 맵을 캐시해 반복 조회 비용을 줄인다. `Uberspector` 인터페이스로 접근 전략을 교체할 수 있다(체이닝 가능).

## 주요 클래스·인터페이스

| 클래스/인터페이스 | 역할 |
|---|---|
| `Uberspector` (인터페이스) | Java 객체 접근 전략 추상화. Spring `BeanWrapper`와 유사 |
| `UberspectImpl` | 기본 리플렉션 기반 구현체 |
| `ChainableUberspector` | 여러 Uberspector를 체인으로 연결 |
| `ClassMap` | 클래스별 메서드·프로퍼티 리플렉션 결과 캐시 |
| `IntrospectionUtils` | getter 이름 규칙(`get*`, `is*`) 처리 유틸 |
| `ConversionHandler` | 타입 자동 변환 처리 |

## 다른 컴포넌트와의 관계

- `RuntimeInstance` → `IntrospectionManager`: 런타임 초기화 시 Uberspector 설정
- `DirectiveEngine`, `Template` 렌더링 → `Uberspector`: `$` 참조 노드 평가 시 호출
- `ContextAPI` → `Uberspector`: 컨텍스트 값에서 프로퍼티 접근

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->