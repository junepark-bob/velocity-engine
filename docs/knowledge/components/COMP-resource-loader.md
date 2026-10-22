---
aliases: []
classification: internal
code:
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/
- velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/loader/
id: COMP-resource-loader
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
owners:
- role:tech-lead
provenance:
  created_by: kn-new
status: active
summary: 파일시스템·클래스패스·JAR·URL 등 다양한 소스에서 .vm 템플릿 파일을 로드하고 캐시한다. Spring의 ResourceLoader
  체인과 유사한 다중 로더 구조를 가진다.
title: 리소스 로더 (Resource Loader)
type: component
---

## 역할

`ResourceManager`가 여러 `ResourceLoader` 인스턴스를 체인으로 묶어 템플릿 파일을 찾는다. 첫 번째 로더에서 못 찾으면 다음 로더로 넘어간다. `ResourceCache`가 파싱된 `Template` AST를 캐시해 반복 요청 성능을 높인다.

## 주요 클래스·인터페이스

| 클래스/인터페이스 | 역할 |
|---|---|
| `ResourceLoader` | 모든 로더의 추상 기반 클래스 |
| `FileResourceLoader` | 파일시스템 경로에서 `.vm` 로드. 기본 로더 |
| `ClasspathResourceLoader` | 클래스패스 내 리소스 로드 (JAR 내 포함) |
| `JarResourceLoader` | JAR 파일 내 `.vm` 직접 로드 |
| `StringResourceLoader` | 문자열로 직접 템플릿 등록 (테스트·동적 생성 용) |
| `DataSourceResourceLoader` | DB에서 템플릿 로드 |
| `ResourceManager` / `ResourceManagerImpl` | 로더 체인 + 캐시 조율 |
| `ResourceCache` / `ResourceCacheImpl` | 파싱된 AST 캐시 |

## 다른 컴포넌트와의 관계

- `RuntimeInstance` → `ResourceManager`: 초기화 시 설정된 로더 등록
- `Template` → `ResourceLoader`: 파일 내용(InputStream) 요청
- `ResourceCache` ↔ `Template`: AST 저장·조회
- Spring 통합 → `SpringResourceLoader`: Spring `Resource` 추상화 기반 로더 추가

<!-- kn:generated:start source=git-log -->
<!-- kn:generated:end -->