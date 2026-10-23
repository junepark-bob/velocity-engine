# 기능 (features)
> 자동 생성 (`kn index`). 직접 고치지 마세요. 항목 10개 · [갈래 목록](../index.md)

| ID | 제목 | 요약 |
|---|---|---|
| FEAT-classpath-resource-loading | 클래스패스 리소스 로딩 | ClasspathResourceLoader가 클래스패스(JAR 내부 포함)에서 .vm 파일을 로드한다. |
| FEAT-custom-parser | 커스텀 파서 설정 | JavaCC 파서의 특수문자(# $ * @)를 빌드 시점에 바꿔 커스텀 파서를 생성하면 Markdown 등 … |
| FEAT-file-resource-loading | 파일시스템 리소스 로딩 | FileResourceLoader가 파일시스템 경로에서 .vm 템플릿을 로드한다. |
| FEAT-foreach-directive | #foreach 반복 지시어 | 컬렉션·배열·맵·이터레이터를 순회하는 VTL 반복 지시어. |
| FEAT-if-directive | #if 조건 지시어 | VTL 조건 분기 지시어. |
| FEAT-macro-definition | #macro 매크로 정의 | 재사용 가능한 VTL 블록을 매크로로 정의한다. |
| FEAT-spring-integration | Spring Framework 통합 | spring-velocity-support 모듈이 VelocityEngineFactoryBean을 제공해 S… |
| FEAT-string-interpolation | 문자열 보간 (String Interpolation) | 큰따옴표로 감싼 VTL 문자열 리터럴 안에서 $variable을 평가해 값을 삽입한다. |
| FEAT-template-rendering | VTL 템플릿 렌더링 | VTL 템플릿 파일과 VelocityContext를 병합해 최종 텍스트를 생성하는 핵심 기능. |
| FEAT-variable-resolution | 변수 참조 해석 ($variable) | VTL의 $variable, ${variable} 표현식을 컨텍스트에서 조회해 문자열로 변환한다. |
