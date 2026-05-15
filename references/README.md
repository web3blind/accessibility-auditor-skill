# References

This directory contains the portable reference layer for the accessibility-auditor skill.

These files are intended to stay mostly runtime-agnostic:
- standards and criteria
- platform checklists
- deeper-testing suggestions
- compliance mapping

The runtime should decide how to fetch pages, read files, render UI, or run optional tools.
The references here define **what to check**, not vendor-specific tool calls.

| File | Contents |
|------|----------|
| wcag-criteria.md | Full WCAG 2.1 criteria reference - Level A, AA, and relevant 2.2 notes |
| additional-checks.md | Extra product/web checks beyond the core WCAG pass |
| gost-checklist.md | Russian GOST R 52872-2019 and Mincifry order checklist |
| mobile-checklist.md | Mobile app static analysis - Android, iOS, Flutter, React Native |
| desktop-checklist.md | Desktop app static analysis - Electron, WPF, PyQt, wxWidgets, GTK |
| tools.md | Recommended deeper-testing tools by platform |
| international-standards.md | Supplemental international standards note |
