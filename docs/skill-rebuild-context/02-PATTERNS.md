# 02. Component Recipes · Interactions · Anti-Patterns

> 실전 검증된 v4.3 패턴 모음. 스킬 템플릿 제작 시 이 레시피를 기본 블록으로.

## 1. Component Recipes

### 1.1 Brand Mark (Header Logo)

```html
<a class="brand" href="/">
    <img class="brand-mark" src="/assets/logos/cmds-logo-round.png"
         alt="CMDS" width="28" height="28">
    <span>{사이트명}</span>
</a>
```

```css
.brand {
    display: flex; align-items: center; gap: 10px;
    font-weight: 600; font-size: 15px;
    color: var(--fg);
    text-decoration: none;
    letter-spacing: -0.01em;
}
.brand-mark {
    width: 28px; height: 28px;
    border-radius: 50%;
    object-fit: contain;
    display: block;
    flex-shrink: 0;
    /* 배경색 금지 - 라운드 로고는 투명 영역 포함 */
}
```

### 1.2 Primary CTA Button

```html
<a class="btn btn-primary" href="{url}">
    <span>{버튼 텍스트}</span>
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
</a>
```

```css
.btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 14px 24px;
    font-size: 15px; font-weight: 500;
    letter-spacing: -0.01em;
    border-radius: var(--radius-pill);
    border: 1px solid transparent;
    cursor: pointer;
    transition: background .15s, transform .08s, box-shadow .15s;
    text-decoration: none;
}
.btn-primary {
    background: var(--cmds-green);
    color: #fff !important;
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.12),
                0 1px 2px rgba(19,69,56,0.2),
                0 8px 24px -8px rgba(19,69,56,0.3);
}
.btn-primary:hover {
    background: var(--cmds-green-hover);
    color: #fff !important;
}
.btn-primary:active { transform: scale(0.985); }

/* Dark mode: Pink */
[data-theme="dark"] .btn-primary {
    background: var(--cmds-pink);
    color: #0b0f0d !important;
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.2),
                0 2px 6px rgba(0,0,0,0.4),
                0 12px 32px -12px rgba(233,133,162,0.4);
}
[data-theme="dark"] .btn-primary:hover {
    background: var(--cmds-pink-dark);
    color: #0b0f0d !important;
}
```

**⚠️ Specificity 함정**: 부모 컨테이너에 `a:hover` 규칙 있으면 덮어쓸 수 있음. 셀렉터 구체화 + `!important`:

```css
.sidebar a.btn-primary, .sidebar a.dl-btn {
    /* ... */
}
.sidebar a.btn-primary:hover {
    background: var(--cmds-green-hover) !important;
    color: #fff !important;
}
```

### 1.3 Copy Button (Progressive Disclosure)

```css
/* 항상 보이되 연하게 → hover 시 진해짐 */
.copy-btn {
    position: absolute; top: 8px; right: 8px;
    padding: 4px 10px;
    font: 600 11px var(--font-sans);
    background: var(--cmds-green);
    color: #fff;
    border: 1px solid color-mix(in srgb, var(--cmds-green-bright) 30%, transparent);
    border-radius: 5px;
    cursor: pointer;
    opacity: 0.4;              /* ← 기본 흐릿 */
    transition: opacity .2s, background .15s, transform .08s;
}
pre:hover .copy-btn { opacity: 0.85; }   /* pre hover */
.copy-btn:hover {
    opacity: 1 !important;               /* 직접 hover */
    background: var(--cmds-green-hover);
}
.copy-btn:active { transform: scale(0.95); }
.copy-btn.copied {
    opacity: 1 !important;
    background: var(--cmds-green-bright);
}

/* Dark mode */
[data-theme="dark"] .copy-btn {
    background: var(--cmds-pink);
    color: #0b0f0d;
    border: none;
    opacity: 0.5;
}
[data-theme="dark"] pre:hover .copy-btn { opacity: 0.9; }
[data-theme="dark"] .copy-btn:hover {
    opacity: 1 !important;
    background: var(--cmds-pink-dark);
}
[data-theme="dark"] .copy-btn.copied {
    opacity: 1 !important;
    background: var(--cmds-pink-light);
}
```

JS (코드 블록에 자동 부착):
```javascript
document.querySelectorAll('pre').forEach(pre => {
    const btn = document.createElement('button');
    btn.className = 'copy-btn';
    btn.textContent = 'Copy';
    btn.addEventListener('click', () => {
        const code = pre.querySelector('code')?.textContent ?? pre.textContent;
        navigator.clipboard.writeText(code).then(() => {
            btn.textContent = 'Copied';
            btn.classList.add('copied');
            setTimeout(() => { btn.textContent = 'Copy'; btn.classList.remove('copied'); }, 1500);
        });
    });
    pre.appendChild(btn);
});
```

### 1.4 Footer Brand Lockup (Sign-off)

```html
<section class="brand-lockup">
    <div class="brand-lockup-inner">
        <img class="lockup-img lockup-light" src="/assets/logos/cmds-logo-typo-black.png" alt="CMDSPACE" loading="lazy">
        <img class="lockup-img lockup-dark"  src="/assets/logos/cmds-logo-typo-white.png" alt="CMDSPACE" loading="lazy">
        <p class="lockup-tagline">Command your space.</p>
    </div>
</section>
```

```css
.brand-lockup {
    padding: clamp(64px, 8vw, 96px) var(--section-px);
    background: var(--bg);
    border-top: 1px solid var(--border);
}
.brand-lockup-inner { max-width: 640px; margin: 0 auto; text-align: center; }
.lockup-img { max-width: 320px; width: 100%; height: auto; display: block; margin: 0 auto; }
.lockup-dark { display: none; }
[data-theme="dark"] .lockup-light { display: none; }
[data-theme="dark"] .lockup-dark  { display: block; }
.lockup-tagline {
    margin-top: 24px;
    font-family: var(--font-display);
    font-size: 15px;
    font-weight: 500;
    letter-spacing: -0.01em;
    color: var(--fg-subtle);
}
```

### 1.5 Accent Word (Headlines 내 강조)

```html
<h1>사람과 <span class="accent-word">AI를 위한</span> 지식 아키텍처</h1>
```

```css
.accent-word { color: var(--cmds-green); }
[data-theme="dark"] .accent-word { color: var(--cmds-pink); }
```

**반드시 클래스 사용** — 인라인 `style="color: #134538"` 절대 금지 (다크 모드 전환 불가).

### 1.6 Hero "em" Gradient Text

```html
<h1 class="hero-title">
    Knowledge architecture<br>
    for <em>humans and AI</em>.
</h1>
```

```css
.hero-title em {
    font-style: normal;
    background: linear-gradient(135deg, var(--cmds-green) 0%, var(--cmds-green-bright) 50%, var(--cmds-green-glow) 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
}
[data-theme="dark"] .hero-title em {
    background: linear-gradient(135deg, #F4A4B8 0%, #E985A2 50%, #D16C8A 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
}
```

### 1.7 Full-Bleed CTA Block

```css
.cta-block {
    background: linear-gradient(135deg,
        var(--cmds-green) 0%,
        var(--cmds-green-hover) 60%,
        var(--cmds-green-bright) 100%);
    color: #fff;
    text-align: center;
    padding: clamp(72px, 10vw, 120px) var(--section-px);
    position: relative;
    overflow: hidden;
}
.cta-block::before {
    content: ''; position: absolute; inset: 0;
    background:
        radial-gradient(circle at 30% 30%, rgba(255,255,255,0.08), transparent 50%),
        radial-gradient(circle at 70% 70%, rgba(47,180,136,0.15), transparent 50%);
}

[data-theme="dark"] .cta-block {
    background: linear-gradient(135deg,
        var(--cmds-pink) 0%,
        var(--cmds-pink-dark) 55%,
        #B8577A 100%);
    color: #0b0f0d;
}
```

내부 버튼:
- `.btn-white` (흰 배경 + 브랜드 글자): 라이트에서 글자 `cmds-green`, 다크에서 `cmds-pink-dark`
- `.btn-outline` (투명 + 보더): 라이트 `#fff`, 다크 `#0b0f0d`

### 1.8 Sticky Header (Apple-style Blur)

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

## 2. Interactions (JS)

### 2.1 Light/Dark Toggle (localStorage 저장)

```javascript
function applyTheme(theme) {
    document.documentElement.dataset.theme = theme;
    localStorage.setItem('cmds-theme', theme);
    const icon = document.getElementById('themeIcon');
    if (theme === 'dark') {
        icon.innerHTML = '<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>';
    } else {
        icon.innerHTML = '<circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M4.93 19.07l1.41-1.41M17.66 6.34l1.41-1.41"/>';
    }
}
document.getElementById('themeToggle').addEventListener('click', () => {
    applyTheme(document.documentElement.dataset.theme === 'light' ? 'dark' : 'light');
});
applyTheme(localStorage.getItem('cmds-theme') || (window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light'));
```

### 2.2 KO/EN Lang Toggle

```javascript
const I18N = { en: {...}, ko: {...} };
function applyLang(lang) {
    document.documentElement.lang = lang;
    document.documentElement.dataset.lang = lang;
    document.querySelectorAll('[data-i18n]').forEach(el => {
        const key = el.dataset.i18n;
        if (I18N[lang][key]) el.textContent = I18N[lang][key];
    });
    localStorage.setItem('cmds-lang', lang);
}
```

HTML 사용:
```html
<span class="en-only">Read the docs</span>
<span class="ko-only">문서 읽기</span>
```

CSS:
```css
[data-lang="en"] .ko-only { display: none; }
[data-lang="ko"] .en-only { display: none; }
```

### 2.3 Double-click Empty Space → Scroll Top/Bottom

```javascript
document.addEventListener('dblclick', (e) => {
    const tag = e.target.tagName;
    // 인터랙티브 요소는 제외
    if (['A','BUTTON','INPUT','TEXTAREA','CODE','PRE','IMG','SVG','PATH','SPAN','MARK','KBD'].includes(tag)) return;
    // 본문·팔레트 내부는 제외 (docs 전용)
    if (e.target.closest('.doc-body') || e.target.closest('.palette')) return;
    // 텍스트 선택 중이면 비활성
    if (window.getSelection().toString().length > 0) return;

    const scrollY = window.scrollY;
    const max = document.documentElement.scrollHeight - window.innerHeight;
    window.scrollTo({ top: scrollY < max / 2 ? max : 0, behavior: 'smooth' });
});
```

### 2.4 IntersectionObserver Reveal (prefers-reduced-motion 존중)

```css
.reveal {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity .7s ease, transform .7s cubic-bezier(0.22, 0.61, 0.36, 1);
}
.reveal.visible { opacity: 1; transform: translateY(0); }
@media (prefers-reduced-motion: reduce) {
    .reveal { opacity: 1; transform: none; transition: none; }
}
```

```javascript
const io = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); io.unobserve(e.target); } });
}, { rootMargin: '-10% 0px -10% 0px' });
document.querySelectorAll('.reveal').forEach(el => io.observe(el));
```

### 2.5 Cross-Page Navigation (Landing ↔ Docs)

**랜딩 헤더**: Architecture · Process · Docs · GitHub · Primary CTA "Read the docs"
**문서 헤더**: 브랜드 로고 `href="/"` + inline "Home" · "GitHub" nav

```html
<nav class="header-nav-inline">
    <a href="/" class="nav-home">
        <svg><!-- home icon --></svg>
        <span data-i18n="nav.home">Home</span>
    </a>
    <a href="https://github.com/…" target="_blank" rel="noopener" class="nav-gh">
        <svg><!-- github icon --></svg>
        GitHub
    </a>
</nav>
```

## 3. Anti-Patterns (절대 금지)

| ❌ 잘못 | ✅ 올바름 | 이유 |
|--------|---------|------|
| `<link rel="icon" href="data:image/svg+xml,…§…">` | `<link rel="icon" href="/assets/logos/cmds-logo-round.png">` | 실제 CMDS 로고 사용 |
| `<meta property="og:image" content="/assets/og/og.png">` | `<meta property="og:image" content="https://{domain}/assets/og/og.png">` | 상대 경로는 Slack/Twitter 프리뷰 깨짐 |
| `<span style="color: #134538">강조</span>` | `<span class="accent-word">강조</span>` | 다크 모드 자동 전환 |
| `.dl-btn:hover { background: white }` (sidebar 안) | `.sidebar a.dl-btn:hover { background: green !important; }` | specificity `.sidebar a:hover` (0,2,1) > `.dl-btn:hover` (0,1,1) → white로 덮임 |
| `<picture media="prefers-color-scheme">` 다크 로고 | 2개 `<img>` + `[data-theme]` CSS 토글 | 수동 토글이랑 충돌 |
| 히어로 상단 로고 + 아이브로우 "CMDS" 텍스트 | 둘 중 하나만 (헤더 28px + 하단 lockup 권장) | 시각 중복 |
| 브랜드 마크 배경 녹색 + 로고 안에 또 색상 | `border-radius: 50%; object-fit: contain;` 만 | 라운드 로고는 자체 투명 영역 포함 |
| 다크 모드 primary CTA 에 녹색 + 흰글자 | 다크 모드 CTA 는 핑크 + 어두운 글자 | CI 규칙 (v2.5 에서 확정) |

## 4. Migration Learnings (2026-04-18~19 세션)

### 4.1 중요 결정 기록

1. **Vercel 프로젝트 이름의 "-v2" 는 인프라 iteration** — 시스템 파일 콘텐츠 버전과 무관
2. **GitHub ↔ Vercel 자동 연결 없음** — 각 사이트는 수동 `vercel deploy --prod --yes`
3. **Cloudflare DNS**: `cmdspace.work` apex 하위 17개 서브도메인, 대부분 A record `76.76.21.21` (Vercel) 또는 CNAME `cname.vercel-dns.com`
4. **Tunnel 도메인** (`dify`, `n8n`, `openwebui` 등) 은 웹사이트 아님 — 도구 endpoint
5. **LG/AX 제외 룰** — `lg.cmdspace.work` · `ax.cmdspace.work` · `test.cmdspace.work` 는 고객사 퍼블리시, 수정 금지

### 4.2 실수·함정 기록

- **index.html 실수로 옛 버전 동기화** 문제 발생: vault backup 폴더의 old `index.html` 과 프로덕션 HTML 사이의 divergence. → 항상 프로덕션 현재 HTML 을 baseline 으로 패치.
- **파비콘 하드리프레시 필요**: 크롬이 파비콘 캐시 오래 유지 → `Cmd+Shift+R`
- **OG 이미지 외부 리소스 의존 시 Chrome headless 가 로드 못할 수 있음** → 로고 PNG 를 템플릿 폴더에 복사 후 상대경로로 참조
- **Copy 버튼 CSS specificity** — `.sidebar a:hover { background: white }` 가 버튼 `:hover` 를 덮어 흰색으로 변함 → `.sidebar a.dl-btn:hover` 로 구체화

### 4.3 CMDS Color System 진화 이력

세션 중 v2.0 → v2.5 로 5단계 진화:
- v2.0 — CI/BI 분리 · Obsidian 그래프 팔레트 · Apple 타이포
- v2.1 — Copy Button Progressive Disclosure · CSS Specificity 주의 · Interaction Patterns
- v2.2 — `.accent-word` 확정 · Full-Bleed CTA 다크 핑크 그라디언트
- v2.3 — 공식 로고 6종 등록
- v2.4 — 히어로 상단 로고 기본 사용 안 함 결정
- v2.5 — OG 이미지 시스템 정식 등록 (17 메타 체크리스트 포함)

### 4.4 사용자 피드백에서 확정된 룰

- "어두운 버튼에는 밝은 글씨" → 다크 버튼 대비 룰
- "마우스 오버 했을 때 과하게 밝아져서 안 보임" → specificity fix
- "다크모드 하이라이트는 #E985A2 핑크" → CMDS Pink 등재
- "히어로 로고 제거, 헤더 + footer lockup 으로 분산" → v2.4 결정
- "OG 누락 없게 신경" → 17 메타 체크리스트 정식화
- "CTA 블록 다크에서 핑크 계열로" → `.cta-block` 다크 그라디언트
