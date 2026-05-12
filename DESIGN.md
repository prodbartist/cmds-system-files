---
version: alpha
name: CMDS System Files Design System
description: >-
  Design tokens for CMDSPACE (커맨드스페이스) web surfaces — Apple SF Pro typography
  paired with the CMDS Green/Pink palette. Used by system.cmdspace.work,
  cmdspace.work, llm-wiki.cmdspace.work, and any CMDS-branded landing or docs
  page. Light mode anchors on CMDS Green (#134538); dark mode pivots to
  CMDS Pink (#E985A2) as the highlight color.
colors:
  # ── Brand · CMDS Green (primary, light mode accent)
  cmds-green:        "#134538"
  cmds-green-hover:  "#1A5D4B"
  cmds-green-bright: "#22896A"
  cmds-green-glow:   "#2FB488"
  cmds-green-50:     "#F1F7F4"
  cmds-green-100:    "#DCEBE3"
  cmds-green-200:    "#BAD9C9"
  cmds-green-800:    "#0D3529"
  cmds-green-900:    "#0A2820"

  # ── Brand · CMDS Pink (dark mode accent)
  cmds-pink:         "#E985A2"
  cmds-pink-light:   "#F4A4B8"
  cmds-pink-dark:    "#D16C8A"
  cmds-pink-soft:    "#2B1922"

  # ── Light mode surfaces
  bg:                "#FBFBFA"
  bg-elev:           "#FFFFFF"
  bg-subtle:         "#F5F6F4"
  bg-code:           "#F5F5F3"

  # ── Light mode foreground
  fg:                "#0B0D0C"
  fg-muted:          "#4A544F"
  fg-subtle:         "#8A938E"

  # ── Light mode borders
  border:            "#E6E8E6"
  border-strong:     "#D0D3D0"

  # ── Dark mode surfaces
  bg-dark:           "#0B0F0D"
  bg-dark-elev:      "#0D1411"
  bg-dark-subtle:    "#0A1110"

  # ── Dark mode foreground
  fg-dark:           "#F2F4F3"
  fg-dark-muted:     "#9AA39D"
  fg-dark-subtle:    "#626A66"

  # ── Dark mode borders
  border-dark:       "#1A231F"
  border-dark-strong:"#26302A"

  # ── Semantic
  on-accent:         "#FFFFFF"
  on-accent-dark:    "#0B0F0D"
  warn:              "#B45309"

typography:
  hero:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Pretendard', sans-serif"
    fontSize: "clamp(48px, 8vw, 104px)"
    fontWeight: 700
    lineHeight: 1.02
    letterSpacing: "-0.042em"
  h1:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Pretendard', sans-serif"
    fontSize: "clamp(36px, 5vw, 60px)"
    fontWeight: 700
    lineHeight: 1.1
    letterSpacing: "-0.028em"
  h2:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Pretendard', sans-serif"
    fontSize: "clamp(24px, 2.6vw, 36px)"
    fontWeight: 600
    lineHeight: 1.2
    letterSpacing: "-0.018em"
  h3:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Pretendard', sans-serif"
    fontSize: "32px"
    fontWeight: 700
    lineHeight: 1.25
    letterSpacing: "-0.028em"
  lead:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Pretendard', sans-serif"
    fontSize: "clamp(19px, 1.8vw, 22px)"
    fontWeight: 400
    lineHeight: 1.5
    letterSpacing: "-0.015em"
  body-lg:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Pretendard', sans-serif"
    fontSize: "17px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "-0.011em"
  body-md:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Pretendard', sans-serif"
    fontSize: "15px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "-0.011em"
  body-sm:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Pretendard', sans-serif"
    fontSize: "14px"
    fontWeight: 400
    lineHeight: 1.5
    letterSpacing: "-0.008em"
  label:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'SF Pro Text', 'Pretendard', sans-serif"
    fontSize: "13px"
    fontWeight: 600
    lineHeight: 1.3
    letterSpacing: "-0.005em"
  code:
    fontFamily: "ui-monospace, 'SF Mono', 'Menlo', 'JetBrains Mono', Consolas, monospace"
    fontSize: "0.9em"
    fontWeight: 400
    lineHeight: 1.5

rounded:
  none:  "0px"
  sm:    "6px"
  md:    "8px"
  lg:    "16px"
  xl:    "20px"
  pill:  "999px"
  round: "50%"

spacing:
  xs:       "4px"
  sm:       "8px"
  md:       "16px"
  lg:       "24px"
  xl:       "32px"
  "2xl":    "48px"
  "3xl":    "80px"
  section:  "clamp(24px, 5vw, 80px)"
  block:    "clamp(80px, 10vw, 140px)"

layout:
  max-width-page:    "1200px"
  max-width-content: "720px"
  sidebar-width:     "280px"
  toc-width:         "240px"
  header-height:     "56px"

components:
  # ── Buttons (all radius pill, weight 500, letter -0.01em)
  button-primary:
    backgroundColor: "{colors.cmds-green}"
    textColor: "{colors.on-accent}"
    typography: "{typography.body-md}"
    rounded: "{rounded.pill}"
    padding: "14px 24px"
  button-primary-dark:
    backgroundColor: "{colors.cmds-pink}"
    textColor: "{colors.on-accent-dark}"
    typography: "{typography.body-md}"
    rounded: "{rounded.pill}"
    padding: "14px 24px"
  button-secondary:
    backgroundColor: "{colors.bg-elev}"
    textColor: "{colors.fg}"
    rounded: "{rounded.pill}"
    padding: "14px 24px"
  button-ghost:
    backgroundColor: "transparent"
    textColor: "{colors.fg-muted}"
    rounded: "{rounded.pill}"
    padding: "10px 14px"

  # ── Cards
  card:
    backgroundColor: "{colors.bg-elev}"
    textColor: "{colors.fg}"
    rounded: "{rounded.xl}"
    padding: "28px 32px"
  card-subtle:
    backgroundColor: "{colors.bg-subtle}"
    textColor: "{colors.fg}"
    rounded: "{rounded.lg}"
    padding: "24px"

  # ── Chips / pills
  chip:
    backgroundColor: "{colors.bg-subtle}"
    textColor: "{colors.fg-muted}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.pill}"
    padding: "6px 14px"

  # ── Logo mark
  logo:
    rounded: "{rounded.round}"
    size: "32px"

  # ── Code block (inline)
  code-inline:
    backgroundColor: "{colors.bg-code}"
    textColor: "{colors.fg}"
    typography: "{typography.code}"
    rounded: "{rounded.sm}"
    padding: "2px 6px"
---

# CMDS System Files Design System

## Overview

The CMDS design system powers the public-facing web surfaces of **CMDSPACE
(커맨드스페이스)** — a knowledge architecture operated by **구요한 (Yohan Koo)**.
The system documents the visual language behind `system.cmdspace.work` (the
landing + technical docs for the 5 core system files), `cmdspace.work` (the
operator's personal hub), and any sibling subdomain that needs to feel like
part of the same family.

The aesthetic is **Apple-engineered typography paired with a
practitioner-researcher palette**: SF Pro Display/Text for headings and body,
SF Mono for code, with CMDS Green (`#134538`) anchoring light mode and CMDS
Pink (`#E985A2`) lighting up dark mode. The brand is quiet, dense with
information, and biased toward long-form reading — closer to a documentation
site than a marketing landing page.

Primary use cases:

- Public landing pages for CMDS subdomains
- Long-form technical documentation
- Editorial / essay pages (e.g., 더배러 newsletter mirror)
- AI coding agents (Claude Code, Codex, Cursor, Antigravity) building new
  CMDS-branded surfaces — this file is the single source of truth.

## Colors

**Light mode (default).** Warm off-white surface (`#FBFBFA`) over near-black
text (`#0B0D0C`). The primary accent is **CMDS Green** — used for CTAs,
links, focus rings, and emphatic body text. Greens beyond `cmds-green` are
calibrated for hover, bright callouts, and tonal backgrounds (the `50/100/200`
ramp is for soft fills; `800/900` is for high-contrast badges).

**Dark mode.** Near-black warm surface (`#0B0F0D`) over off-white text
(`#F2F4F3`). The primary accent flips to **CMDS Pink** — the green never
appears as a CTA color in dark mode. Pink ramps from `light` for hover up to
`dark` for active states, with `pink-soft` (`#2B1922`) as a tinted background.

**Semantic tokens.**

- `bg` / `bg-elev` / `bg-subtle` — page, elevated surface, sunken surface
- `fg` / `fg-muted` / `fg-subtle` — primary text, secondary text, tertiary text
- `border` / `border-strong` — hairlines and emphatic separators
- `on-accent` — text color on top of the accent (`#FFFFFF` light, near-black dark)
- `warn` — single semantic warning color (`#B45309`)

The palette is intentionally narrow. There are no blue/purple/red accents and
no semantic success/info colors — confirmations use foreground tone, errors
borrow the warn color.

## Typography

The typeface stack is **Apple system fonts first, Pretendard as Korean
fallback** — SF Pro Display for display sizes (`hero`, `h1`, `h3`), SF Pro
Text for everything else, SF Mono for code, and New York (serif) reserved
for editorial / essay surfaces only.

Type scale follows a fluid pattern using `clamp()` so that hero and h2 sizes
scale gracefully across mobile and desktop. The two unbreakable rules:

1. **Tight letter-spacing on display sizes.** Hero is `-0.042em`, h1/h3 is
   `-0.028em`. Body sits at `-0.011em`. This is what makes the type feel
   Apple-engineered rather than generic.
2. **Body line-height is 1.55**, not the default 1.5. Long-form reading is
   the primary use case.

Use `typography.lead` for the single sentence that follows a hero or h2 —
it bridges display and body sizes. Use `typography.label` (13px, weight 600,
slight letter-spacing tightening) for category badges and metadata rows.

## Layout

The system uses **two page widths**:

- `max-width-page` (`1200px`) — landing pages, marketing surfaces. Section
  padding is fluid (`clamp(24px, 5vw, 80px)`).
- `max-width-content` (`720px`) — documentation, essays, long-form reading.
  This is the reading column; everything else (sidebar, TOC) sits outside it.

Documentation surfaces use a **three-column grid**: `sidebar-width` (280px)
+ `max-width-content` (720px) + `toc-width` (240px). The sidebar collapses
below the lg breakpoint; the TOC collapses below the xl breakpoint.

Vertical rhythm uses two scales:

- `spacing.section` (`clamp(24px, 5vw, 80px)`) — horizontal page padding
- `spacing.block` (`clamp(80px, 10vw, 140px)`) — vertical gap between top-level page sections

The site header is `56px` tall and behaves as a sticky top bar with a
hairline border-bottom.

## Elevation & Depth

Elevation is **flat by default**. Hairline borders carry most of the
hierarchy work. Two shadow recipes exist:

- **Card shadow** (rest):
  `0 1px 2px rgba(19, 69, 56, 0.06)` — a soft tint of CMDS Green.
- **Card shadow** (hover): adds `0 8px 24px -8px rgba(19, 69, 56, 0.18)`.

Primary buttons get a richer treatment — they combine an inset top
highlight (`inset 0 1px 0 rgba(255,255,255,0.12)`) with two stacked drop
shadows. This is the only place pseudo-3D treatment is allowed; everything
else stays flat.

Dark mode replaces the green-tinted shadows with neutral black at higher
opacity (`rgba(0,0,0,0.4)`) and re-tints the primary button shadows with
CMDS Pink.

## Shapes

The corner radius scale is opinionated. Buttons and chips are **pill-shaped**
(`rounded.pill` = `999px`). Cards are **soft-cornered** (`rounded.xl` =
`20px`). Inline code uses `rounded.sm` (`6px`). The logo mark is always a
**perfect circle** (`rounded.round` = `50%`) — never a square or
rounded-square.

There is no `none` radius outside `<hr>` rules and full-bleed dividers.
Sharp corners read as "unfinished" in this system.

## Components

### Buttons

Three variants — primary, secondary, ghost — all pill-shaped, all using
`typography.body-md` (15px / weight 500 / letter-spacing `-0.01em`).

- **Primary (light)**: CMDS Green background, white text, double-stack
  shadow + inset highlight. Hover darkens to `cmds-green-hover`. Active
  scales to `0.985` (no other component uses transform).
- **Primary (dark)**: CMDS Pink background, near-black text. Hover darkens
  to `cmds-pink-dark`.
- **Secondary**: `bg-elev` background, `border-strong` border. Hover swaps
  background to `bg-subtle`, border to `fg-subtle`.
- **Ghost**: transparent, `fg-muted` text, tighter padding (`10px 14px`).
  Used inside dense rows where a full button would dominate.

### Cards

`card` uses `bg-elev` + `rounded.xl` + `28px 32px` padding. For grids of
many cards, use `card-subtle` (sunken into `bg-subtle`, `rounded.lg`,
tighter `24px` padding).

### Chips

Pill-shaped, `bg-subtle` background, `fg-muted` text, `body-sm` typography,
`6px 14px` padding. Used for metadata badges (version numbers, dates,
precedence ranks).

### Code (inline)

`bg-code` background, `rounded.sm`, `2px 6px` padding, monospace `0.9em`.
Block code uses the same background but no rounded corners on the outer
container — the surrounding card does the rounding.

### Logo

The CMDS logo is **always a circular mark** (32px in the header, scales up
for hero placements). The asset lives at
`/assets/logos/cmds-logo-round.png` and is reused as both `favicon` and
`apple-touch-icon`.

## Do's and Don'ts

### Do

- **Do** use SF Pro / SF Pro Display first. Pretendard is the Korean
  fallback, not a replacement. New York is reserved for editorial surfaces.
- **Do** preserve `letter-spacing: -0.011em` on body and tighter on
  display. This is the dominant visual signature.
- **Do** flip the primary accent from CMDS Green (light) to CMDS Pink
  (dark) — never use green CTAs in dark mode.
- **Do** keep cards on `rounded.xl` (20px). Smaller radii on cards read as
  generic Material.
- **Do** use `spacing.block` for vertical gaps between top-level page
  sections. Tight vertical rhythm breaks the editorial feel.
- **Do** include 17 Open Graph / Twitter meta tags on every public page,
  with a dedicated 1200×630 OG image. The CMDS surface is link-shared
  heavily.

### Don't

- **Don't** introduce additional accent colors (blue / purple / red). The
  CMDS palette is intentionally narrow.
- **Don't** use square or rounded-square logos. The mark is always a circle.
- **Don't** apply box shadows to non-button components by default. Cards
  rely on hairline borders.
- **Don't** use sharp corners on buttons. Pills are the only shape; even
  small icon buttons follow the pill (or `round` for circular icon-only
  buttons).
- **Don't** stack more than two shadow layers — the primary button is the
  only place where layered shadows are warranted.
- **Don't** let body line-height drop below 1.5. Long-form reading is the
  primary use case.

---

**Maintained by**: 구요한 (Yohan Koo) · CMDSPACE · `johnfkoo951@gmail.com`
**Canonical URL**: `https://system.cmdspace.work/DESIGN.md` (once deployed)
**Source repo**: `https://github.com/johnfkoo951/cmds-system-files`
**Spec**: `https://github.com/google-labs-code/design.md` (alpha)
