# Blank Line Rules (Obsidian-tight Markdown)

Obsidian 편집기에서 사용자는 **빈 줄을 최소화한 tight 마크다운** 을 선호한다. AI agent 가 Write/Edit 시 헤딩·리스트·콘텐츠 사이에 습관적으로 빈 줄을 추가하면, 사용자가 매번 수동으로 제거해야 한다.

## Rule (Default: Tight)

**기본은 빈 줄 없음.** 빈 줄이 *명시적으로 의미 있는* 경우에만 삽입한다.

### ❌ 빈 줄 넣지 말 것

| 위치 | 예시 |
|------|------|
| `##` 바로 다음에 `###` | `## Bible` ↵ `### Main Text` (빈 줄 없음) |
| `###` 바로 다음에 콘텐츠 (callout, blockquote, table) | `### Main Text` ↵ `> [!bible]+ ...` |
| `####` 바로 다음에 리스트 | `#### 한국어` ↵ `- **십계명**` |
| 리스트 끝 다음에 `####` | `- ...뉘앙스` ↵ `#### 영어` |
| `####` 다음에 인라인 텍스트 | `#### Section` ↵ `텍스트 시작` |

### ✅ 빈 줄 넣어도 OK (의미 있는 분리)

| 위치 | 이유 |
|------|------|
| `---` 구분선 앞뒤 | 시각적 단락 분리 |
| `##` 앞 (이전 섹션과 구분) | major section 분리 |
| `##` 다음에 본문 standalone blockquote | 인용이 본문처럼 기능할 때 |
| 콜아웃 (`> [!info]`) 앞뒤 | 박스가 독립 요소 |
| **연속된 콜아웃 사이 (필수)** | **빈 줄 없으면 다음 콜아웃이 앞 콜아웃 안으로 빨려 들어가 하나로 합쳐짐 (겹침 렌더 에러)** |
| `###` 와 `####` 사이 (intro 후 sub-section 시작) | 한 단계 깊이 들어갈 때 시각적 호흡 |

### ⚠️ 연속 콜아웃은 반드시 빈 줄로 분리 (Callout Separation)

`> [!quote]+` 같은 콜아웃을 두 개 이상 연달아 쓸 때, 사이에 **빈 줄(`>` 없는 진짜 빈 줄)** 이 없으면 Obsidian 이 둘째 콜아웃의 `[!quote]+ [[...]]` 헤더 줄까지 *첫째 콜아웃의 내용*으로 파싱한다. 결과: 두 박스가 하나로 겹쳐 렌더되고 `[!quote]+` 라벨이 본문 텍스트로 노출됨.

```markdown
❌ Bad — 두 콜아웃이 하나로 겹침
> *— [[이남정]] 목사 발췌*
> [!quote]+ [[다음 책]]
> ...

✅ Good — 빈 줄로 분리
> *— [[이남정]] 목사 발췌*

> [!quote]+ [[다음 책]]
> ...
```

이는 "헤딩→콘텐츠 tight" 규칙의 *예외* 다. 콜아웃은 독립 블록이므로 인접 콜아웃 사이에는 빈 줄이 **필수**.

## Examples

### ❌ Bad (AI가 흔히 만드는 형태)

```markdown
## Bible

### Main Text

> [!bible]+ ...

[[Exodus]]

### Reference Verse

-

---

## 새로운 여정

### 십계명의 어원과 의미

#### 한국어 / 한자

- **십계명 (十誡命)**
	- 十(열 십)

#### 영어 (English)

- **Ten Commandments**
```

### ✅ Good (사용자 선호 형태)

```markdown
## Bible
### Main Text
> [!bible]+ ...

[[Exodus]]
### Reference Verse
-

---

## 새로운 여정

### 십계명의 어원과 의미

#### 한국어 / 한자
- **십계명 (十誡命)**
	- 十(열 십)
#### 영어 (English)
- **Ten Commandments**
```

## Rule of Thumb

> "헤딩과 그 다음 첫 콘텐츠 (또는 sub-heading) 사이에는 빈 줄을 두지 않는다. 리스트 끝과 다음 헤딩 사이에도 두지 않는다. 빈 줄은 `---`, `##` 단락 분리, 독립 콜아웃 정도에만 쓴다."

이 룰은 Markdown 사양 위반이 아니다 — Obsidian/CommonMark 모두 빈 줄 없이 헤딩→콘텐츠 전환을 정상 파싱한다. 단지 사용자의 시각적 선호이며, vault 일관성을 위해 따른다.

## Anti-pattern

```markdown
❌ ## Section
❌
❌ ### Subsection
❌
❌ - item
```

```markdown
✅ ## Section
✅ ### Subsection
✅ - item
```
