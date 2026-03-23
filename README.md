# Accessibility Auditor — Hermes Skill

A Hermes AI skill for comprehensive accessibility auditing of websites, GitHub repositories, local project folders, and mobile/desktop app source code.

Built by a blind developer. Based on WCAG 2.1, GOST R 52872-2019, and the Russian Mincifry accessibility order.

## What It Does

The skill guides the AI agent through a structured accessibility audit workflow. You give it a target — a URL, a GitHub repo, or a local path — and the agent:

1. Fetches and analyzes the source (HTML, JS, layout XML, Swift, Dart, etc.)
2. Applies the appropriate checklist for the platform
3. Reports issues by severity with specific fix recommendations
4. Maps findings to WCAG 2.1 / GOST R 52872-2019 criteria
5. Scores the result (0–100) and assigns a letter grade

## Supported Targets

| Target | How to provide | Analysis quality |
|--------|---------------|-----------------|
| Website | Any public URL | Full static HTML/CSS/ARIA analysis |
| GitHub repo | GitHub URL | Source code analysis for web, mobile, desktop |
| Local folder | Absolute or relative path | Same as GitHub — reads files directly |

## Supported Platforms

### Web / Electron
- Full WCAG 2.1 AA checklist (60+ checks)
- GOST R 52872-2019 / Mincifry order compliance
- HTML structure, ARIA, keyboard navigation, contrast hints, forms

### Mobile Apps (static source analysis)
| Framework | What's checked statically |
|-----------|--------------------------|
| Android (XML + Kotlin/Java) | Missing contentDescription, labelFor, focusable, importantForAccessibility misuse |
| iOS (Swift / SwiftUI) | Missing accessibilityLabel, accessibilityRole, incorrect accessibilityHidden |
| Flutter (Dart) | Images without semanticLabel, GestureDetector without Semantics wrapper |
| React Native (JS/TSX) | Missing accessibilityLabel, accessibilityRole, nested touchables |

### Desktop Apps (static source analysis)
| Framework | What's checked statically |
|-----------|--------------------------|
| Electron | Same as web — full WCAG checklist applies |
| WPF / XAML | AutomationProperties.Name, HelpText, LabeledBy |
| PyQt / PySide | setAccessibleName(), setAccessibleDescription(), setBuddy() |
| wxWidgets / wxPython | SetName(), SetHelpText(), wxAccessible subclass |
| GTK (Python) | AT-SPI2 / AtkObject properties |

> Static analysis covers ~40–60% of accessibility issues for native apps. The rest requires running the app with a screen reader (TalkBack, VoiceOver, NVDA, Orca). This is always stated clearly in the report.

## Report Format

Every audit produces:

- Executive summary — score, grade, issue counts
- Critical issues — must fix (each with element, WCAG criterion, specific fix)
- Warnings — should fix
- Informational notes
- Passed checks
- GOST / Mincifry compliance table (for Russian gov sites)
- What cannot be checked statically (for mobile/desktop)
- Recommended tools for deeper testing

### Scoring

| Severity | Deduction |
|----------|-----------|
| Critical | −10 pts |
| Warning | −5 pts |
| Info | −1 pt |

Grades: A (90–100), B (80–89), C (70–79), D (60–69), F (0–59)

## Standards Covered

- **WCAG 2.1 Level A and AA** — international web accessibility standard
- **WCAG 2.2** — new criteria noted where relevant
- **GOST R 52872-2019** — Russian national standard (based on WCAG 2.1)
- **Mincifry order (Приказ Минцифры России)** — mandatory for Russian government websites

## How to Use

Just tell the AI agent what to audit:

```
Check accessibility of https://example.com
Audit the GitHub repo https://github.com/user/myapp for accessibility
Check accessibility of /home/user/projects/myapp
Проверь доступность https://gosuslugi.ru
Аудит доступности github.com/user/android-app
```

The agent auto-detects the target type and applies the right checklist.

## Skill Files

```
~/.hermes/skills/accessibility/accessibility-auditor/
├── SKILL.md                        # Main workflow and audit instructions
├── plan.md                         # Development plan
└── references/
    ├── README.md                   # This index
    ├── wcag-criteria.md            # WCAG 2.1 full criteria reference
    ├── gost-checklist.md           # GOST R 52872-2019 + Mincifry checklist (RU)
    ├── mobile-checklist.md         # Android / iOS / Flutter / React Native
    ├── desktop-checklist.md        # Electron / WPF / PyQt / wxWidgets / GTK
    └── tools.md                    # Testing tools by platform
```

## Limitations

- No headless browser execution — HTML is fetched and analyzed statically
- Color contrast requires visual rendering (flagged but not calculated precisely)
- Dynamic JavaScript-heavy sites may require browser snapshot mode
- Native mobile/desktop apps: ~40–60% issue coverage without running the app
- PyQt/wxWidgets: fewest available static tools — imperative code is harder to analyze

## Related Project

This skill was developed alongside the [Accessibility Auditor](https://github.com/web3blind/accessibility-auditor) — a production web service and Telegram bot that audits websites via WCAG 2.1 and supports pay-per-use via the x402 protocol.

The skill is independent — it does not call the service's API. It works entirely through AI analysis guided by these checklists.
