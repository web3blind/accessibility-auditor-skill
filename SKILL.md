---
name: accessibility-auditor
description: Comprehensive accessibility audit for websites, repositories, local projects, and app source code. Uses WCAG 2.1 / 2.2 references, GOST R 52872-2019, and platform-specific checklists with graceful degradation across different agent runtimes.
triggers:
  - audit accessibility
  - check accessibility
  - accessibility audit
  - accessibility check
  - analyse accessibility
  - WCAG audit
  - audit a11y
  - аудит доступности
  - проверить доступность
  - проверить сайт на доступность
  - ГОСТ доступность
---

# Accessibility Auditor Skill

Performs structured accessibility audits on:
- **Websites** — public URLs
- **GitHub repositories** — source code analysis
- **Local project folders** — source code analysis
- **Mobile apps** — Android, iOS, Flutter, React Native source (static-first)
- **Desktop apps** — Electron, WPF/XAML, PyQt/PySide, wxWidgets, GTK source (static-first)

The skill is designed to be **portable across agent runtimes**.
It should describe **what to inspect and what to report**, not depend on one vendor's tool names.

## Core Operating Rules

1. **Use the best capabilities already available in the current environment first.**
2. **Prefer useful partial results over hard failure.**
3. **If deeper checks need more tooling, either:**
   - use approved tools already present in the environment, or
   - if installs are allowed in the current runtime, extend only from the approved audit-tool allowlist below, or
   - otherwise recommend the exact tools for a deeper follow-up pass.
4. **Do not install arbitrary tools outside the approved allowlist.**
5. **Always report what was checked, what was not checked, and why.**
6. **For native mobile/desktop apps, be explicit that static analysis is partial.**

## Capability Model

When this skill says to inspect something, the runtime may satisfy that with different tools. Think in capabilities:

- **Fetch page content** — retrieve the content of a public page or document
- **Render in browser** — load a JS-heavy page or interactive flow when static fetch is insufficient
- **Read source files** — open relevant code and markup files directly
- **Search source files** — find files by extension and locate relevant patterns
- **Run local audit tools** — only if they are already available or approved for optional installation
- **Report evidence** — quote files, elements, selectors, code patterns, and coverage limits clearly

Do not require a specific tool name when a capability is enough.

## Approved Optional Audit-Tool Allowlist

Use existing environment capabilities first.
If richer checks are needed and the runtime allows extension, prefer the smallest approved tool that unlocks the missing check.

### Web / browser-based
- `@axe-core/cli`
- `pa11y`
- `lighthouse`
- `playwright`

### Source inspection helpers
- `ripgrep` / `rg`
- framework linters already standard for the target stack

### Android
- Android Lint
- Accessibility Test Framework (ATF)

### iOS
- Xcode Accessibility Inspector
- XCTest accessibility audit support
- SwiftLint with accessibility-focused custom rules

### Flutter
- `accessibility_lints`
- built-in Flutter semantics testing

### React Native
- `eslint-plugin-react-native-a11y`
- `eslint-plugin-jsx-a11y`

### Desktop
- `axe-windows`
- Accessibility Insights for Windows
- `accerciser`
- `pyatspi`
- `dogtail`

Policy:
- do not install anything outside this list from inside the skill
- prefer already-installed tools over new installs
- if installs are disallowed or inappropriate for the environment, continue with a partial audit and recommend the relevant tools explicitly

## Quick Start

The user provides one of:
- a URL: `https://example.com`
- a GitHub repo: `https://github.com/user/repo`
- a local path: `/home/user/myapp` or `./myapp`
- multiple targets at once

Then follow the workflow below.

---

## Step 1: Detect Input Type and Gather Data

### Website (URL)
1. Fetch the page content.
2. If the site is JS-heavy or critical UI is missing from static content, render it in a browser-capable environment.
3. Inspect a few important secondary pages when relevant: `/about`, `/contact`, key forms, pricing, sign-in, checkout, docs, or any user-critical flow.
4. If automated audit tools are already available, use them as supporting evidence — not as the only source of truth.

### GitHub Repository
1. Inspect the repo entry point (README, docs, package files, platform folders).
2. Fetch or read relevant source files:
   - web: HTML, CSS, JS/JSX/TSX
   - Android: XML, Kotlin, Java
   - iOS: Swift, SwiftUI, ObjC
   - Flutter: Dart
   - React Native: JS/TSX
   - desktop: Electron HTML/JS, XAML, Python GUI files, GTK-related files
3. Check whether the repo already mentions accessibility, testing, semantics, ARIA, screen reader support, or compliance.
4. If the repo is large, prioritize entry points and key user flows.

### Local Folder
1. Search for relevant files by extension and framework structure.
2. Read the most important source files directly.
3. Prioritize entry points, reusable components, forms, navigation, dialogs, and key workflows.
4. Check package/config/build files for accessibility-related dependencies or test tooling.

---

## Step 2: Identify Platform and Load the Right References

Determine what is being audited:
- **Web** → HTML/CSS/JS, check WCAG 2.1 / 2.2 + Russian compliance when relevant
- **Android** → layout XML + Kotlin/Java, use mobile checklist
- **iOS** → Swift/SwiftUI/ObjC, use mobile checklist
- **Flutter** → Dart widget files, use mobile checklist
- **React Native** → JS/TSX files, use mobile checklist
- **Electron** → web checklist + desktop caveats
- **PyQt/PySide / wxWidgets / GTK / WPF/XAML** → desktop checklist

Load the appropriate reference files:
- `references/wcag-criteria.md` — web/WCAG criterion detail
- `references/additional-checks.md` — extra web/product checks when applicable
- `references/mobile-checklist.md` — Android/iOS/Flutter/React Native
- `references/desktop-checklist.md` — desktop app static analysis
- `references/gost-checklist.md` — Russian government/compliance framing
- `references/tools.md` — deeper verification tooling

Use `references/international-standards.md` only if needed as supplemental context.

---

## Step 3: Run the Audit

### Coverage Strategy
Choose the best level the environment supports:

#### Level A — zero-setup baseline
Use available page/source inspection only.
Deliver a useful static audit immediately.

#### Level B — richer audit
If browser rendering or local audit tools are available, add:
- rendered DOM inspection
- richer evidence for interactive flows
- stronger confidence on forms, dialogs, menus, tabs, and stateful UI

#### Level C — advanced follow-up
If the environment supports deeper tooling or the user allows it, add:
- approved audit CLI tools
- platform-native lint/test tools
- broader multi-page or multi-module coverage

Always keep the report honest about which level was reached.

### For Websites — check ALL of the following when possible

#### A. Perceivable
- [ ] All images have descriptive `alt` text (not empty, not "image", not filename)
- [ ] Decorative images have `alt=""` and `role="presentation"` where appropriate
- [ ] Videos have captions (`<track kind="captions">`) or equivalent support
- [ ] Audio has transcripts
- [ ] Color is not the only way to convey information
- [ ] Text contrast appears sufficient; if exact calculation is unavailable, say so
- [ ] Text can be resized to 200% without loss of content or usability
- [ ] Page content reflows at narrow/mobile widths
- [ ] No content flashes more than 3 times per second

#### B. Operable
- [ ] All functionality appears keyboard-accessible
- [ ] No keyboard traps are evident
- [ ] Visible focus indicator exists and is clear
- [ ] Skip navigation link exists where relevant
- [ ] Page has a meaningful `<title>` tag
- [ ] Focus order is logical
- [ ] Time limits are absent or adjustable
- [ ] Moving content can be paused/stopped/hidden
- [ ] No content auto-navigates without user control

#### C. Understandable
- [ ] `<html lang="...">` is set correctly
- [ ] Navigation and labeling are consistent
- [ ] Forms have descriptive labels
- [ ] Error messages explain what is wrong and how to fix it
- [ ] Instructions do not rely only on color, shape, or screen position
- [ ] Unclear jargon or abbreviations are explained where needed
- [ ] Input purpose is programmatically determinable where applicable

#### D. Robust
- [ ] HTML structure appears valid and semantically coherent
- [ ] ARIA roles, states, and properties are used correctly
- [ ] Accessible names exist where needed
- [ ] `aria-hidden="true"` is not applied to interactive/focusable elements
- [ ] Buttons, links, and form controls have usable names
- [ ] Form inputs have associated labels
- [ ] State attributes such as `aria-expanded`, `aria-selected`, `aria-checked` match behavior

#### E. Structure & Landmarks
- [ ] Exactly one `<h1>` per page when appropriate
- [ ] Heading hierarchy is logical
- [ ] Landmarks such as `<main>`, `<nav>`, `<header>`, `<footer>`, `<aside>` are used well
- [ ] Links have descriptive text
- [ ] Tables use proper headers/captions where needed
- [ ] Lists are semantically marked up

#### F. Special Elements
- [ ] iframes have descriptive `title`
- [ ] PDFs have an accessible alternative or a note about accessibility
- [ ] CAPTCHA has an accessible alternative
- [ ] Modals/dialogs manage focus correctly
- [ ] Custom widgets have appropriate semantics and state handling

### For Mobile App Source Code

Use `references/mobile-checklist.md`.

Static audit examples:
- Android: missing `contentDescription`, `labelFor`, misuse of `importantForAccessibility`
- iOS: missing `accessibilityLabel`, incorrect accessibility hiding, weak traits/roles
- Flutter: missing `Semantics`, unlabeled images, gesture-only wrappers
- React Native: missing `accessibilityLabel`, `accessibilityRole`, nested touchables, unclear accessible names

Always state that static analysis does **not** fully prove:
- color contrast
- touch target size
- focus traversal order
- spoken announcements
- real custom widget behavior with screen readers

### For Desktop App Source Code

Use `references/desktop-checklist.md`.

Examples:
- Electron: treat as web plus app-shell interaction caveats
- PyQt/PySide: inspect `setAccessibleName()`, `setAccessibleDescription()`, buddies/labels
- wxWidgets: inspect naming/help text/accessibility hooks
- WPF/XAML: inspect `AutomationProperties.*`
- GTK: inspect AT-SPI/Atk exposure where visible from source

---

## Step 4: Produce the Report

Use this structure:

```md
## Accessibility Audit Report

**Target:** [URL / repo / path]
**Date:** [date]
**Platform:** [web / Android / iOS / Flutter / React Native / Electron / etc.]
**Audit depth:** [Level A / B / C]
**Standards checked:** [WCAG 2.1 AA / WCAG 2.2 notes / GOST R 52872-2019 / etc.]

---

### Executive Summary

**Score:** XX/100
**Grade:** [A/B/C/D/F]
**Critical issues:** N
**Warnings:** N
**Informational:** N

Overall assessment: [1-2 sentence summary]

---

### Coverage

- What was checked
- What was not checked
- Which capabilities or tools were available
- Which checks remain lower-confidence because of environment limits

---

### Critical Issues (must fix)

**[Category]**
- Issue: [description]
  Evidence: [element / selector / file / code pattern]
  WCAG criterion: [e.g., 1.1.1 Non-text Content]
  Fix: [specific recommendation]

---

### Warnings (should fix)

[same format]

---

### Informational (good to know)

[same format]

---

### Passed Checks

[List what was checked and found acceptable]

---

### Compliance Mapping

[Map findings to GOST / Mincifry when relevant, otherwise keep to WCAG mapping]

---

### What Requires Runtime or Manual Testing

[List what static analysis could not prove]

---

### Recommended Deeper Verification

[List tools or manual checks from the approved references/tools set]

---

### Next Steps

1. [Highest-priority fix]
2. ...
```

---

## Scoring Formula

Calculate score as: `max(0, 100 - deductions)`

| Severity  | Deduction per issue |
|-----------|---------------------|
| Critical  | 10 points           |
| Warning   | 5 points            |
| Info      | 1 point             |

Grade scale:
- 90-100: A (Excellent)
- 80-89: B (Good)
- 70-79: C (Fair)
- 60-69: D (Poor)
- 0-59: F (Fail)

---

## Important Notes

### Graceful Degradation
If the environment cannot support browser rendering, local source search, or richer audit tooling:
- continue with the best partial audit possible
- explicitly state the missing coverage
- recommend the smallest relevant next-step tools from `references/tools.md`

### Honesty for Native Apps
Static analysis often finds roughly 40-60% of accessibility issues in native apps.
The following usually require running the real app with assistive technology:
- real screen reader announcements
- color contrast in rendered UI
- touch target sizes
- focus traversal order
- dynamic announcements
- behavior of custom components

Always say this clearly.

### Russian Standards
For Russian public-sector or compliance-sensitive targets, map findings against:
1. GOST R 52872-2019
2. relevant Mincifry requirements from `references/gost-checklist.md`

### Large Targets
If the target is large, prioritize:
1. main page / entry points
2. key user flows
3. forms and interactive elements
4. navigation structure
5. representative templates or reusable components

State what was and was not covered.
