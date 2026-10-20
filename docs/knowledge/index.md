# 시스템 지식 목록
> 자동 생성 (`kn index`). 직접 고치지 마세요. 항목 22개

## 아키텍처
| ID | 제목 | 요약 | 코드 |
|---|---|---|---|
| ARCH-velocity-engine-core | Velocity Engine Core 아키텍처 | Java 기반 범용 템플릿 엔진. VTL(Velocity Template Language)을 파싱해 컨텍스트 데이터와 병합하여 텍스트를 생성한다 | velocity-engine-core/src/main/java/org/apache/velocity/** |

## 구성 요소
| ID | 제목 | 요약 | 코드 |
|---|---|---|---|
| COMP-context-api | 컨텍스트 API (Context API) | 템플릿에 주입되는 키-값 데이터 컨테이너. Spring MVC의 Model과 동일한 역할로, VTL 변수 조회·저장·체이닝을 담당한다. | velocity-engine-core/src/main/java/org/apache/velocity/context/, velocity-engine-core/src/main/java/org/apache/velocity/VelocityContext.java |
| COMP-directive-engine | 지시어 엔진 (Directive Engine) | #foreach #if #set #macro 등 VTL 지시어를 실행한다. 내장 지시어 외에 커스텀 지시어를 등록할 수 있어 Spring의 Ha | velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/ |
| COMP-event-handler | 이벤트 핸들러 (Event Handler) | 렌더링 생명주기에 훅을 삽입한다. 참조 삽입·잘못된 참조·메서드 예외 등 이벤트를 가로채 로깅·변환·예외 처리를 커스터마이징할 수 있다. | velocity-engine-core/src/main/java/org/apache/velocity/app/event/ |
| COMP-introspection | 인트로스펙션 (Introspection) | 리플렉션으로 Java 객체의 프로퍼티·메서드를 조회한다. OGNL 없이 순수 리플렉션 캐시로 $object.property 접근을 처리하며 Sp | velocity-engine-core/src/main/java/org/apache/velocity/util/introspection/ |
| COMP-parser | JavaCC VTL 파서 | JavaCC로 생성된 VTL 문법 파서를 풀로 관리한다. 파서는 재진입 불가라서 동시 요청마다 별도 인스턴스를 대여하고 반납하는 풀 방식을 사용 | velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserPool.java, velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserPoolImpl.java |
| COMP-resource-loader | 리소스 로더 (Resource Loader) | 파일시스템·클래스패스·JAR·URL 등 다양한 소스에서 .vm 템플릿 파일을 로드하고 캐시한다. Spring의 ResourceLoader 체인과 | velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/, velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/loader/ |
| COMP-runtime-engine | RuntimeInstance 런타임 엔진 | 엔진 초기화와 설정을 보관하는 중앙 조율자. Spring의 ApplicationContext에 해당하며 파서 풀·리소스 관리자·지시어 레지스트리 | velocity-engine-core/src/main/java/org/apache/velocity/runtime/RuntimeInstance.java, velocity-engine-core/src/main/java/org/apache/velocity/runtime/RuntimeServices.java |
| COMP-template-engine | VelocityEngine 템플릿 엔진 | 외부에 노출되는 공개 API 진입점. 템플릿 파싱과 VTL 컨텍스트 병합을 담당하며 Spring MVC의 ViewResolver + View 역 | velocity-engine-core/src/main/java/org/apache/velocity/app/VelocityEngine.java, velocity-engine-core/src/main/java/org/apache/velocity/app/Velocity.java |

## 기능
| ID | 제목 | 요약 | 코드 |
|---|---|---|---|
| FEAT-classpath-resource-loading | 클래스패스 리소스 로딩 | ClasspathResourceLoader가 클래스패스(JAR 내부 포함)에서 .vm 파일을 로드한다. 배포 시 JAR 안에 템플릿을 패키징하는 | velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/loader/ClasspathResourceLoader.java |
| FEAT-custom-parser | 커스텀 파서 설정 | JavaCC 파서의 특수문자(# $ * @)를 변경해 Markdown 등 다른 포맷과 충돌 없이 VTL을 사용할 수 있다. ParserConfi | velocity-engine-core/src/main/java/org/apache/velocity/runtime/ParserConfiguration.java |
| FEAT-file-resource-loading | 파일시스템 리소스 로딩 | FileResourceLoader가 파일시스템 경로에서 .vm 템플릿을 로드한다. 기본 로더이며 수정 감지 후 자동 재로딩을 지원한다. | velocity-engine-core/src/main/java/org/apache/velocity/runtime/resource/loader/FileResourceLoader.java |
| FEAT-foreach-directive | #foreach 반복 지시어 | 컬렉션·배열·맵·이터레이터를 순회하는 VTL 반복 지시어. $velocityCount와 $velocityHasNext 내장 변수로 인덱스·끝 여 | velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Foreach.java, velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/ForeachScope.java |
| FEAT-if-directive | #if 조건 지시어 | VTL 조건 분기 지시어. #if/#elseif/#else/#end로 구성되며 null·false·빈 컬렉션을 모두 false로 평가하는 Vel | velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Block.java |
| FEAT-macro-definition | #macro 매크로 정의 | 재사용 가능한 VTL 블록을 매크로로 정의한다. 파라미터를 받아 인라인·글로벌 범위로 사용할 수 있으며 Java의 메서드 정의와 유사하다. | velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/Macro.java, velocity-engine-core/src/main/java/org/apache/velocity/runtime/directive/RuntimeMacro.java |
| FEAT-spring-integration | Spring Framework 통합 | spring-velocity-support 모듈이 VelocityEngineFactoryBean을 제공해 Spring 빈으로 VelocityEn | spring-velocity-support/src/main/java/org/apache/velocity/spring/ |
| FEAT-string-interpolation | 문자열 보간 (String Interpolation) | 큰따옴표로 감싼 VTL 문자열 리터럴 안에서 $variable을 평가해 값을 삽입한다. 작은따옴표 문자열은 보간하지 않는다. | velocity-engine-core/src/main/java/org/apache/velocity/runtime/ |
| FEAT-template-rendering | VTL 템플릿 렌더링 | VTL 템플릿 파일과 VelocityContext를 병합해 최종 텍스트를 생성하는 핵심 기능. VelocityEngine.merge()가 진입점 | velocity-engine-core/src/main/java/org/apache/velocity/app/VelocityEngine.java |
| FEAT-variable-resolution | 변수 참조 해석 ($variable) | VTL의 $variable, ${variable} 표현식을 컨텍스트에서 조회해 문자열로 변환한다. null이면 리터럴 텍스트로 출력하거나 이벤트 | velocity-engine-core/src/main/java/org/apache/velocity/util/introspection/, velocity-engine-core/src/main/java/org/apache/velocity/context/ |

## 결정 (ADR)
| ID | 제목 | 요약 | 코드 |
|---|---|---|---|
| ADR-javacc-parser | ADR: JavaCC 기반 파서 채택 | VTL 문법 파서를 JavaCC로 구현하고, 특수문자 커스터마이징을 위한 빌드 타임 파서 재생성을 공식 지원한다. | velocity-engine-core/src/main/parser/Parser.jjt |

## 가이드
| ID | 제목 | 요약 | 코드 |
|---|---|---|---|
| GUIDE-velocity-context-best-practices | VelocityContext 사용 모범 사례 | VelocityContext를 안전하고 효율적으로 사용하기 위한 체인·중첩·스레드 안전성 지침. | velocity-engine-core/src/main/java/org/apache/velocity/context/** |

## 계약
| ID | 제목 | 요약 | 코드 |
|---|---|---|---|
| CTR-runtime-properties | Velocity 런타임 설정 속성 계약 | RuntimeConstants.java에 선언된 Velocity 런타임 설정 키·기본값 계약. 키 이름 변경 및 기본값 수정 규칙을 정의한다. | velocity-engine-core/src/main/java/org/apache/velocity/runtime/RuntimeConstants.java |
