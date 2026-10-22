# 시스템 지식 지도

이 폴더는 `kn`이 관리하는 지식 지도입니다.

- `index.md`: 갈래 목록 (자동 생성, `kn index`). 갈래마다 `<갈래>/_index.md`에 항목 목록
- `paths.md`: 경로 역인덱스 (자동 생성, `kn index`)
- `schema.md`: 작성 규칙 — Claude Code와 사람이 함께 읽는 규약
- `sources.yaml`: 연동 레지스트리와 정책 (직접 편집)
- `knowledge-types.yaml`: 지식 유형 설정
- `roles.yaml`: 역할자 목록

> 자동 생성 파일(`index.md`, `_index.md`, `paths.md`)은 직접 고치지 마세요.
> `kn index`로 다시 생성합니다.
