# Plan: Accessibility Auditor Skill for Hermes

## Goal

Create a Hermes skill that enables an AI agent to perform comprehensive
accessibility audits on websites, GitHub repositories, and local project folders.
Additionally, document capabilities and limitations for mobile and desktop apps.

## Scope

### In Scope
- Website auditing via URL (WCAG 2.1, GOST R 52872-2019, Mincifry checklist)
- GitHub repository auditing (source code analysis for accessibility patterns)
- Local folder auditing (same as GitHub but for local paths)
- Mobile app source code static analysis (Android, iOS, Flutter, React Native)
- Desktop app source code static analysis (Electron, PyQt, wxWidgets)
- Structured reporting with severity levels and recommendations

### Out of Scope
- Running the actual websites (no headless browser in the skill itself)
- Installing accessibility testing frameworks
- Automated CI/CD pipeline setup
- The existing accessibility-auditor project (bot, API, web) — don't touch it

## Deliverables

1. `~/.hermes/skills/accessibility-auditor/SKILL.md` — main skill instructions
2. `references/web-checklist.md` — comprehensive web accessibility checklist
3. `references/mobile-checklist.md` — mobile app accessibility checklist
4. `references/desktop-checklist.md` — desktop app accessibility checklist
5. `references/tools.md` — analysis tools by platform
6. `references/wcag-criteria.md` — WCAG 2.1 criteria reference
7. `references/gost-checklist.md` — Russian GOST/Mincifry requirements

## Implementation Tasks

1. Create skill directory structure
2. Write SKILL.md with full workflow
3. Write web checklist reference (from docx + WCAG 2.1)
4. Write mobile checklist reference
5. Write desktop checklist reference
6. Write tools reference
7. Write WCAG criteria quick reference
8. Write GOST/Mincifry checklist reference

## Architecture Decisions

### Source Type Detection
The skill detects input type automatically:
- URL starting with http/https → website audit
- URL containing github.com → GitHub repo audit
- Local path → folder audit
- Mixed → multi-target audit

### Analysis Approach
- Websites: use web_extract + browser tools to fetch HTML, then analyze
- GitHub repos: use web_extract on raw files + GitHub API
- Local folders: use read_file + search_files on source code
- All: AI-driven analysis following checklists in references/

### Report Structure
Every audit produces:
1. Executive summary (score, grade, critical issues count)
2. Issues by category with severity (critical/warning/info)
3. Platform-specific recommendations
4. WCAG/GOST compliance mapping
5. Next steps

## Definition of Done

- SKILL.md is complete and actionable
- All reference files are populated with real checklists
- Skill correctly handles all input types (URL, GitHub, folder)
- Report format is clear and useful for both technical and non-technical readers
- Mobile/desktop limitations are documented honestly
