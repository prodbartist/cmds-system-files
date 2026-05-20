# 03. Skill Rebuild Spec — `cmdspace-web-builder` v4.3

> 새 스킬의 설계 청사진. 이 문서대로 제작하면 v4.3 표준이 자동 반영되는 web builder 가 완성됨.

## 1. 목표 (Skill Goals)

1. **호출 한 번으로 v4.3 준수**: 사용자가 `cmdspace-web-builder` 호출 시 favicon · OG · 색상 · 타이포 · 로고 · 컴포넌트 전부 자동 포함
2. **템플릿 타입 기반**: 6종 주요 템플릿 + 변형으로 다양한 웹 프로젝트 커버
3. **DEV-first 원칙**: 모든 출력은 `/Users/yohankoo/DEV/{project}/` 에 생성 (볼트 금지)
4. **자동 OG 생성**: Chrome headless 로 1200×630 PNG 자동 렌더
5. **vercel 링크 자동화**: 프로젝트 생성 시 `vercel link` 까지 가이드 (실행은 사용자)

## 2. 스킬 파일 구조 (제안)

```
~/.claude/skills/cmdspace-web-builder-v2/
├── SKILL.md                        — 메인 스킬 문서 (트리거 + 워크플로)
├── templates/
│   ├── landing/                    — Template 1: Marketing Landing
│   │   ├── index.html
│   │   ├── assets/                 — 로고 + OG 템플릿
│   │   ├── scripts/build-og.sh
│   │   └── README.md              — 이 템플릿 커스터마이즈 방법
│   ├── editorial-docs/             — Template 2: Editorial Documentation
│   │   └── (same structure)
│   ├── showcase/                   — Template 3: Showcase (컨퍼런스·연구)
│   ├── archive/                    — Template 4: Personal/Event Archive
│   ├── technical-product/          — Template 5: Tool/Product
│   └── brutalist-legacy/           — Template 6: Brutalist variant
├── assets/
│   ├── logos/                      — 6종 로고 PNG 원본 (모든 템플릿 공유)
│   ├── og-base/                    — OG 베이스 템플릿 (라이트·다크)
│   └── common/                     — 공용 CSS/JS 스니펫
├── scripts/
│   ├── new-site.sh                — 새 사이트 생성 (template → DEV 복사 + 변수 치환)
│   └── build-og.sh                — OG 이미지 빌드 (모든 템플릿 공유)
└── references/
    ├── color-system-v2.5.md       — 색상 참조 (링크: 볼트 CMDS Color System)
    ├── minimal-snippet.md         — 복붙 키트 (링크: 볼트 v4.3-minimal-snippet)
    └── deployment-guide.md        — Vercel 배포 가이드
```

## 3. Template Types (6종)

### 3.1 Landing (마케팅 랜딩)

**Reference**: `system.cmdspace.work` (https://system.cmdspace.work)
**Source**: `/Users/yohankoo/DEV/cmds-system-files/index.html`

**구조**:
- Header (sticky + blur + nav)
- Hero (eyebrow pill + display title + lede + CTA buttons + meta grid)
- "The Idea" (2-column quote + body)
- Architecture panel (5-file precedence cards)
- Process flow (4-stage dots + connecting gradient line)
- Audiences (2-column cards)
- Categories grid (9 cells)
- Teaser (dark terminal-style code block)
- Full-bleed CTA block (green/pink gradient)
- Brand lockup (footer sign-off)
- Footer

**특징**:
- 최대 타이포 104px hero title
- Gradient text on accent words
- IntersectionObserver reveal animations
- Double-click scroll toggle

### 3.2 Editorial Documentation (기술 문서)

**Reference**: `system.cmdspace.work/docs/`
**Source**: `/Users/yohankoo/DEV/cmds-system-files/docs/index.html`

**구조**:
- Header (brand logo `href="/"` + inline Home/GitHub nav)
- 3-column layout: Sidebar (280px) · Main (720px max) · TOC (240px)
- Inline Markdown rendering (marked.js)
- ⌘K Command Palette (fulltext search)
- Copy buttons with progressive disclosure
- Sidebar scroll-spy + auto-generated TOC
- Light/Dark + KO/EN toggles

**특징**:
- 독서 최적화 본문 폭 720px
- Newsreader → SF Pro 로 톤 전환 (v4.3)
- TOC 자동 생성 from h2/h3
- 다크모드 핑크 accent

### 3.3 Showcase (컨퍼런스·연구 발표)

**대상**: sicem.cmdspace.work · course.cmdspace.work · showcloud.cmdspace.work
**특징**:
- Hero with large typography
- 갤러리 섹션 (이미지·비디오)
- 리소스 다운로드 링크
- 발표자/저자 정보
- 연관 자료 링크

### 3.4 Archive (개인·행사 기록)

**대상**: yhn.cmdspace.work · windlight.cmdspace.work
**특징**:
- 조용한 톤, reading-first 레이아웃
- 연도·날짜 중심 네비게이션
- 사진·감상 중심 콘텐츠
- 조용한 애니메이션 (fade only)

### 3.5 Technical Product (도구·제품)

**대상**: cmdtrace.cmdspace.work
**특징**:
- Feature grid
- How it works (step-by-step)
- Demo screenshot/video
- Installation instructions
- GitHub link 강조

### 3.6 Brutalist Legacy (기존 스타일 유지 변형)

**대상**: hrprompt.cmdspace.work (기존 BRUTALIST v3.0 유지 원하는 경우)
**특징**:
- v4.3 이전 스타일 유지
- 다만 파비콘·OG 는 v4.3 표준 강제 (favicon · 17 메타)
- Space Grotesk + Toxic Green `#CCFF00`

**이유**: 기존 브루탈리즘 팬층·특정 프로젝트 아이덴티티 보호. 단 metadata 는 현대적.

## 4. 공통 파이프라인 (모든 템플릿)

### 4.1 `new-site.sh` 워크플로

```bash
# 예상 사용법
./new-site.sh --template=landing --name=my-project --domain=my-project.cmdspace.work

# 내부 동작:
# 1. /Users/yohankoo/DEV/my-project/ 생성
# 2. templates/landing/ 내용 복사
# 3. HTML 내 {변수} 치환 (사이트명·도메인·타이틀·설명)
# 4. /DEV/my-project/assets/logos/ 에 6종 로고 복사
# 5. /DEV/my-project/assets/og/templates/og-my-project.html 생성
# 6. /DEV/my-project/scripts/build-og.sh 복사 (공용)
# 7. 사용자에게 안내:
#    - "cd /DEV/my-project && vercel link" 로 Vercel 연결
#    - "./scripts/build-og.sh" 로 OG 렌더
#    - "vercel deploy --prod --yes" 로 배포
#    - Cloudflare 에 A record 추가 (76.76.21.21)
```

### 4.2 Variable 치환

스킬이 HTML·CSS·OG 템플릿에서 치환할 변수:
- `{project_name}` — 내부 명 (소문자·하이픈)
- `{site_title}` — 사이트 타이틀 (UI 표시)
- `{site_description}` — 1-2문장 설명
- `{domain}` — 풀 도메인 (e.g., `my-project.cmdspace.work`)
- `{author}` — "구요한" 또는 공유자
- `{github_url}` — 있으면, 없으면 빈 문자열

### 4.3 OG 자동 생성

각 템플릿은 `assets/og/templates/og-{project}.html` 을 자동 생성:
- Landing → 라이트 녹색 그라디언트 베이스
- Editorial Docs → 다크 핑크 그라디언트 베이스
- Showcase/Archive/Product → 라이트 녹색 (기본)
- Brutalist → 검정 + toxic green

`scripts/build-og.sh` 실행 시 각 HTML → 1200×630 PNG 자동 렌더.

## 5. 스킬 트리거 (SKILL.md 의 description 후보)

```yaml
description: >
  Create and deploy CMDSPACE-style web pages using v4.3 design standards
  (Apple SF Pro × CMDS Green/Pink · 17 OG meta tags · round logo favicon).
  6 template types: Landing · Editorial Documentation · Showcase · Archive
  · Technical Product · Brutalist Legacy. Generates new project in
  /Users/yohankoo/DEV/{name}/, copies assets, prepares Vercel deploy.
  Use when creating any cmdspace.work subdomain site.

triggers:
  - "사이트 만들어줘"
  - "웹페이지 만들어"
  - "cmdspace-web-builder"
  - "새 랜딩 페이지"
  - "editorial docs 만들어"
  - "cmdspace subdomain"
```

## 6. 마이그레이션 범위 (10개 사이트, 스킬 리빌드 후 적용)

| # | 도메인 | Vercel 프로젝트 | 소스 현황 | 추천 템플릿 |
|---|--------|----------------|-----------|-----------|
| 1 | sicem.cmdspace.work | web | 🗂 `00. Inbox/03. AI Agent/…/2026-04-03-SICEM-2026-keynote/web/` | Showcase |
| 2 | showcloud.cmdspace.work | website | 🗂 `…/2026-03-21-research-knowledge-resolution/website/` | Showcase |
| 3 | course.cmdspace.work | website (2번과 동일) | 위와 동일 | Showcase |
| 4 | llm-wiki.cmdspace.work | cmds-llm-wiki-showcase | 📁 `/DEV/cmds-llm-wiki-web/website/` | Editorial Documentation |
| 5 | cmdtrace.cmdspace.work | cmdtrace | 📁 `/DEV/CmdTrace/website/` | Technical Product |
| 6 | openclaw.cmdspace.work | openclaw-study-guide | 🗂 `…/2026-01-31-openclaw-study/website/` | Showcase |
| 7 | terminal.cmdspace.work | macos-terminal-comparison-2026 | 🗂 `…/2026-03-28-macos-terminal-comparison/website/` | Archive (blog) |
| 8 | hrprompt.cmdspace.work | hrprompt-cmdspace | ❓ 로컬 소실 | Brutalist Legacy (복원) |
| 9 | youth.cmdspace.work | 2026-02-07-cmds-youth-showcase | 🗂 `10. CMDS Process/13. Develop/…` | Showcase |
| 10 | windlight.cmdspace.work | 2026-04-05-windlight | 🗂 `…/2026-04-05-windlight/` | Archive |
| 11 | yhn.cmdspace.work | spring-camp-emotion-records | 📁 `/DEV/web-deployments/spring-camp-emotion-records/` | Archive |

**이관 원칙**: 🗂 볼트 → 📁 DEV 로 옮기고 v4.3 적용. Vercel 링크 재설정.

**제외 대상**: `lg.cmdspace.work` · `ax.cmdspace.work` · `test.cmdspace.work` (LG 고객사)

## 7. 구현 순서 제안

### Phase A: Skill Foundation
1. `~/.claude/skills/cmdspace-web-builder-v2/` 폴더 생성
2. SKILL.md 작성 (description + trigger + workflow)
3. `assets/logos/` 에 볼트 로고 복사
4. `scripts/build-og.sh` 작성
5. `scripts/new-site.sh` 작성 (변수 치환 + 폴더 scaffold)

### Phase B: Template 1 - Landing
1. `templates/landing/` 에 `/DEV/cmds-system-files/index.html` 을 기반으로 작성
2. 변수 포인트 식별 · placeholder 로 치환
3. OG 템플릿 `templates/landing/assets/og/templates/og-landing.html`
4. 테스트: 새 프로젝트 생성 → 배포 → 검증

### Phase C: Template 2 - Editorial Documentation
1. `templates/editorial-docs/` 에 `/DEV/cmds-system-files/docs/index.html` 기반 작성
2. 변수 치환 + 동일 프로세스

### Phase D: Templates 3-6 (Showcase · Archive · Technical · Brutalist)
기존 마이그레이션 대상 사이트들을 표준화하면서 **실전 검증된 템플릿 추출** :
- Showcase → sicem 마이그레이션에서 추출
- Archive → yhn/windlight 마이그레이션에서 추출
- Technical Product → cmdtrace 마이그레이션에서 추출
- Brutalist Legacy → hrprompt 복원에서 추출

### Phase E: 10개 사이트 마이그레이션
스킬을 이용해서 모든 사이트를 v4.3 으로 이관.

## 8. 성공 기준

스킬 리빌드 후, 다음 한 줄로 새 사이트 생성 가능:

```
"sicem 2026 컨퍼런스 랜딩 페이지 만들어줘. 도메인 sicem.cmdspace.work"
```

→ 스킬이 자동으로:
1. `/DEV/sicem-web/` 생성
2. Showcase 템플릿 복사 + 변수 치환
3. 로고·OG 에셋 복사
4. OG 이미지 1200×630 PNG 렌더
5. 17 메타 태그 완비 HTML
6. Vercel 링크 · 배포 명령 안내

사용자가 `vercel deploy --prod` 한 번만 치면 v4.3 준수 사이트가 라이브.

## 9. 참고 자료

- **README.md** (이 폴더) — 네비게이션 + 전체 맥락
- **01-STANDARDS.md** — 색상·타이포·에셋 표준
- **02-PATTERNS.md** — 컴포넌트 레시피·인터랙션·Anti-patterns
- **볼트 `[[CMDS Color System]]` v2.5** — 원천 디자인 시스템
- **볼트 `[[v4.3-minimal-snippet]]`** — 복붙 키트
- **`/DEV/cmds-system-files/`** — 살아있는 레퍼런스 구현

## 10. 다음 세션 시작 방법

```
새 세션에서:

cd /Users/yohankoo/DEV/cmds-system-files/docs/skill-rebuild-context/
→ README.md · 01-STANDARDS.md · 02-PATTERNS.md · 03-SKILL-SPEC.md
  4개 읽고 컨텍스트 복구

→ `skill-creator` 스킬 호출

→ Phase A 부터 순서대로 시작
```
