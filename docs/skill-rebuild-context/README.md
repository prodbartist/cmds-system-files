# v4.3 Skill Rebuild Context

> **목적**: `cmdspace-web-builder` 스킬을 v4.3 표준으로 리빌딩하기 위한 컨텍스트 집약 문서.
> 이 폴더의 4개 문서가 새 스킬 제작에 필요한 모든 배경지식·패턴·결정사항을 담고 있음.

## 왜 이 문서들이 필요한가?

2026-04-18~19 세션에서 `system.cmdspace.work` 를 v4.3 표준으로 리빌딩하면서 **실전 검증된 디자인 시스템 (CMDS Color System v2.5)** 이 도출됨. 이 경험을 바탕으로 기존 `cmdspace-web-builder` 스킬 (Brutalist 기반, v4.3 이전) 을 전면 업데이트하려 함.

컨텍스트가 거의 차서 이 세션에서 직접 스킬 업데이트를 못 함. 다음 세션에서 이어가도록 배경을 집약.

## 문서 구성

| 파일 | 내용 |
|------|------|
| `README.md` (이 파일) | 네비게이션 + 전체 맥락 요약 |
| **[01-STANDARDS.md](01-STANDARDS.md)** | v4.3 디자인 표준 — 색상·타이포·에셋·레이아웃 토큰 전부 |
| **[02-PATTERNS.md](02-PATTERNS.md)** | 컴포넌트 레시피·인터랙션·Anti-patterns·실전 교훈 |
| **[03-SKILL-SPEC.md](03-SKILL-SPEC.md)** | 새 스킬 제작 스펙 — 템플릿 타입·빌드 파이프라인·마이그레이션 범위 |

## 핵심 전제 3가지

1. **Reference Implementation**: `/Users/yohankoo/DEV/cmds-system-files/` 가 v4.3 표준의 **살아있는 레퍼런스**.
   - 랜딩: https://system.cmdspace.work (`index.html`)
   - 문서: https://system.cmdspace.work/docs/ (`docs/index.html`)
   - 구버전: https://system.cmdspace.work/index-brutalist.html (아카이브, 비교 참조용)

2. **Canonical Source (볼트)**:
   - [[CMDS Color System]] v2.5 — `50. Assets/51. Brand/CMDS Color System.md`
   - [[v4.3-minimal-snippet]] — `50. Assets/51. Brand/v4.3-minimal-snippet.md` (복붙 키트)
   - 마이그레이션 계획 — `70. Outputs/71. Published/2026-04-19-CMDS 웹사이트 v4.3 마이그레이션 계획.md`

3. **Build Pipeline**:
   - Vercel CLI 수동 배포 (GitHub Auto-deploy 없음)
   - Chrome headless 로 OG 이미지 자동 생성 (`scripts/build-og.sh`)
   - DEV 폴더가 배포 소스 원천

## v4.3 이전과 뭐가 달라졌나 (요약)

| 영역 | Pre-v4.3 (Brutalist) | v4.3 (현행) |
|------|---------------------|-------------|
| 색상 | 흑백 + Toxic Green `#CCFF00` | CMDS Green `#134538` (CI) + Pink `#E985A2` (dark accent) |
| 타이포 | Space Grotesk + JetBrains Mono | Apple SF Pro (SF Pro Display/Text) + Pretendard (한글) |
| 톤 | 날카로운 브루탈리즘 · 두꺼운 보더 | 애플 editorial · 부드러운 shadow · tight letter-spacing |
| 로고 | 인라인 SVG `§` placeholder | 실제 라운드 로고 PNG (`cmds-logo-round.png`) |
| 파비콘 | Data URL SVG | `/assets/logos/cmds-logo-round.png` |
| OG 이미지 | 없음 또는 부실 | 1200×630 PNG + 17 메타 태그 + Chrome headless 자동 생성 |
| 다크모드 | 단순 반전 | Pink accent 전환 (brand mark만 녹색 고정) |
| 코드 복사 | 숨김 (pre:hover 시 보임) | Progressive disclosure (0.4 → 0.85 → 1) |
| 강조 단어 | 인라인 `style="color"` | `.accent-word` 클래스 (테마 자동 전환) |

## 우선순위

스킬 리빌드의 **최소 버전** 은 아래 6개 템플릿 타입을 커버해야 함:

1. **Landing** — 마케팅 랜딩 (system.cmdspace.work 레퍼런스)
2. **Editorial Documentation** — 기술 문서 (system.cmdspace.work/docs 레퍼런스)
3. **Showcase** — 컨퍼런스/연구 쇼케이스 (sicem, course 대상)
4. **Archive** — 개인/행사 아카이브 (yhn spring camp, windlight)
5. **Technical Product** — 도구 소개 (cmdtrace)
6. **Brutalist Legacy** — 기존 Brutalist 스타일 유지 변형 (hrprompt)

자세한 템플릿 스펙은 `03-SKILL-SPEC.md` 참조.

## 다음 세션 시작 프롬프트 (복붙용)

```
`cmdspace-web-builder` 스킬을 v4.3 표준으로 리빌딩할 거야.

배경지식은 /Users/yohankoo/DEV/cmds-system-files/docs/skill-rebuild-context/
에 README.md + 01-STANDARDS.md + 02-PATTERNS.md + 03-SKILL-SPEC.md 로 정리해뒀어.
먼저 4개 다 읽어서 컨텍스트 복구하고, 03-SKILL-SPEC.md 의 계획대로 진행해줘.

레퍼런스 구현: /Users/yohankoo/DEV/cmds-system-files/
원천 디자인: [[CMDS Color System]] v2.5 @ 50. Assets/51. Brand/
복붙 키트: [[v4.3-minimal-snippet]] @ 50. Assets/51. Brand/

시작할 때 `skill-creator` 스킬 참조.
```

## 관련 문서 (볼트)

- [[CMDS Color System]] — v2.5 디자인 표준 원천
- [[v4.3-minimal-snippet]] — 복붙 스니펫 키트
- [[2026-04-19-CMDS 웹사이트 v4.3 마이그레이션 계획]] — 10개 사이트 이관 계획
- [[2026-04-19-CMDS System Files 공개 안내문]] — system.cmdspace.work 런칭 카피
- [[CLAUDE.md]] — "📦 System Files Deployment" 섹션
