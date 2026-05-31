# CMDS System Files

> 6 Core System Files + 8 Shared Rules + 9 Architecture Patterns that power the CMDSPACE Personal Knowledge Management ecosystem.

## Live Demo

**https://system.cmdspace.work**

## Overview

CMDS (CMDSPACE) is a comprehensive Personal Knowledge Management (PKM) system built on Obsidian with 10,000+ notes. This repository contains the core system files that provide complete guidance for AI agents and human users working with the vault.

## What's New in v4.9.0 (2026-05-30)

- **8→9 propagation complete** — DESIGN.md (precedence 9) is now fully surfaced across every public layer (index, docs, OG meta, README). The system files scheme is **9 total**: 6 publicly deployed + 3 private.
- **DESIGN.md is the 6th public download** — added to the `files/` bundle and download list (Visual Language spec — CMDS Green/Pink, SF Pro + Pretendard, Anti-AI-Slop rules).
- **8 shared rules** — `blank-line-rules.md` (Obsidian-tight markdown) included alongside the original 7.
- **Engine hardening** — `system-docs-updater` upgraded to a 6-file sweep with a built-in count-canon (9 total / 6 public / 3 private / 8 rules) and a pre-deploy grep gate that blocks stale `5-file` / `5-way` labels before publishing.
- **git tags backfilled** — v4.7.0 and v4.8.0 tags restored; cmds-vault starter kit gains DESIGN.md (v1.2.0).

## Previous Highlights

- **v4.8.0** (2026-05-27) — 8→9 transition declared (DESIGN.md as precedence 9); 7-way satellite sync routine (mothership + cmds-vault + LLM Wiki)
- **v4.6.0** (2026-05-13) — `DESIGN.md` + `design-tokens.json` design-system surface added
- **v4.4** (2026-05-03) — 8-file scheme + Codex/Antigravity output lanes
- **v4.2** (2026-04-15) — CMDS Process Command Suite (8 slash commands: `/connect`, `/merge`, `/develop`, `/share` + `/inbox`, `/lint`, `/query`, `/status`)
- **v4.1** (2026-04-07) — `description` field (English, LLM relevance hint) added as required property; 7 required properties total
- **v4.0** (2026-04-01) — Shared rules (`.claude/rules/`) via `@include`; 9 architecture patterns; enhanced frontmatter (`precedence`, `memory-type`, `token-estimate`, etc.)
- **v3.0** (2026-03-15) — Structured YAML frontmatter; share system with placeholder rules
- **v2.0** (2026-01-20) — 5-file architecture (CLAUDE.md, AGENTS.md, CMDS.md, CMDS Guide, CMDS Head Quarter)
- **v1.0** (2025-10-01) — Initial system files

See [CHANGELOG.md](CHANGELOG.md) for full history.

## Repository Structure

```
files/
├── CLAUDE.md              # Claude Code technical guide (precedence: 1)
├── AGENTS.md              # Other AI agents guide (precedence: 2)
├── CMDS.md                # System philosophy for all LLMs (precedence: 4)
├── CMDS-Guide.md          # Operational standards (precedence: 5)
├── CMDS-Head-Quarter.md   # Navigation hub (precedence: 6)
├── DESIGN.md              # Visual language spec (precedence: 9)
└── CMDS-System-Files.zip  # All files bundled

rules/
├── indentation-rules.md        # YAML 2-spaces / Markdown TAB
├── frontmatter-standard.md     # 7 required properties + format
├── file-creation-rules.md      # Output path, naming, project folders
├── wikilink-rules.md           # Obsidian wikilink syntax + YAML quoting
├── directory-structure.md      # Vault folder structure + CMDS categories
├── mermaid-rules.md            # Mermaid diagram quoting rules (Obsidian)
├── blank-line-rules.md         # Obsidian-tight blank line rules
└── video-project-workflow.md   # Remotion / video project placement rules

CHANGELOG.md               # Version history
```

## The 6 Core Files

These are the 6 publicly deployed files. The full scheme is **9 total** — the other 3 (ANTIGRAVITY.md precedence 3 = Gemini-only; BRAIN.md precedence 7 and BRAIN_PROMPT.md precedence 8 = Gobi persona) are private and not distributed here.

### For AI Agents (loaded into context window)

| File | Audience | Focus | Precedence |
|------|----------|-------|:----------:|
| **CLAUDE.md** | Claude Code | Technical implementation (HOW) | 1 |
| **AGENTS.md** | Gemini, Codex, Cursor | Portable technical rules (HOW) | 2 |
| **CMDS.md** | All LLM assistants | Context & philosophy (WHY/WHAT) | 4 |

### For Humans (referenced in Obsidian)

| File | Audience | Focus | Precedence |
|------|----------|-------|:----------:|
| **CMDS Guide** | User + AI | Operational standards | 5 |
| **CMDS Head Quarter** | User | Navigation hub | 6 |

### Visual Language (loaded when producing visual artifacts)

| File | Audience | Focus | Precedence |
|------|----------|-------|:----------:|
| **DESIGN.md** | All agents producing visual output | Visual language spec (HOW — visual) | 9 |

## Architecture Patterns (from Claude Code Source Analysis)

| # | Pattern | Purpose |
|---|---------|---------|
| 1 | **precedence** | File priority ordering (1-5) for conflict resolution |
| 2 | **STATIC/DYNAMIC** | Cache-aware sections for AI processing |
| 3 | **@include** | Shared rules via file inclusion (AI reads inline) |
| 4 | **Essential** | Post-compact recovery — core rules that survive context compression |
| 5 | **required-for/optional-for** | Agent scoping — which tasks need which files |
| 6 | **memory-type** | Maps to Claude Code's memdir types (feedback/user/reference) |
| 7 | **token-estimate** | Token budget awareness for AI load prioritization |
| 8 | **changelog** | Inline version history in each file's frontmatter |
| 9 | **shared rules** | Common rules in `.claude/rules/` shared via @include |

## @include vs [[wikilink]]

| Syntax | Purpose | Used By |
|--------|---------|---------|
| `@path` | AI reads file content inline | AI agents (Claude Code, etc.) |
| `[[name]]` | Obsidian internal link for navigation | Obsidian graph view, backlinks |
| Both together | `@file → [[file]]` | When both AI loading and human navigation needed |

## CMDS Process

```
Connect → Merge → Develop → Share
```

| Stage | Categories | What Happens |
|-------|-----------|--------------|
| **Connect** | 100 Themes | Discover ideas, capture interests |
| **Merge** | 200 Literature | Integrate knowledge, build theory |
| **Develop** | 300-600 | Collect data, apply methods, use tools |
| **Share** | 700-800 | Create content, publish, teach, consult |

## Getting Started

1. **Download** all files from [system.cmdspace.work](https://system.cmdspace.work)
2. **Place** system files in the root of your Obsidian vault
3. **Place** rules in `.claude/rules/` directory
4. **Customize** placeholders (`{your-name}`, `{vault-path}`, etc.)
5. **Reference** CMDS.md in your AI conversations for context

## Stats

| Metric | Value |
|--------|-------|
| Core System Files | 6 |
| Shared Rules | 8 |
| Slash Commands (CMDS Process) | 8 |
| Architecture Patterns | 9 |
| Required Frontmatter Properties | 7 |
| CMDS Categories | 9 (100-900) |
| Subcategories | 91 |
| Vault Notes | 10,000+ |

## Download

- [Download All (ZIP)](https://system.cmdspace.work/files/CMDS-System-Files.zip)
- [Browse Files](https://system.cmdspace.work/#download)

## Links

- [Profile](https://litt.ly/cmds)
- [YouTube](https://www.youtube.com/@cmdspace)
- [X (Twitter)](https://x.com/YohanKoo)
- [LinkedIn](https://www.linkedin.com/in/yohan-koo-a1baa3138/)
- [Threads](https://www.threads.com/@cmds_pace)
- [Education](https://class.cmdspace.kr/)

## License

All intellectual property rights belong to CMDSPACE.

---

Last Updated: 2026-05-30 · v4.9.0
