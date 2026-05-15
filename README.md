# Accessibility Auditor Skill

A portable AI skill for comprehensive accessibility auditing of websites, GitHub repositories, local project folders, and mobile/desktop app source code.

Built by a blind developer. Based on WCAG 2.1, WCAG 2.2 notes, GOST R 52872-2019, and the Russian Mincifry accessibility order.

## What It Does

The skill guides an AI agent through a structured accessibility audit workflow. You give it a target - a URL, a GitHub repo, or a local path - and the agent:

1. Gathers the best available evidence from the current environment
2. Applies the appropriate checklist for the target platform
3. Reports issues by severity with specific fix recommendations
4. Maps findings to WCAG 2.1 / GOST R 52872-2019 criteria
5. Scores the result (0-100) and assigns a letter grade
6. Clearly states coverage gaps and what still needs runtime/manual verification

## Portability Model

This skill is meant to work across different agent runtimes such as Hermes, OpenClaw, Codex, Claude Code, and similar systems.

To stay portable, it separates:
- **portable core** - workflow, references, report format, scoring, coverage rules
- **runtime capabilities** - fetch page content, render a page, read files, search files, run local audit tools

The skill should describe capabilities and outputs, not hard-code vendor-specific tool names.

## Supported Targets

| Target | How to provide | Analysis quality |
|--------|---------------|-----------------|
| Website | Any public URL | Static-first HTML/CSS/ARIA analysis, optionally richer with browser/audit tooling |
| GitHub repo | GitHub URL | Source code analysis for web, mobile, desktop |
| Local folder | Absolute or relative path | Same as GitHub - reads files directly |

## Supported Platforms

### Web / Electron
- WCAG 2.1 AA checklist
- WCAG 2.2 notes where relevant
- GOST R 52872-2019 / Mincifry framing when applicable
- HTML structure, ARIA, keyboard navigation, forms, responsive and contrast heuristics

### Mobile Apps (static source analysis)
| Framework | What's checked statically |
|-----------|--------------------------|
| Android (XML + Kotlin/Java) | Missing contentDescription, labelFor, importantForAccessibility misuse |
| iOS (Swift / SwiftUI) | Missing accessibilityLabel, roles/traits issues, incorrect accessibilityHidden |
| Flutter (Dart) | Images without semanticLabel, GestureDetector without Semantics wrapper |
| React Native (JS/TSX) | Missing accessibilityLabel, accessibilityRole, nested touchables |

### Desktop Apps (static source analysis)
| Framework | What's checked statically |
|-----------|--------------------------|
| Electron | Same as web - WCAG-oriented static checks apply |
| WPF / XAML | AutomationProperties.Name, HelpText, LabeledBy |
| PyQt / PySide | setAccessibleName(), setAccessibleDescription(), setBuddy() |
| wxWidgets / wxPython | SetName(), SetHelpText(), wxAccessible subclass |
| GTK (Python) | AT-SPI2 / AtkObject-related patterns where visible from source |

> Static analysis covers only part of accessibility for native apps. The remainder requires runtime/manual testing with screen readers and platform-specific inspectors.

## Audit Depth Levels

### Level A - zero-setup baseline
Works with the environment as-is:
- URL or source inspection
- static findings
- useful report right away

### Level B - richer audit
If the environment already has more capability or tools:
- browser rendering
- better evidence for dialogs, menus, forms, dynamic UI
- richer source coverage

### Level C - advanced follow-up
If the environment allows deeper tooling or optional installs:
- approved audit CLI tools
- framework/platform-native linting or testing
- broader coverage across more pages/modules

## Approved Optional Tooling

If deeper checks are needed, the skill should prefer existing tools first.
If installation is allowed, it should extend only from an approved allowlist.

### Web / browser-based
- `@axe-core/cli`
- `pa11y`
- `lighthouse`
- `playwright`

### Source inspection helpers
- `ripgrep` / `rg`
- standard framework linters already normal for the target stack

### Platform-specific
See `references/tools.md` for the recommended tools by platform.

## Skill Files

```text
accessibility-auditor-skill/
├── README.md
├── SKILL.md
├── PORTABILITY.md
├── plan.md
└── references/
    ├── README.md
    ├── additional-checks.md
    ├── desktop-checklist.md
    ├── gost-checklist.md
    ├── international-standards.md
    ├── mobile-checklist.md
    ├── tools.md
    └── wcag-criteria.md
```

## Install / Extension Policy

The skill should follow this order:
1. use the current agent environment first
2. deliver the best partial audit it can immediately
3. if richer checks are needed, extend only through the approved allowlist from `SKILL.md` and `references/tools.md`
4. never install arbitrary tooling outside that approved set

This keeps the skill low-friction without turning it into an uncontrolled installer.

## Limitations

- Static analysis alone cannot fully prove accessibility
- Color contrast may need rendering or dedicated tools
- JavaScript-heavy sites may need browser rendering for deeper confidence
- Native mobile/desktop apps require runtime/manual testing for full coverage
- Large repositories should be audited by representative flows/components first

## Related Project

This skill was developed alongside the [Accessibility Auditor](https://github.com/web3blind/accessibility-auditor) - a production service and Telegram bot for website accessibility audits.

This skill is independent. It is meant to work through AI-guided analysis plus optional approved tooling, not through the service API.
