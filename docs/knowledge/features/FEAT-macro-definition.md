---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Macro.java
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/RuntimeMacro.java
components: []
id: FEAT-macro-definition
links:
  confluence:
  - instance: apache
    page_id: '120730655'
    page_owner: human
    role: design
    title: MacroEvaluationStrategy
  - instance: apache
    page_id: '120730631'
    page_owner: human
    role: reference
    title: GenericVelocimacros
  - instance: apache
    page_id: '120730681'
    page_owner: human
    role: reference
    title: VelocimacroLibrary
  jira:
  - instance: apache
    key: VELOCITY-789
    relation: changed-by
  - instance: apache
    key: VELOCITY-776
    relation: changed-by
  - instance: apache
    key: VELOCITY-797
    relation: changed-by
  - instance: apache
    key: VELOCITY-917
    relation: changed-by
  - instance: apache
    key: VELOCITY-916
    relation: changed-by
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:731b8a848b29ceb2946fc60a6f6b82b11fc3e56f302cb505963a52042ba966cd
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: 재사용 가능한 VTL 블록을 매크로로 정의한다. 파라미터를 받아 인라인·글로벌 범위로 사용할 수 있으며 Java의 메서드 정의와 유사하다.
title: '#macro 매크로 정의'
type: feature
---

## 목적

반복 사용되는 VTL 렌더링 블록을 이름과 파라미터가 있는 매크로로 캡슐화한다. HTML 컴포넌트, 공통 테이블 행, 반복 헤더 등에 활용한다.

## 동작 방식

1. `#macro(이름 $파라미터...)...#end` 로 정의
2. `#이름($arg)` 형태로 호출 (일반 지시어처럼)
3. 정의 위치: 같은 템플릿 내(인라인), 별도 `.vm` 파일(글로벌, `velocimacros.vm`)
4. `velocimacros.library` 설정으로 글로벌 매크로 라이브러리 파일 지정

## 사용 예시

```vtl
## 매크로 정의
#macro(renderTag $tag $content)
<$tag>$content</$tag>
#end

## 사용
#renderTag("h1" $title)
#renderTag("p" $body)

## 파라미터 여러 개
#macro(tableRow $label $value $class)
<tr class="$class"><td>$label</td><td>$value</td></tr>
#end
```

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->