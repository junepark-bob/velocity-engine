---
agreement: ''
aliases: []
classification: public
code:
- spring-velocity-support/src/main/java/org/apache/velocity/spring/
components: []
id: FEAT-spring-integration
links:
  confluence:
  - instance: apache
    page_id: '120730683'
    page_owner: human
    role: guide
    title: VelocityAndSpringStepByStep
  - instance: apache
    page_id: '120730684'
    page_owner: human
    role: reference
    title: VelocityAndSpringTips
owners:
- role:tech-lead
provenance:
  created_by: kn-new
  sources_of_knowledge: []
related: []
status: active
summary: spring-velocity-support 모듈이 VelocityEngineFactoryBean을 제공해 Spring 빈으로 VelocityEngine을
  관리한다. Spring 6/7(Java 17+)과 Spring 5(레거시) 모듈로 분리된다.
title: Spring Framework 통합
type: feature
---

## 목적

Spring IoC 컨테이너에서 `VelocityEngine`을 빈으로 관리하고 `@Autowired`로 주입받을 수 있게 한다. 기존 Spring MVC 프로젝트에서 `VelocityEngine`을 사용하는 레거시 코드베이스 지원이 주 목적이다.

## 동작 방식

`VelocityEngineFactoryBean`이 `FactoryBean<VelocityEngine>`을 구현한다. Spring이 빈 초기화 시 `VelocityEngine.init()`을 자동 호출한다. `SpringResourceLoader`가 Spring `Resource` 추상화를 통해 클래스패스·파일시스템·URL 리소스를 통합 처리한다.

## 사용 예시

```java
// Spring Boot @Configuration
@Bean
public VelocityEngine velocityEngine() throws VelocityException, IOException {
    VelocityEngineFactoryBean factory = new VelocityEngineFactoryBean();
    Properties p = new Properties();
    p.setProperty("resource.loaders", "classpath");
    p.setProperty("resource.loader.classpath.class",
        "org.apache.velocity.runtime.resource.loader.ClasspathResourceLoader");
    factory.setVelocityProperties(p);
    return factory.createVelocityEngine();
}
```

```xml
<!-- Spring XML (레거시) -->
<bean id="velocityEngine" class="org.apache.velocity.spring.VelocityEngineFactoryBean">
  <property name="velocityProperties">
    <props>
      <prop key="resource.loaders">classpath</prop>
    </props>
  </property>
</bean>
```
## 상세 문서

<!-- kn:generated:start source=links -->
- [VelocityAndSpringStepByStep](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730683) — guide
- [VelocityAndSpringTips](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=120730684) — reference
<!-- kn:generated:end -->

## 변경 이력

<!-- kn:generated:start source=git+jira -->
- 2025-11-01: Avoid using deprecated properties syntax in tests and extension loaders (da719218)
- 2024-09-07 [VELOCITY-943](https://issues.apache.org/jira/browse/VELOCITY-943): Proposed conditional patch to address VELOCITY-943 (#51) (977b3881)
- 2024-08-23: Normalize some tab-indented source files (08211a61)
- 2023-08-13 [VELOCITY-974](https://issues.apache.org/jira/browse/VELOCITY-974): Use non-deprecated config property for resource loaders in VelocityEngineFactory (d5c52e90)
- 2021-02-25: A lot of almost purely cosmetic code cleanups (836d28fa)
<!-- kn:generated:end -->