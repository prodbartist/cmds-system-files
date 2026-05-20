---
type: documentation
aliases:
  - System Files Changelog
  - 시스템 파일 변경 로그
description: Central version history for the 5 core CMDS system files (CLAUDE.md, AGENTS.md, CMDS.md, CMDS Guide, CMDS Head Quarter). Tracks schema changes, architecture upgrades, and frontmatter standard evolution. Reference when auditing version lineage or planning migrations.
author:
  - "[[구요한]]"
date created: 2026-04-01T11:30
date modified: 2026-05-04T00:10
tags: [CMDS, system, changelog]
CMDS: "[[📚 501 Obsidian]]"
---

# CMDS System Files — Changelog

> 공개 배포되는 5개 시스템 파일(CLAUDE.md, AGENTS.md, CMDS.md, 🏛 CMDS Head Quarter, 🏛 CMDS Guide)의 변경 이력을 추적합니다. 볼트 내부에는 추가로 3개 비공개 시스템 파일(ANTIGRAVITY.md, BRAIN.md, BRAIN_PROMPT.md)이 있어 총 8개로 운영되며, 이 3개는 vendor·product 전용이라 외부 배포 대상이 아닙니다.

## 📐 2-Layer Version System

이 changelog 는 **2-layer 버전 시스템**의 매크로 레이어:

| Layer | 단위 | 위치 | 예시 |
|-------|------|------|------|
| 🌐 **매크로 (시스템 전체)** | Vercel 배포 스냅샷 | **이 CHANGELOG.md** | v4.5, v4.5.1 |
| 🔬 **마이크로 (파일별)** | 각 파일의 evolution | 각 파일 frontmatter `version:` | CLAUDE 3.8, CMDS 2.5, ... |

각 매크로 entry 에는 **그 시점의 8 files version snapshot matrix** 를 포함해 마이크로 ↔ 매크로 매핑이 명시됩니다.

---

## v4.7.0 — 2026-05-20 (CMDS.md Diet · System Files Dedup · 5-Way Sync)

**트리거**: 사용자 지적 — *"CMDS.md 캐릭터 너무 많다"*. 전체 8 system file 검증 후 CMDS.md 가 43,856자 / 883줄로 비대화 확인. 주요 원인은 다른 파일과의 중복 콘텐츠 (Working Environments 4중복, Key Directories vs `.claude/rules/directory-structure.md`, Command Suite 상세 vs CLAUDE.md, Quick Reference 표 vs 본문 9 카테고리).

**왜 v4.7.0 (minor) 인가**: 단순 cleanup 이 아니라 **CMDS.md 의 정체성 재정의** — "철학·사용자·9 카테고리·CMDS Process 의 정본" 으로 좁히고, "기술 정본" 은 CLAUDE.md / `.claude/rules/` 로 위임. 다른 시스템 파일 (CLAUDE / Guide) 도 stray tag 정리. 또한 **5-way sync 패턴 도입** (기존 4-way 에 GitHub push 단계 명시 추가).

### File Version Snapshot

| File | Version | Δ from v4.6.0 |
|------|:-------:|:-------------:|
| CLAUDE.md | **4.0** | ⬆ 3.9 → 4.0 (tags `[CMDS, system, 1, 2]` → `[CMDS, system]`, 3.8 changelog 가 claim 했지만 실제 미적용된 수정을 진짜로 반영) |
| AGENTS.md | 2.5 | — (header 날짜만 갱신) |
| ANTIGRAVITY.md | 2.0 | — (header 날짜만 갱신) |
| CMDS.md | **2.6** | ⬆ 2.5 → 2.6 (**Moderate diet**: 43,856 → 33,519 chars, -23.6%) |
| 🏛 CMDS Guide.md | **2.6** | ⬆ 2.5 → 2.6 (tags noise 5개 제거: `태그는자유로워야지`, `maps`, `example`, `service`, `index`) |
| 🏛 CMDS Head Quarter.md | 1.4 | — (header 날짜만 갱신) |
| BRAIN.md *(internal)* | (Gobi-managed) | — |
| BRAIN_PROMPT.md *(internal)* | (Gobi-managed) | — |

### CMDS.md Diet (Moderate ~28k 목표, 결과 33.5k)

- ❌ **삭제**: Working Environments & Sync · Public Deployment 섹션 — CLAUDE.md / AGENTS.md / ANTIGRAVITY.md 와 4중복
- ❌ **삭제**: Key Directories & Their Roles (~100줄) — `.claude/rules/directory-structure.md` 가 정본
- ❌ **삭제**: Command Suite 상세 (28줄) — CLAUDE.md "CMDS Process Command Suite" 가 정본 → 1단락 요약 + 링크
- ❌ **삭제**: Quick Reference 카테고리 표 — 본문 9 카테고리와 자체 중복
- 🔻 **축약**: System Documentation Overview — When to Reference + Quick Decision Tree 를 한 줄 routing block 으로
- 🔻 **축약**: Note Properties & Metadata — 스키마는 [[🏛 CMDS Guide]] 와 frontmatter-standard 로 위임
- 🔄 **갱신**: Vault Statistics 날짜 (2026-03-15 → 2026-05-20)
- ✅ **유지**: 9 카테고리 전문 (사용자 결정) · Workflow Patterns · Understanding User Intent · Guiding Principles

### Header Sync (전체 6개 public-deployable files)

모든 헤더 `Last Updated` 와 frontmatter `date modified` 를 **2026-05-20** 으로 통일. 이전 상태: CLAUDE 2026-05-04, 나머지 2026-05-03 ~ 2026-05-05 혼재.

### Sync Process Upgrade: 4-way → 5-way

스킬 `system-docs-updater` 의 `All-in-One Sync Command` 가 기존 ① backup → ② share → ③ DEV → ④ Vercel 4단계였는데, **④ GitHub push 를 명시적 단계로 추가**해 5-way 로 확장. 사용자 mental model "백업 → 동기화 → github → 홈페이지" 와 1:1 매핑. GitHub repo 는 Vercel 자동배포 없음을 다시 명시 (사고 패턴 #2 재발 방지).

### Install Snapshot (v4.7.0 기준)

```bash
curl -O https://system.cmdspace.work/files/CMDS-System-Files.zip
unzip CMDS-System-Files.zip
git clone --branch v4.7.0 https://github.com/johnfkoo951/cmds-system-files.git
```

---

## v4.6.0 — 2026-05-13 (Design System Surface + Share Folder Catch-Up)

**트리거**: Google Stitch 의 `DESIGN.md` 패턴([google-labs-code/design.md](https://github.com/google-labs-code/design.md)) 도입 결정 + 5/4-5 vault 편집이 share 폴더로 sync 안 된 채 ~9일 stale 상태 발견 (사고 패턴 #2 재발).

**왜 v4.6.0 (minor) 인가**: 이번 릴리즈는 단순 catch-up 이 아니라 **새 public surface 추가**. `DESIGN.md` 와 `design-tokens.json` 은 *AI 코딩 에이전트가 CMDS 디자인 시스템을 직접 학습할 수 있는 새 진입점* 이고, Claude 디자인 시스템·Figma Tokens Studio·Style Dictionary 등 외부 도구가 fetch 하는 정본이 됨. patch (v4.5.4) 가 아니라 minor bump 가 의미상 맞음.

### File Version Snapshot

| File | Version | Δ from v4.5.3 |
|------|:-------:|:-------------:|
| CLAUDE.md | 3.9 | — |
| AGENTS.md | 2.5 | — |
| ANTIGRAVITY.md | 2.0 | — |
| CMDS.md | 2.5 | — |
| 🏛 CMDS Guide.md | 2.5 | — |
| 🏛 CMDS Head Quarter.md | 1.4 | — |
| BRAIN.md *(internal)* | (Gobi-managed) | — |
| BRAIN_PROMPT.md *(internal)* | (Gobi-managed) | — |

(8 파일 micro 버전 무변경 — 이번 매크로 bump 는 *기존 파일 변경* 이 아니라 *새 자산 추가* 와 *share 폴더 catch-up* 이 트리거. 5/4-5 vault 편집은 의도적으로 micro bump 안 친 minor edit 들로 처리됨.)

### Added

- **`DESIGN.md`** — Google `design.md` alpha spec 준수. YAML frontmatter (colors / typography / rounded / spacing / layout / components) + canonical section order markdown body. CMDS Green/Pink 듀얼 모드, SF Pro + Pretendard 타이포 시스템 정본화.
- **`design-tokens.json`** — DTCG / Tokens Studio for Figma 호환. light/dark 모드를 별도 token set 으로 분리, `{core.*}` alias 로 brand palette 참조. Figma Variables 자동 import 가능.

### Fixed (share folder drift — 사고 패턴 #2 재발 대응)

5/4 share 스냅샷 (May 4 20:12) 이후 vault 에서 추가 편집되었지만 `files/` 에 반영 안 된 3개 파일을 catch-up sync:

- `files/CLAUDE.md` (vault 5/4 22:10) — ~2h drift
- `files/CMDS-Guide.md` (vault 5/5 12:57) — ~17h drift
- `files/CMDS-Head-Quarter.md` (vault 5/4 21:39) — ~1.5h drift
- `files/CMDS-System-Files.zip` 재생성 (75139 B → 75258 B) — 5 files + 8 rules 반영

### Distribution Policy (재확인)

8개 system file 중 **공개 5개만** `files/` 에 포함:
- ✅ 공개: CLAUDE.md / AGENTS.md / CMDS.md / 🏛 CMDS Guide / 🏛 CMDS Head Quarter
- ❌ 비공개 (vendor / persona): ANTIGRAVITY.md (Gemini 전용) / BRAIN.md / BRAIN_PROMPT.md (Gobi 전용)

이번 릴리즈에서 ANTIGRAVITY.md 를 share 에 추가할지 검토했으나, CMDS.md 의 분배 정책에 따라 *vendor-specific* 으로 분류해 비공개 유지 결정.

### Install Snapshot (v4.6.0 기준)

```bash
# 풀 ZIP 다운로드
curl -O https://system.cmdspace.work/files/CMDS-System-Files.zip
unzip CMDS-System-Files.zip
# → CLAUDE.md, AGENTS.md, CMDS.md, CMDS-Guide.md, CMDS-Head-Quarter.md + rules/ (8개)

# 또는 GitHub tag 로 고정
git clone --branch v4.6.0 https://github.com/johnfkoo951/cmds-system-files.git
# (tag 는 이 commit 에서 생성됨)

# 디자인 시스템 자산 (이번 릴리즈에 신설)
curl -O https://system.cmdspace.work/DESIGN.md
curl -O https://system.cmdspace.work/design-tokens.json
```

### Sequencing Rule 적용 결과

v4.5 에서 도입한 *deploy 후 변경은 반드시 재배포* 룰에 따라 이번 catch-up + DESIGN.md 추가도 모두 `vercel deploy --prod` 로 라이브 반영 완료. live label `v4.6.0 · 2026-05-13` 까지 동시 갱신.

---

## v4.5.3 — 2026-05-04 (Landing Page Version Label Sync)

**트리거**: 사용자 스크린샷 — system.cmdspace.work 랜딩 페이지에 *"CMDS v4.3 · 2026-04-19 업데이트"* 배지가 stale. 시스템 파일은 v4.5.2 까지 잘 따라왔으나, **랜딩 페이지 / 문서 페이지의 버전 라벨은 별개의 수동 갱신 대상** 이라 누락. 사고 패턴 #4 = "marketing surface drift".

### File Version Snapshot

| File | Version | Δ from v4.5.2 |
|------|:-------:|:-------------:|
| CLAUDE.md | 3.9 | — |
| AGENTS.md | 2.5 | — |
| ANTIGRAVITY.md | 2.0 | — |
| CMDS.md | 2.5 | — |
| 🏛 CMDS Guide.md | 2.5 | — |
| 🏛 CMDS Head Quarter.md | 1.4 | — |
| BRAIN.md *(internal)* | (Gobi-managed) | — |
| BRAIN_PROMPT.md *(internal)* | (Gobi-managed) | — |

(시스템 파일 무변경 — 랜딩/문서 페이지만 갱신)

### Changes

**`DEV/index.html`** (4 patches):
- 버전 배지 EN: `v4.3 · Updated 2026-04-19` → `v4.5.2 · Updated 2026-05-04`
- 버전 배지 KO: `v4.3 · 2026-04-19 업데이트` → `v4.5.2 · 2026-05-04 업데이트`
- "seven shared rules" → "eight shared rules" (4 occurrences in EN: meta description, og:description, twitter:description, hero lede)
- "일곱 개의 공유 규칙" → "여덟 개의 공유 규칙" (KO hero lede)

**`DEV/docs/index.html`** (7 patches):
- title / og:title / og:image:alt / twitter:title / twitter:image:alt / brand-version: `v4.3` → `v4.5.2`
- hero-eyebrow: `CMDS · 2026-04-19 · v4.3` → `CMDS · 2026-05-04 · v4.5.2`

### 사고 패턴 #4 명시 + 누락 방지

`SKILL.md` 의 Pre-Deploy Checklist 에 **"랜딩 페이지 버전 라벨" 항목 신설** (4-way sync 의 0번째 단계 격으로 격상). 매크로 version 바뀔 때마다 grep 로 `v4\.[0-9]` / `2026-` / `seven|eight|일곱|여덟` 패턴 sweep 의무화.

→ "5 destinations sync" 가 사실은 **6번째 surface (마케팅 랜딩) 까지 포함해야** 완전했음. v4.5.3 이후로는 marketing surface 까지 7-way 정렬.

---

## v4.5.2 — 2026-05-04 (2-Layer Version System Formalized)

**트리거**: 사용자 질문 — *"파일마다 버전 넘버가 다른 게 괜찮나? 전체 버전은 어디에서 관리해?"* — 정당한 지적이지만 답이 묵시적으로만 존재했음. 이번에 명시적 시스템화.

### File Version Snapshot

| File | Version | Δ from v4.5.1 |
|------|:-------:|:-------------:|
| **CLAUDE.md** | **3.9** | ⬆ 3.8 → 3.9 |
| AGENTS.md | 2.5 | — |
| ANTIGRAVITY.md | 2.0 | — |
| CMDS.md | 2.5 | — |
| 🏛 CMDS Guide.md | 2.5 | — |
| 🏛 CMDS Head Quarter.md | 1.4 | — |
| BRAIN.md *(internal)* | (Gobi-managed) | — |
| BRAIN_PROMPT.md *(internal)* | (Gobi-managed) | — |

### Changes

- **CHANGELOG.md** 상단에 "📐 2-Layer Version System" 섹션 추가 — 매크로(이 changelog) vs 마이크로(파일별 frontmatter `version:`) 구분 명시
- **모든 매크로 entry 에 File Version Snapshot matrix 의무화** — v4.5.2/v4.5.1/v4.5/v4.4 까지 backfill 완료 (이전은 추정값으로 표기)
- **SKILL.md** (system-docs-updater) 에 매트릭스 템플릿 + 버전 번호 규칙 (매크로 = `v{maj}.{min}.{patch}`, 마이크로 = `{maj}.{min}`) 추가
- **CLAUDE.md v3.9**: "📦 System Files Deployment" 섹션에 2-Layer Version System 표 명시. 다음 LLM 세션이 자동으로 매크로/마이크로 구분 인지

### Why 2 Layers (정당화)

| Layer | 답하는 질문 | 비유 |
|-------|------------|------|
| 🌐 매크로 (CHANGELOG) | "외부 사용자가 다운받는 ZIP 의 스냅샷 버전?" | `package.json` 의 `"version"` |
| 🔬 마이크로 (frontmatter) | "이 파일이 얼마나 진화했나?" | `node_modules/<lib>/package.json` 의 각 lib version |

둘 다 의미 있고 보완적. 단점은 매핑 추적 — 그래서 매크로 entry 마다 matrix 의무화로 보완.

---

## v4.5.1 — 2026-05-04 (Frontmatter Cleanup)

**트리거**: CLAUDE.md 의 `tags: [CMDS, system, 1, 2]` 에 stray numeric `1, 2` 가 어떤 자동 편집으로 leak. 본문은 무변경, frontmatter만 정상화.

### File Version Snapshot

| File | Version | Δ from v4.5 |
|------|:-------:|:-----------:|
| **CLAUDE.md** | **3.8** | ⬆ 3.7 → 3.8 |
| AGENTS.md | 2.5 | — |
| ANTIGRAVITY.md | 2.0 | — |
| CMDS.md | 2.5 | — |
| 🏛 CMDS Guide.md | 2.5 | — |
| 🏛 CMDS Head Quarter.md | 1.4 | — |
| BRAIN.md *(internal)* | (Gobi-managed) | — |
| BRAIN_PROMPT.md *(internal)* | (Gobi-managed) | — |

### Changes

- CLAUDE.md frontmatter: `tags: [CMDS, system, 1, 2]` → `tags: [- CMDS, - system]` (proper YAML array)
- `1, 2` 는 precedence/audience leak 으로 추정 (이전 자동 편집의 artifact)
- 본문 0 byte 변경, ZIP 74,639 bytes (74,542 에서 +97 bytes — frontmatter 차이만)

---

## v4.5 — 2026-05-04 (4-Way Sync Workflow + Share Folder Restored + Sequencing Rule)

### File Version Snapshot

| File | Version | Δ from v4.4 |
|------|:-------:|:-----------:|
| **CLAUDE.md** | **3.7** | ⬆ 3.5 → 3.7 (3.6 + 3.7 in same cycle) |
| AGENTS.md | 2.5 | — |
| ANTIGRAVITY.md | 2.0 | — |
| CMDS.md | 2.5 | — |
| 🏛 CMDS Guide.md | 2.5 | — |
| 🏛 CMDS Head Quarter.md | 1.4 | — |
| BRAIN.md *(internal)* | (Gobi-managed) | — |
| BRAIN_PROMPT.md *(internal)* | (Gobi-managed) | — |

**트리거 #1 (share folder)**: v4.4 배포 직후 사용자 지적 — `40. Docs/47. CMDS Docs/cmds-system-files-share/` (sanitized 외부 공유본) 가 4월 18일 이후 16일간 stale 상태로 방치됨. 원인은 `system-docs-updater` 스킬의 옛 "Quick Update Command" 가 backup 만 다루고 share 는 별도 섹션으로 분리되어 있어 매번 누락됨. 운영 워크플로 자체를 4-way fan-out 으로 재설계.

**트리거 #2 (sequencing)**: v4.5 첫 배포 후 CHANGELOG.md 에 v4.5 entry 추가 → git push → 사용자 지적 "GitHub 은 했으면서 왜 라이브는 안 해?". 원인은 ④ Vercel deploy 가 그 순간의 DEV 폴더 *스냅샷* 을 배포하는데, 그 이후 추가된 콘텐츠는 라이브에 반영 안 됨. GitHub repo 와 Vercel 자동배포 미연결 (수동 CLI 만) 이라 git push 로는 라이브 갱신 불가. → **Sequencing Rule** 명시.

### CLAUDE.md v3.5 → v3.7 (precedence 1)

"📦 System Files Deployment" 섹션 재작성:
- 단순 flow 다이어그램 → **4-way fan-out 다이어그램** (① 백업 → ② 공유 → ③ DEV → ④ Vercel 시각화)
- 단순 `vercel deploy` 명령 → **All-in-One bash 스크립트** (4 destinations 모두 처리, sed sanitize 포함)
- "⚠️ 누락 방지 룰" 박스 + 16일 stale 사고 사례 명시
- 자동화 흐름 설명도 4-way 명시로 갱신

### system-docs-updater 스킬 재구성

`~/.claude/skills/system-docs-updater/SKILL.md`:
- 기존 "Quick Update Command" (backup만) + 별도 "Quick Share Command" → **단일 "All-in-One Sync Command"** 통합
- "4-way Sync Pre-Deploy Checklist" 추가 (체크박스 4개 — 모두 ✅ 후에만 deploy)
- 누락 사고 패턴 #1, #2, #3 명시
- 자동 leak 검증 (`exit 1` if SANITIZE 룰 미커버 시 중단)
- Quick Verification Command 추가 (배포 후 즉시 실행 가능한 라이브 검증)

### Share 폴더 복구 + sanitization 강화

7개 share 파일 (5 system + SKILL_share + system-docs-map_share) 모두 즉시 재생성:
- SANITIZE 룰 확장 — 기존 5개 (`vault-path` · `구요한` · `바람빛교회` · ...) 에 5개 추가 (`Yohan Koo` · `johnfkoo951` · `Cmdspace.contact@gmail.com` · `dev-path` · `home`)
- 자동 leak 검증 통과 (실제 개인정보 0건)

### 영속화 (다음 세션부터 자동 적용)

3중 안전망:
1. **CLAUDE.md** (precedence 1, 항상 LLM 컨텍스트 로드) — 4-way 명시
2. **SKILL.md** — All-in-One Sync Command (구조적으로 누락 불가)
3. **메모리** (`feedback_system_files_4way_sync.md`) — MEMORY.md 인덱스에 추가, 모든 새 세션에서 자동 로드

### 검증 결과 (4 destinations 동시 갱신)

| Destination | Files | mtime | 상태 |
|-------------|:---:|:---:|:---:|
| ① 백업 | 6 | 00:06 | ✅ |
| ② 공유 | 7 | 00:06 | ✅ leak 0건 |
| ③ DEV | 5 + 8 rules + ZIP | 00:06 | ✅ |
| ④ Vercel | system.cmdspace.work | 200 OK | ✅ |

---

## v4.4 — 2026-05-03 (8-File Scheme + Codex/Antigravity Lanes)

### File Version Snapshot

| File | Version | Δ from v4.3 |
|------|:-------:|:-----------:|
| CLAUDE.md | 3.5 | ⬆ ~3.3 → 3.5 |
| AGENTS.md | 2.5 | ⬆ ~2.3 → 2.5 |
| **ANTIGRAVITY.md** | **2.0** | ⬆ bare → 2.0 (full rewrite) |
| CMDS.md | 2.5 | ⬆ ~2.3 → 2.5 |
| 🏛 CMDS Guide.md | 2.5 | ⬆ ~2.3 → 2.5 |
| 🏛 CMDS Head Quarter.md | 1.4 | ⬆ 1.2 → 1.4 |
| BRAIN.md *(internal)* | (Gobi-managed) | — |
| BRAIN_PROMPT.md *(internal)* | (Gobi-managed) | — |

**트리거**: 다중 AI agent 운영 정착 — Codex 일상 사용 본격화 + Antigravity (Google Gemini) 시스템 파일 모더나이즈 + 8개 system file 의 precedence 정합성 확보.

### 8-File System Scheme 확립

볼트 내 시스템 파일을 4 그룹 8 파일로 정렬 (precedence 1-8):

| Group | Files | Precedence |
|-------|-------|:---:|
| 🤖 LLM Coding Agents | CLAUDE.md · AGENTS.md | 1, 2 |
| 🧪 Vendor-Specific | ANTIGRAVITY.md (Gemini) | 3 |
| 📚 Context & Standards | CMDS.md · 🏛 Guide · 🏛 HQ | 4, 5, 6 |
| 🧠 Gobi Persona | BRAIN.md · BRAIN_PROMPT.md | 7, 8 |

**공개 배포 (이 사이트)**: precedence 1, 2, 4, 5, 6 — 즉 5개 파일. ANTIGRAVITY/BRAIN/BRAIN_PROMPT 는 vendor/product 전용이라 미배포.

### AI Agent Output Lanes — 6 → 8 lane

`00. Inbox/03. AI Agent/` 산출물 분리 lane 확장:

```
03-1/03-2: Claude Code (MBP / Studio)
03-3/03-4: OpenClaw (MBP / Studio)
03-5/03-6: Codex (MBP / Studio)        ← v4.3에서 추가
03-7/03-8: Antigravity (MBP / Studio)  ← v4.4에서 추가
```

odd = MBP, even = Studio 컨벤션.

### 파일별 변경 요약

- **CLAUDE.md** v3.4 → **3.5**: Antigravity 03-7/03-8 lane 반영, 배포 flow rules count 7→8 (blank-line-rules.md 포함), "8 system files 중 5개 공개" 명시
- **AGENTS.md** v2.4 → **2.5**: Antigravity 03-7/03-8 lane 추가, ANTIGRAVITY 가 별도 system file 임을 명시
- **CMDS.md** v2.4 → **2.5**: precedence 3→4 정렬 (ANTIGRAVITY 가 3 차지), Antigravity lane 본문 반영, stray numeric tag (`3`) 제거
- **🏛 CMDS Guide** v2.4 → **2.5**: precedence 4→5 정렬, Antigravity lane 추가, `94. System Prompts/` → `94. Agent Settings/claude/` 폴더 rename 반영, `99. Format/` 중복 entry 제거, Sync Settings lane 표기 갱신, Version History 백필 (v2.3/v2.4/v2.5)
- **🏛 CMDS Head Quarter** v1.3 → **1.4**: precedence 5→6 정렬, Antigravity 03-7/03-8 lane 추가
- **(비공개) ANTIGRAVITY.md** bare → **2.0**: 전체 modernization — 8-file scheme 의 precedence 3 vendor-specific 자리 부여, 죽은 `00. Inbox/03. Antigravity/` 경로를 03-7/03-8 lane 으로 교체, frontmatter 표준화 (description/audience/precedence/version/changelog 추가), Required Properties 5→7 (description 추가), 모든 룰 파일 `@` 참조 추가, file reference 3-way decision tree 반영

### 룰 (`.claude/rules/`)

- 8개 룰 파일 정렬 — `blank-line-rules.md` 신규 포함 (Obsidian-tight markdown 강제)
- `file-creation-rules.md`, `directory-structure.md` 모두 03-7/03-8 lane 반영
- `wikilink-rules.md` 대폭 확장 — 파일 참조 3종 결정 트리 (`[[wikilink]]` · `@import` · 백틱) + 외부 경로 / 코드 식별자 표기 가이드

### 정합성 검증

전수 스캔 결과:
- ✅ Precedence 1→2→3→4→5→6 완벽 정렬
- ✅ "5 Core Files" 잔존 0건 (전부 "8 system files"로 갱신)
- ✅ `03-1~03-4` outdated 표기 0건
- ✅ `03. Antigravity/` 죽은 경로 의도적 경고 2건만 잔존 (사용 금지 안내용)
- ✅ stray numeric tag artifact 제거 (CMDS `[..., 3]`, ANTIGRAVITY `[..., 1]`)

---

## v4.3 — 2026-04-19 (Visual Identity + Web Redesign)

**트리거**: 사용자 요청 — "시스템 파일 페이지를 새로운 웹 스타일로 리빌딩 하려 해" + 공식 CMDS 로고 에셋 6종 정식 등록 + OG 이미지 시스템 정비.

### 신규 페이지 · 구조 개편

- **랜딩 + 문서 분리**: `/` (마케팅 랜딩) · `/docs/` (기술 문서) · `/index-brutalist.html` (구버전 아카이브)
- **Editorial Documentation 스타일** 신규 구축 (Apple SF Pro × CMDS Green × Stripe docs 영감)
  - 3컬럼 레이아웃 (사이드바 · 본문 · TOC)
  - marked.js 로 MD 인라인 렌더 + YAML frontmatter 추출 표시
  - ⌘K Command Palette 전역 검색 (titles + file paths + fulltext + 하이라이팅)
  - 코드블록 progressive disclosure copy 버튼 (opacity 0.4 → pre:hover 0.85 → btn:hover 1)
  - KO/EN 토글 · Light/Dark 토글 · scroll spy · 자동 TOC · 더블클릭 스크롤 상/하단 토글

### 신규 에셋

- **공식 로고 6종 정식 등록** (`/assets/logos/`)
  - `cmds-logo-round.png` — 파비콘 · 헤더 brand mark (28px)
  - `cmds-logo-black.png` / `cmds-logo-white.png` — 아이콘 only
  - `cmds-logo-typo-black.png` / `cmds-logo-typo-white.png` — 로고 + 타이포 lockup
  - `cmds-typo-white.png` — 타이포 only
- **OG 이미지 시스템** (`/assets/og/`)
  - `og-landing.png` (1200×630, 라이트 녹색 그라디언트)
  - `og-docs.png` (1200×630, 다크 핑크 그라디언트)
  - `templates/*.html` 재생성용 HTML 템플릿
- **자동 빌드 스크립트** — `/scripts/build-og.sh` (Chrome headless 로 HTML → PNG 변환)

### CMDS Color System v2.0 → v2.5 대폭 확장

기존 v1.0 에서 2.5 로 5단계 진화 (볼트 `50. Assets/51. Brand/CMDS Color System.md`):

- **v2.0** — CI/BI 분리, 라이트/다크 토큰, Obsidian 그래프 팔레트, Apple 타이포 스택
- **v2.1** — Copy Button Progressive Disclosure, CSS Specificity 주의, Interaction Patterns (더블클릭 스크롤), Component Recipes
- **v2.2** — `.accent-word` 클래스 확정 (인라인 style 금지), Full-Bleed CTA 다크 핑크 그라디언트, Cross-Page Navigation
- **v2.3** — 공식 로고 에셋 6종 등록, Logo Usage Rules
- **v2.4** — 히어로 상단 로고 기본 사용 안 함 결정 (헤더 + 하단 lockup 으로 분산)
- **v2.5** — OG 이미지 시스템 정식 등록 (1200×630 규격, 메타 17종 체크리스트, 자동 생성 스크립트)

### CI/BI 디자인 결정 기록

- **Brand mark (로고)** — 테마 무관 `#134538` CMDS Dark Green 고정 (CI)
- **Primary CTA 버튼**:
  - 라이트: `#134538` + `#fff` 흰 글씨
  - 다크: **`#E985A2` CMDS Pink** + `#0b0f0d` 어두운 글씨
  - hover: `#1a5d4b` (green-hover) / `#D16C8A` (pink-dark)
- **Accent highlights** — 라이트=녹색 · 다크=핑크 자동 전환 (`.accent-word` 클래스)
- **Full-Bleed CTA 블록** — 라이트 녹색 그라디언트 / 다크 핑크 그라디언트

### 시스템 파일 업데이트

- **CLAUDE.md** — "📦 System Files Deployment" 섹션 신설 (Vercel · Cloudflare · DEV 폴더 · 배포 명령)
- **AGENTS.md** — "Public Deployment" 간결 요약 + CLAUDE.md 참조
- **CMDS.md** — "Public Deployment of System Files" 철학 수준 언급
- `date modified` 모두 2026-04-19

### 인프라 · 배포 명확화

- **Vercel 프로젝트 "cmds-system-files-v2"** 의 "v2" 는 인프라 세팅의 2차 시도 (v1 orphaned) — 시스템 파일 콘텐츠 버전 v4.x 와 **무관**
- DEV 폴더 `/Users/yohankoo/DEV/cmds-system-files/` 가 **배포 소스 폴더** 로 확정
- 배포 명령: `cd /DEV/cmds-system-files && vercel deploy --prod --yes`
- GitHub `johnfkoo951/cmds-system-files` 는 코드 히스토리 백업 (Vercel 자동 배포 연결 없음, 수동 배포)
- 도메인: Cloudflare DNS (`system.cmdspace.work` A record → `76.76.21.21` Vercel)

### 사용성 개선

- **Cross-Page Navigation** — docs 헤더에 "Home" + "GitHub" inline nav (랜딩 ↔ 문서 왕복)
- **더블클릭 빈 공간 → 스크롤 토글** — 상단 절반: 최하단 이동 · 하단 절반: 최상단 이동
- **KO/EN 토글 + Light/Dark 토글** — localStorage 저장, 시스템 다크모드 자동 감지
- **파비콘** — inline SVG `§` → 실제 라운드 로고 PNG 로 교체

### 공개 안내문

- 볼트 `70. Outputs/71. Published/2026-04-19-CMDS System Files 공개 안내문.md` 신설
- 6가지 버전: SNS 긴 (한/영) · 카카오톡 짧은 (한/영) · 카카오톡 3분할 (한/영)
- "Fork the architecture. Keep the philosophy." CMDSPACE 공식 tagline 확정

---

## v4.2 — 2026-04-15 (CMDS Process Command Suite)

**트리거**: 사용자 지시 — "cmds 프로세스에 맞게 connect merge develop share 로 하면 어떨까? inbox 명령어는 인박스 파악하는데 쓰고 c m d s 명령어들 통해서 각각 프로세스에 맞게 구조화하는 것이 중요할듯."

### 신규 파일 생성 (8개 슬래시 커맨드)

`90. Settings/94. Agent Settings/claude/commands/` 에 8개 커맨드 파일 신설:

1. `inbox.md` — 9개 inbox 서브폴더 스캔 + AskUserQuestion 라우팅 (router only)
2. `connect.md` — inbox → 📖 100 Themes, 자동 분류·중복제거·stub (low-friction)
3. `merge.md` — N개 노트 → 1개 📖 200 Literature, multi-dialog 합성 (heaviest)
4. `develop.md` — method 적용 + artifact 생성 (code/prompt/curriculum/specialty)
5. `share.md` — 기존 skills 자동 위임 오케스트레이션 (thebetter-writer, markdown-slides 등)
6. `lint.md` — 단계별 위생 점검 scope (inbox/connect/merge/develop/share/all)
7. `query.md` — 볼트 + LLM Wiki 검색, 결과는 해당 CMDS 카테고리에 file-back (별도 폴더 X)
8. `status.md` — 단계별 노트 수 + 추천 액션 one-screen snapshot

### 5개 시스템 파일 업데이트

1. **CLAUDE.md** — "CMDS Process Command Suite (2026-04-14+)" 섹션 신설 (Cross-Vault Query 다음)
	- 8 커맨드 역할 표, 결정 트리, 설계 결정 기록, 전형적 세션 패턴
2. **AGENTS.md** — "CMDS Process Command Suite" 섹션 신설 (Templates 다음)
	- 다른 AI 에이전트용 요약 + slash command 미지원 런타임에서의 대안 가이드
3. **CMDS.md** — "Command Suite: CMDS Process as Operational Verbs" 섹션 신설 (Working with CMDS System 안)
	- 커맨드를 CMDS Process 의 operational verb 로 격상, 철학/맥락 해설
4. **🏛 CMDS Guide.md** — "CMDS Process Command Fields (v2.2, 2026-04-14+)" 섹션 신설 (Properties 안)
	- 신규 v2 프로퍼티 10개 공식 등록 (mergePurpose, sourceNotes, mainVaultRelated, developSources, shareSourceNotes, shareFormat, sharePurpose, queryOrigin, querySources, sourceInbox)
5. **🏛 CMDS Head Quarter.md** — "CMDS Process Commands (2026-04-14+)" 섹션 신설 (CMDS Process 다음)
	- 네비게이션 허브에 8 커맨드 한 줄 요약 등재

### 주요 설계 결정 (사용자 승인)

1. **Vocabulary**: LLM Wiki 의 ingest/query/lint 대신 CMDS Process (Connect/Merge/Develop/Share) 어휘 채택. Satellite 와 mothership 의 workflow 언어 분리.
2. **Inbox = Router only**: `/inbox` 는 절대 write 안 함. `AskUserQuestion` 으로 multi-select 스코프 받고 stage 커맨드로 위임.
3. **Share = Orchestrator only**: `/share` 는 content 직접 작성 금지. 기존 13개 skills (thebetter-writer, markdown-slides, tone-writer, pptx-cmds, series-writer, social-media-content-adapter, course-designer, markdown-video, business-docs 등) 로 자동 라우팅.
4. **Query results ≠ separate folder**: 사용자 정책 "내 모든 노트가 쿼리의 소재이고 결과" — `/query` 결과는 적합한 CMDS 카테고리 (220 Personal Insights, 210 Literature Reviews 등) 로 분류. LLM Wiki 의 `30. Queries/` 같은 origin-based 폴더 구조 거부.
5. **Automation density**: `/connect` auto-pilot (dialog 0~1회), `/merge` 의도적 multi-dialog (synthesis = 정보 손실), `/develop`+`/share` 결정 지점 1~2회, `/lint`+`/status` zero-dialog.
6. **AskUserQuestion 표준화**: stage 커맨드 모두 MCP 도구 사용, `multiSelect` 가능한 경우 활용, max 4 options, "(Recommended)" 첫 번째.
7. **CMDS 카테고리 = 메타데이터**: 100/200 물리 폴더 없음. 모든 노트는 `30. Permanent Notes/`, `60. Collections/` 등 기존 구조에 저장되고 `CMDS:` + `index:` frontmatter 로 카테고리 등록.

### 메모리 파일 신규

`~/.claude/projects/.../memory/cmds-process-commands.md` — 커맨드 존재 + 사용 정책 reference 메모리 추가.

### 왜 v4.2인가

- v4.0/v4.1 이 frontmatter schema 확장이었다면, v4.2 는 **operational layer** 추가.
- 문서 구조나 프로퍼티 schema 는 v4.1 유지 — 새 프로퍼티 10개가 추가됐지만 기존 노트 호환성은 그대로 (backward compatible).
- 가장 큰 변화는 **파일이 아닌 워크플로** — CMDS Process 가 철학에서 실행 가능한 커맨드로 구현됨.

---

## v4.1 — 2026-04-07 (Description Field Standardization)

**트리거**: 사용자 지시 — "생성하는 문서에 항상 YAML에 description 필드를 만들고 영어로 LLM용 설명을 작성하자"

### 변경 사항

1. **필수 프로퍼티 6개 → 7개**
	- `description` 필드가 7번째 필수 프로퍼티로 승격
	- **반드시 영어로 1-2문장** 작성 — LLM의 관련성 판단용 기계 가독 힌트
	- Skill/tool description 스타일: "무엇을 담고 있는가 + 언제 참조해야 하는가"

2. **`.claude/rules/frontmatter-standard.md`** (공용 규칙 업데이트)
	- 필수 프로퍼티 블록에 `description:` 추가
	- Rule #6 신설: "description must be in English"
	- ✅ Good / ❌ Bad 예시 제공

3. **시스템 파일 5개 개별 버전 bump**
	- CLAUDE.md: 3.0 → **3.1**
	- AGENTS.md: 2.0 → **2.1**
	- CMDS.md: 2.1 → **2.2**
	- 🏛 CMDS Guide.md: 2.2 → **2.3**
	- 🏛 CMDS Head Quarter.md: 1.1 → **1.2**

4. **5개 파일 description 필드 영어 변환** (exemplar 역할)
	- 기존 한국어 설명 → 영어 1-2문장으로 재작성
	- 모든 파일이 "what + when to reference" 패턴 준수

5. **CLAUDE.md Pre-Flight Checklist 항목 추가**
	- `[ ] description field present and in English`

6. **CLAUDE.md / AGENTS.md / CMDS.md Essential (Post-Compact) 업데이트**
	- "필수 프로퍼티 6개" → "필수 프로퍼티 7개"

7. **Feedback 메모리 저장**
	- `~/.claude/projects/-Users-yohankoo/memory/feedback_yaml-description-english.md`

### 왜 v4.1인가

- v4.0(2026-04-01) Architecture Upgrade의 연장선 — frontmatter schema를 한 필드 확장
- 과거 v2.0 → v2.1(Frontmatter Standard) 패턴과 동일한 성격의 Minor bump
- 기존 6-프로퍼티 노트들과 호환됨 (추가일 뿐 breaking change 아님)

---

## v4.0 — 2026-04-01 (Architecture Upgrade)

**영감**: Claude Code 소스 코드 아키텍처 분석 → 9개 패턴 적용

### 신규 파일 생성
- `.claude/rules/indentation-rules.md` — YAML 2spaces / MD tab 공통 규칙
- `.claude/rules/frontmatter-standard.md` — 필수 6프로퍼티 + 포맷 규칙
- `.claude/rules/file-creation-rules.md` — 출력 경로, 네이밍, 프로젝트 폴더 규칙
- `.claude/rules/wikilink-rules.md` — 옵시디언 위키링크 문법 + YAML 인용 규칙
- `.claude/rules/directory-structure.md` — 볼트 폴더 구조 + CMDS 카테고리

### 전체 파일 공통 변경
1. **`precedence` 추가** — 파일 간 우선순위 명시 (1=CLAUDE → 5=HQ)
2. **`memory-type` 추가** — Claude Code memdir 타입 매핑 (feedback/user/reference)
3. **`required-for` / `optional-for` 추가** — 에이전트 스코핑 (어떤 작업에 이 파일이 필수/선택인지)
4. **`token-estimate` 추가** — 토큰 예산 의식 (AI가 어떤 파일을 우선 로드할지 판단)
5. **`changelog` 추가** — 각 파일 frontmatter에 버전 이력 내장
6. **`<!-- STATIC -->` / `<!-- DYNAMIC -->` 마커** — 캐시 가능 영역 vs 갱신 필요 영역 구분
7. **`## Essential (Post-Compact)` 섹션** — 컨텍스트 압축 후 복구용 핵심 규칙 요약

### 파일별 변경

#### CLAUDE.md (v2.1 → v3.0)
- 중복 규칙을 `@.claude/rules/` 로 분리 (@include 5개)
- Critical Rules 섹션: 인라인 규칙 → @include 참조로 전환
- Pre-Flight Checklist 유지 (빠른 확인용)
- Directory Structure: @include로 교체
- File Creation Rules: @include로 교체
- Note Types 통계 업데이트 (최신 수치 반영)
- Related System Files에 precedence 번호 추가
- `[[wikilink]]`는 옵시디언 탐색용으로 유지, `@include`는 AI 로딩용으로 분리
- 토큰 약 21KB → 예상 ~14KB (rules 포함 시 동일하나 공유 가능)

#### AGENTS.md (v1.0 → v2.0)
- 중복 규칙 60% 제거 → @include 4개로 교체
- Critical Rules 전체를 @include 기반으로 전환
- Directory Structure를 @include로 교체
- 고유 섹션만 유지: Note Types, Status Values, File Prefixes, Templates
- 토큰 약 9KB → 예상 ~5KB (rules 포함 시 동일하나 공유 가능)

#### CMDS.md (v2.0 → v2.1)
- frontmatter 강화: precedence(3), memory-type(user), required-for, token-estimate
- Essential (Post-Compact) 섹션 추가 — 5개 핵심 컨텍스트
- `<!-- STATIC -->` 마커 추가 (System Documentation Overview 이전)
- `<!-- DYNAMIC -->` 마커 추가 (Vault Statistics 이전)
- changelog 필드 추가

#### 🏛 CMDS Head Quarter (→ v1.1)
- frontmatter 강화: precedence(5), memory-type(reference), required-for, token-estimate
- version, changelog 필드 추가

#### 🏛 CMDS Guide (v2.1 → v2.2)
- frontmatter 강화: precedence(4), memory-type(reference), required-for, token-estimate
- tags 정리: 불필요한 태그 제거 (태그는자유로워야지, maps, example, service)
- changelog 필드 추가

### @include vs [[wikilink]] 사용 원칙

| 용도 | 문법 | 예시 |
|------|------|------|
| **AI가 내용을 인라인 로드** | `@path` | `@.claude/rules/indentation-rules.md` |
| **옵시디언 내부 탐색/링크** | `[[name]]` | `[[🏛 CMDS Guide]]` |
| **양쪽 모두 필요** | 둘 다 사용 | `@CMDS.md → [[CMDS.md]]` |

- `@include`: AI 에이전트가 파일 내용을 실제로 읽어야 할 때 (규칙, 구조 정의)
- `[[wikilink]]`: 사용자가 옵시디언에서 클릭하여 이동할 때 (탐색, 참조)
- Related System Files 같이 양쪽 다 필요한 경우: `@파일 → [[파일]]` 형태로 병기

---

## v2.1 — 2026-03-30 (Frontmatter Standard)

### 변경 사항
- 5개 파일 모두 frontmatter에 `description`, `audience`, `scope` 추가
- AI Documents: `type: documentation` 통일
- Human Documents: `type: CMDS` 유지
- 백업/공유 폴더를 `40. Docs/47. CMDS Docs/`로 이동
- system-docs-updater 스킬에 frontmatter 표준 섹션 추가

---

## v2.0 — 2026-03-15 (Full Review)

### 변경 사항
- 5개 파일 전면 리뷰 및 통계 갱신 (5,344+ → 10,000+)
- CLAUDE.md: 백업 경로 오타 수정, GenAI Chats 추가
- CMDS.md: PhD Candidate → PhD ABD, AI Tools 갱신, 50. Assets 섹션 추가
- 🏛 CMDS Head Quarter: CMDS Process 설명 추가, Vault Folders 섹션 추가
- 🏛 CMDS Guide: 폴더 구조 현행화, 새 type 추가
- AGENTS.md: 볼트 규모 갱신
- 백업/공유 파일 동기화
- 에세이 시리즈 9편 작성
- 웹페이지 v3 배포 (system.cmdspace.work)
- ChatGPT 시스템 프롬프트 생성

---

## v1.0 — 2025-09-27 (Initial)

### 생성
- CLAUDE.md 최초 작성
- 이후 AGENTS.md, CMDS.md, Guide, HQ 순차 추가

---

## 파일 위치 참조

| 구분 | 경로 |
|------|------|
| **정본 (5개)** | 볼트 루트: `/CLAUDE.md`, `/AGENTS.md`, `/CMDS.md`, `/🏛 CMDS Head Quarter.md`, `/🏛 CMDS Guide.md` |
| **공통 규칙 (5개)** | `.claude/rules/indentation-rules.md`, `frontmatter-standard.md`, `file-creation-rules.md`, `wikilink-rules.md`, `directory-structure.md` |
| **백업** | `40. Docs/47. CMDS Docs/cmds-system-files/` (`_backup.md`) |
| **공유본** | `40. Docs/47. CMDS Docs/cmds-system-files-share/` (`_share.md`) |
| **웹 배포** | [system.cmdspace.work](https://system.cmdspace.work) |
| **GitHub** | [johnfkoo951/cmds-system-files](https://github.com/johnfkoo951/cmds-system-files) |
| **변경 로그** | 이 파일 (`40. Docs/47. CMDS Docs/cmds-system-files/CHANGELOG.md`) |
