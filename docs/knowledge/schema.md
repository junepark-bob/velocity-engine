# 지식 항목 작성 규칙 (schema.md)

Claude Code가 지식 항목을 작성하거나 검토할 때 따르는 규칙 요약.

## front matter 필수 필드

- `id`: 타입 접두어 + 슬러그 (예: `FEAT-billing-integration`)
- `type`: architecture | component | feature | domain-rule | decision | guide | contract | ...
- `title`: 제목
- `summary`: 1~2문장. **목적과 맥락만.** 코드와 저장소 문서에서 나온 내용만 (§5.3)

## 필드 소유권 (02 §5.2)

| 필드 | 쓰는 주체 |
|---|---|
| `id`, `type` | 생성 시 kn-init·kn-delta |
| `title`, `status`, `summary`, `code` | AI 스킬 (PR에서 사람이 리뷰) |
| `owners`, `classification`, `agreement` | **사람** (AI는 제안만) |
| `provenance.*`, `links.*.synced_*` | **kn만** — 직접 고치면 경고 |
| `kn:generated` 구역 | **kn만** — 직접 고치면 거부됨 |

## 요약에 쓸 수 있는 원천 (02 §5.3)

| 원천 | 허용 |
|---|---|
| 코드, 저장소 안의 문서 | ✔ |
| 외부 문서(Confluence·JIRA) | ✘ 내용 금지. 제목·링크만 |
| 분류 `confidential` 항목 | 제목·링크만 |

## append-only 유형

`decision`, `contract`, `agreement`: 기존 줄을 고치거나 삭제하지 않는다.
새 결정이 생기면 새 ADR을 만들고 이전 ADR에 `superseded_by`만 추가한다.

## 항목 크기

- 항목 하나 150줄 이내. 넘으면 하위 항목으로 나눕니다.

## kn:generated 구역

`kn`이 재생성하는 구역. 사람이 고치지 않습니다.

```html
<!-- kn:generated:start source=code-facts -->
...
<!-- kn:generated:end -->
```
