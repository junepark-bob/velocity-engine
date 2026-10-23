# 지식 항목 작성 규칙 (schema.md)

Claude Code가 지식 항목을 읽거나 작성하거나 검토할 때 따르는 규칙 요약.

## 지도를 읽는 순서 (설계 08 §3, K84·K86)

0. 질문·작업의 의도로 경로를 고른다. **코드 사실**(무엇이·어떻게 동작하나)이면 지도를 읽지 않고 바로 코드를 찾는다
1. **이유·이력·결정, 문서·이슈·담당 위치**를 물으면 `kn search <키워드>`로 항목을 찾는다
2. **구조·온보딩**처럼 키워드가 없으면 `index.md`(갈래 목록)를 읽고, 질문에 맞는 **갈래의 `_index.md`만** 읽은 뒤 필요한 항목만 연다. 다른 갈래는 읽지 않는다. 같은 세션에서 읽은 파일은 다시 읽지 않는다(파일이 바뀐 경우만)
3. **코드를 바꿀 때**는 바꿀 파일마다 `kn paths <파일>`(또는 kn-mcp `knowledge_for_path`)로 그 파일에 걸린 항목만 찾는다
4. 관련 항목 파일을 읽는다. ⚠ 주의 표시가 있는 지식은 그대로 믿지 않는다
5. 외부 문서의 내용이 필요하면 kn-mcp `source_page_summary`로 그때 읽는다(Git에는 제목·링크만 있다)
6. 답하거나 코드를 바꿀 때 근거가 된 항목 ID를 밝힌다. 코드를 바꿨으면 작업을 끝내기 전에 `/kn:delta`

목차 세 단계: `index.md`(갈래 목록) → `<갈래>/_index.md`(항목 ID·제목·한 줄 요약·주의) → 항목 파일. 모두 `kn index`가 만든다.

## front matter 필수 필드

- `id`: 타입 접두어 + 슬러그 (예: `FEAT-billing-integration`)
- `type`: architecture | component | feature | domain-rule | decision | guide | contract | ...
- `title`: 제목
- `summary`: 1~2문장. **목적과 맥락만.** 코드와 저장소 문서에서 나온 내용만 (§5.3). **첫 문장**이 목차의 한 줄 요약이 되며 60자를 넘으면 잘린다

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

- 항목 하나 약 800토큰 이내(어림: ASCII 3자 ≈ 1토큰, 그 밖 1자 ≈ 1토큰). 넘으면 `kn lint`가 `ITEM_TOO_LONG` 경고를 내니 본문을 나누거나 상세는 연결 문서로 둡니다.

## kn:generated 구역

`kn`이 재생성하는 구역. 사람이 고치지 않습니다.

```html
<!-- kn:generated:start source=code-facts -->
...
<!-- kn:generated:end -->
```
