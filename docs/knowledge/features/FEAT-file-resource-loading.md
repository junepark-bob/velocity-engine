---
agreement: ''
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/loader/FileResourceLoader.java
components: []
confluence: []
git_docs: []
id: FEAT-file-resource-loading
jira: []
links:
  confluence:
  - instance: apache
    page_id: '120730675'
    page_owner: human
    role: reference
    title: StructuredGlobbingResourceLoader
  - instance: apache
    page_id: '120730647'
    page_owner: human
    role: reference
    title: JpaResourceLoader
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
    key: VELOCITY-909
    relation: changed-by
  - instance: apache
    key: VELOCITY-916
    relation: changed-by
owners: []
provenance:
  code_fingerprint: sha256:e6f3bd7ab8ace036cc460dc03622a340d68cfe16142b6bc07f890820cc800fa0
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: FileResourceLoader가 파일시스템 경로에서 .vm 템플릿을 로드한다. 기본 로더이며 수정 감지 후 자동 재로딩을 지원한다.
title: 파일시스템 리소스 로딩
type: feature
---

## 목적

로컬 파일시스템의 `.vm` 파일을 읽어 `Template`으로 제공한다. 개발 중 템플릿 수정 후 서버 재시작 없이 자동 반영하는 핫 리로드 용도로도 사용된다.

## 동작 방식

1. `file.resource.loader.path` 설정으로 검색 루트 경로 지정 (복수 가능)
2. `getTemplate("sub/template.vm")` → 설정된 루트들을 순서대로 탐색
3. `file.resource.loader.cache=true` 시 파일 수정 시간(`lastModified`) 비교로 변경 감지
4. `file.resource.loader.modificationCheckInterval` (초 단위)로 폴링 주기 설정

## 사용 예시

```java
// 설정
Properties p = new Properties();
p.setProperty("file.resource.loader.path", "/opt/templates,/app/views");
p.setProperty("file.resource.loader.cache", "true");
p.setProperty("file.resource.loader.modificationCheckInterval", "10");
ve.init(p);

// 로딩
Template t = ve.getTemplate("emails/welcome.vm");
```

```
# 파일 구조
/opt/templates/
  emails/
    welcome.vm
```

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->