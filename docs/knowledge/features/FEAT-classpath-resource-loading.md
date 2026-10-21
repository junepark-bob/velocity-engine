---
agreement: ''
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/loader/ClasspathResourceLoader.java
components: []
confluence: []
git_docs: []
id: FEAT-classpath-resource-loading
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
  code_fingerprint: sha256:bf80387551f0acd31bf4a53a0b70852f3fcb47dd76e96c4d83272f765a8a2956
  created_by: kn-new
  fingerprint_commit: 6d21dbf7
  sources_of_knowledge: []
related: []
status: active
summary: ClasspathResourceLoader가 클래스패스(JAR 내부 포함)에서 .vm 파일을 로드한다. 배포 시 JAR 안에 템플릿을
  패키징하는 표준 방식이다.
title: 클래스패스 리소스 로딩
type: feature
---

## 목적

JAR 파일 내 `resources/` 디렉토리에 패키징된 `.vm` 템플릿을 런타임에 로드한다. Spring Boot 실행 가능 JAR처럼 템플릿을 배포 산출물 안에 포함할 때 사용한다.

## 동작 방식

1. `resource.loaders=classpath` 또는 `class` 로더 등록
2. `getTemplate("templates/report.vm")` → `ClassLoader.getResourceAsStream("templates/report.vm")`
3. JAR 내 리소스는 변경 불가이므로 캐시 무효화 없음 (항상 캐시 사용)

## 사용 예시

```java
Properties p = new Properties();
p.setProperty("resource.loaders", "classpath");
p.setProperty("resource.loader.classpath.class",
    "org.apache.velocity.runtime.resource.loader.ClasspathResourceLoader");
ve.init(p);

Template t = ve.getTemplate("templates/report.vm");
```

```
# Maven/Gradle 프로젝트 리소스 위치
src/main/resources/
  templates/
    report.vm    →  클래스패스: templates/report.vm
```

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->