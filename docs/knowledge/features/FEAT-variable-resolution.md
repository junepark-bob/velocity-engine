---
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/util/introspection/
- velocity-engine-core/src/main/java/org/apache/velocity/context/
id: FEAT-variable-resolution
links:
  confluence:
  - instance: apache
    page_id: '120730613'
    page_owner: human
    role: reference
    title: CheckingForNull
  - instance: apache
    page_id: '120730642'
    page_owner: human
    role: reference
    title: IfNullDirective
owners: []
provenance:
  created_by: kn-new
status: active
summary: VTL의 $variable, ${variable} 표현식을 컨텍스트에서 조회해 문자열로 변환한다. null이면 리터럴 텍스트로 출력하거나
  이벤트 핸들러가 처리한다.
title: 변수 참조 해석 ($variable)
type: feature
---

## 목적

`$name`, `${user.email}`, `$!nullSafe` 같은 VTL 참조를 컨텍스트에서 조회하고 `toString()`으로 변환해 출력 스트림에 삽입한다.

## 동작 방식

1. 파서가 `$` 참조 노드 생성
2. 렌더링 시 `InternalContextAdapter.get(key)` 호출
3. 점(`.`) 체인(`$user.address.city`)은 `Uberspector`가 리플렉션으로 순차 접근
4. `ReferenceInsertionEventHandler`로 삽입 전 값 변환 가능
5. null이면 `$variable` 리터럴 출력 (또는 `$!variable` 형식으로 빈 문자열)

## 사용 예시

```vtl
## 단순 참조
Hello $name

## 중괄호 (인접 텍스트 구분)
${product}s

## null-safe ($! : null이면 빈 문자열)
$!user.middleName

## 중첩 프로퍼티 체인
$order.customer.address.city
```

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->