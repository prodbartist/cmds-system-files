# 01. v4.3 Design Standards

> 모든 CMDS 퍼블리시 사이트가 공통으로 따라야 할 시각 언어.

## 1. Color System (CMDS Color System v2.5 요약)

### 1.1 CI (Corporate Identity — 절대 불변)

| Name | Hex | Usage |
|------|-----|-------|
| **CMDS Dark Green** | `#134538` | Primary brand · light-mode accent · **brand mark 고정** |
| **CMDS Pink** | `#E985A2` | Dark-mode accent · links · active · CTA in dark |

**핵심 규칙**:
- 브랜드 마크 (로고) → 라이트·다크 **모두 녹색 고정** (CI 일관성)
- CTA 버튼 → 라이트=녹색+흰글자 · 다크=핑크+어두운글자
- Accent text (highlight word) → 라이트=녹색 · 다크=핑크 (자동 `[data-theme]` 전환)

### 1.2 전체 팔레트

```css
:root {
  /* CMDS Green — CI */
  --cmds-green:         #134538;
  --cmds-green-hover:   #1a5d4b;  /* hover darker */
  --cmds-green-bright:  #22896a;  /* bright variant · copied state */
  --cmds-green-glow:    #2fb488;  /* lightest bright · gradient end */
  --cmds-green-50:      #f1f7f4;  /* tinted background */
  --cmds-green-100:     #dcebe3;
  --cmds-green-200:     #bad9c9;
  --cmds-green-800:     #0d3529;
  --cmds-green-900:     #0a2820;

  /* CMDS Pink — Dark accent */
  --cmds-pink:          #E985A2;
  --cmds-pink-light:    #F4A4B8;  /* hover lighter */
  --cmds-pink-dark:     #D16C8A;  /* pressed/darker */
  --cmds-pink-soft:     #2b1922;  /* dark-bg tint */
}
```

### 1.3 Light Mode Surface

```css
:root {
  --bg:            #fbfbfa;  /* warm off-white */
  --bg-elev:       #ffffff;  /* card */
  --bg-subtle:     #f5f6f4;
  --bg-code:       #f5f5f3;
  --fg:            #0a0d0b;
  --fg-muted:      #4a544f;
  --fg-subtle:     #8a938e;
  --border:        #e6e8e6;
  --border-strong: #d0d3d0;
  --accent:        var(--cmds-green);
  --accent-soft:   var(--cmds-green-50);
  --accent-strong: var(--cmds-green-800);
}
```

### 1.4 Dark Mode Surface

```css
[data-theme="dark"] {
  --bg:            #06080a;  /* deep dark */
  --bg-elev:       #0d1411;
  --bg-subtle:     #0a1110;
  --bg-code:       #161c19;
  --fg:            #f2f4f3;
  --fg-muted:      #9aa39d;
  --fg-subtle:     #626a66;
  --border:        #1a231f;
  --border-strong: #26302a;
  --accent:        var(--cmds-pink);       /* ← Pink */
  --accent-soft:   var(--cmds-pink-soft);
  --accent-strong: var(--cmds-pink-light);
}
```

### 1.5 CMDS Process Colors (4 stages)

| Stage | Hex | Usage |
|-------|-----|-------|
| 🔗 Connect | `#3b82f6` | Discovery · linking |
| 🔀 Merge | `#8b5cf6` | Synthesis |
| 🛠 Develop | `#f59e0b` | Creation |
| 📤 Share | `#10b981` | Output |

### 1.6 Obsidian Graph View Palette (참고)

사용자 Obsidian 그래프 뷰 Groups 설정 색:
- Pink `#E985A2` (지배색) · Grey `#6b6b6b` · Coral `#E07B67` · Yellow `#F4D03F` · Orange `#F39C12` · Blue `#3b82f6` · Mint `#10b981`

## 2. Typography

### 2.1 Font Stacks

```css
--font-sans:    -apple-system, BlinkMacSystemFont, 'SF Pro Text', 'SF Pro Display', 'Pretendard', 'Helvetica Neue', Arial, sans-serif;
--font-display: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Pretendard', sans-serif;
--font-mono:    ui-monospace, 'SF Mono', 'Menlo', 'JetBrains Mono', Consolas, monospace;
--font-serif:   ui-serif, 'New York', 'Pretendard', Georgia, serif;  /* 선택 */
```

- Apple SF Pro 스택 기반
- 한글은 Pretendard (CDN): `https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css`
- Google Fonts 의존성 **지양** (SF Pro · Pretendard 만으로 충분)

### 2.2 Letter-Spacing (Apple tracking)

| 크기 | Tracking | 예시 |
|------|---------|------|
| Display (40px+) | `-0.028em` ~ `-0.042em` | Hero headlines |
| Heading (20-32px) | `-0.018em` ~ `-0.025em` | Section titles |
| Body (14-18px) | `-0.011em` | Paragraphs |
| Small (12-13px) | `-0.005em` | Labels |

### 2.3 Base Body

```css
body {
    font-family: var(--font-sans);
    background: var(--bg);
    color: var(--fg);
    line-height: 1.55;
    letter-spacing: -0.011em;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-feature-settings: 'kern', 'liga', 'calt', 'ss01';
    text-rendering: optimizeLegibility;
}
```

## 3. Spacing · Radius · Shadow

```css
--radius-sm: 6px;    /* Small buttons, inputs */
--radius-md: 10px;   /* Cards, buttons */
--radius-lg: 16px;   /* Large surfaces */
--radius-xl: 20px;   /* Hero cards, file rows */
--radius-pill: 999px; /* Pills, rounded buttons */

--shadow-soft:     0 4px 24px rgba(0, 0, 0, 0.08);
--shadow-elevated: 0 12px 40px -12px rgba(19, 69, 56, 0.18);
--shadow-green:    0 8px 24px -8px rgba(19, 69, 56, 0.3);  /* CMDS Green CTA glow */
--shadow-pink:     0 8px 24px -8px rgba(233, 133, 162, 0.35);  /* Dark CTA glow */

--section-px: clamp(24px, 5vw, 80px);
--header-h: 56px;
--max-w: 1200px;
```

## 4. Logo Assets

**위치**: `/assets/logos/` (DEV) · `50. Assets/51. Brand/logos/` (Vault 원본)

| 파일 | 용도 | 크기 |
|------|------|------|
| `cmds-logo-round.png` | **파비콘** + 헤더 brand mark | 28px (display) · 기본 1714×1713 |
| `cmds-logo-black.png` | 라이트 아이콘 only | |
| `cmds-logo-white.png` | 다크 아이콘 only | |
| `cmds-logo-typo-black.png` | 라이트 로고+타이포 lockup | |
| `cmds-logo-typo-white.png` | 다크 로고+타이포 lockup | |
| `cmds-typo-white.png` | 타이포 only | |

**규칙**:
- 파비콘 · 헤더 brand mark → **반드시** `cmds-logo-round.png`
- 배경색 절대 감싸지 않음 (`border-radius: 50%; object-fit: contain;` 만)
- 다크 로고 스왑은 2개 `<img>` + `[data-theme]` CSS 토글 (`<picture media="prefers-color-scheme">` 금지)

## 5. OG · Twitter Image (1200×630 PNG)

### 5.1 메타 태그 17종 (누락 금지)

```html
<!-- Open Graph -->
<meta property="og:type" content="website">                   <!-- article 은 글 페이지 -->
<meta property="og:site_name" content="CMDSPACE">
<meta property="og:title" content="…">
<meta property="og:description" content="…">
<meta property="og:url" content="https://{domain}">
<meta property="og:image" content="https://{domain}/assets/og/og-{site}.png">    <!-- 절대 URL 필수 -->
<meta property="og:image:secure_url" content="https://{domain}/assets/og/og-{site}.png">
<meta property="og:image:type" content="image/png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="…">
<meta property="og:locale" content="ko_KR">
<meta property="og:locale:alternate" content="en_US">

<!-- Twitter / X -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="…">
<meta name="twitter:description" content="…">
<meta name="twitter:image" content="https://{domain}/assets/og/og-{site}.png">
<meta name="twitter:image:alt" content="…">
```

**절대 실수 금지**:
- 상대 경로 사용 X → Twitter/Slack 프리뷰 깨짐
- `og:image:width` / `height` 누락 X → 일부 플랫폼 미리보기 불안정
- `og:image:alt` 누락 X → 접근성

### 5.2 두 가지 OG 스타일

**라이트 (녹색 그라디언트)** — 마케팅·랜딩용. `assets/og/templates/og-landing.html` 참조.
- 배경: `#fbfbfa` + `radial-gradient` 녹색 glow
- 타이틀: `#0a0d0b` + accent 단어는 녹색 그라디언트

**다크 (핑크 그라디언트)** — 기술 문서·어두운 테마. `assets/og/templates/og-docs.html` 참조.
- 배경: `#0b0f0d` + `radial-gradient` 핑크 glow
- 타이틀: `#f2f4f3` + accent 단어는 핑크 그라디언트

### 5.3 자동 생성 스크립트

`/scripts/build-og.sh`:

```bash
#!/usr/bin/env bash
set -euo pipefail
CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
ROOT="$(cd "$(dirname "$0")/.." && pwd)"
TPL="$ROOT/assets/og/templates"
OUT="$ROOT/assets/og"

cp -n "$ROOT/assets/logos/cmds-logo-round.png" "$TPL/logo-round.png" 2>/dev/null || true

cd "$TPL"
for tpl in og-*.html; do
    name="${tpl%.html}"
    "$CHROME" --headless=new --disable-gpu --no-sandbox \
        --window-size=1200,630 --hide-scrollbars \
        --virtual-time-budget=3000 \
        --screenshot="$OUT/$name.png" \
        "file://$TPL/$tpl"
done
```

## 6. Layout Primitives

### 6.1 Sticky Header

```css
.site-header {
    position: sticky; top: 0; z-index: 50;
    height: 56px;
    background: color-mix(in srgb, var(--bg) 85%, transparent);
    backdrop-filter: saturate(180%) blur(12px);
    -webkit-backdrop-filter: saturate(180%) blur(12px);
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center;
    padding: 0 24px;
    gap: 24px;
}
```

### 6.2 Content Max-Width

- **Landing**: `--max-w: 1200px`
- **Editorial Docs**: `--content-width: 720px` (reading optimum) · `--sidebar-width: 280px` · `--toc-width: 240px`

### 6.3 Responsive Breakpoints

- `1120px` — TOC 숨김 (docs)
- `820px` — 모바일 단일컬럼 · 헤더 inline nav 숨김
- `640px` — 버튼·lockup 축소

## 7. Reference Files (읽을 것)

DEV 폴더 기반으로 실제 구현 확인:
- `/Users/yohankoo/DEV/cmds-system-files/index.html` — 랜딩 (2002 lines)
- `/Users/yohankoo/DEV/cmds-system-files/docs/index.html` — 문서 (1391 lines)
- `/Users/yohankoo/DEV/cmds-system-files/index-brutalist.html` — 구버전 (비교용)
- `/Users/yohankoo/DEV/cmds-system-files/assets/og/templates/og-landing.html` — OG 라이트
- `/Users/yohankoo/DEV/cmds-system-files/assets/og/templates/og-docs.html` — OG 다크
- `/Users/yohankoo/DEV/cmds-system-files/scripts/build-og.sh` — OG 빌드

볼트 원천:
- `50. Assets/51. Brand/CMDS Color System.md` v2.5 — 전체 디자인 시스템
- `50. Assets/51. Brand/v4.3-minimal-snippet.md` — 복붙 키트
- `50. Assets/51. Brand/logos/` — 로고 원본 6종
- `50. Assets/51. Brand/og/` — OG 원본 + 템플릿
