---
agreement: ''
aliases: []
classification: public
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/loader/ClasspathResourceLoader.java
components: []
id: FEAT-classpath-resource-loading
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
owners:
- role:tech-lead
provenance:
  code_fingerprint: sha256:bf80387551f0acd31bf4a53a0b70852f3fcb47dd76e96c4d83272f765a8a2956
  created_by: kn-new
  fingerprint_commit: 8dd49ad1
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
## 상세 문서

<!-- kn:generated:start source=links -->
- [StructuredGlobbingResourceLoader](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730675) — reference
- [JpaResourceLoader](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730647) — reference
- [VELOCITY-789](https://issues.apache.org/jira/browse/VELOCITY-789) — changed-by
- [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776) — changed-by
- [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797) — changed-by
- [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909) — changed-by
- [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916) — changed-by
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2026-09-15: Resource loaders now enforce templates paths to stay in their configured root (16a69933)
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
- 2019-09-08 [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916): Add a second effect for the debugging flag runtime.log.track_location: display V… (5782c4cf)
- 2019-03-10 [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909): [engine][VELOCITY-909] Propagate propnames changes thorough javadoc; some more r… (fec80129)
- 2017-02-20: [engine] several coding style fixes (Michael remarks) (95aeb9d5)
- 연결된 JIRA: [VELOCITY-789](https://issues.apache.org/jira/browse/VELOCITY-789), [VELOCITY-776](https://issues.apache.org/jira/browse/VELOCITY-776), [VELOCITY-797](https://issues.apache.org/jira/browse/VELOCITY-797), [VELOCITY-909](https://issues.apache.org/jira/browse/VELOCITY-909), [VELOCITY-916](https://issues.apache.org/jira/browse/VELOCITY-916)
<!-- kn:generated:end -->