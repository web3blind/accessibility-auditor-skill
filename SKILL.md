---
name: accessibility-auditor
description: Comprehensive accessibility audit for websites (WCAG 2.1, GOST R 52872-2019), GitHub repos, and local projects. Also covers mobile (Android/iOS/Flutter/React Native) and desktop (Electron/PyQt) source code static analysis.
triggers:
  - audit accessibility
  - check accessibility
  - аудит доступности
  - проверить доступность
  - analyse accessibility
  - accessibility audit
  - WCAG audit
  - ГОСТ доступность
  - проверь доступность сайта
  - accessibility check
  - проверить сайт на доступность
---

# Accessibility Auditor Skill

Performs comprehensive accessibility audits on:
- **Websites** — via URL (any public site)
- **GitHub repositories** — source code analysis
- **Local project folders** — source code analysis
- **Mobile apps** — Android/iOS/Flutter/React Native source (static)
- **Desktop apps** — Electron/PyQt/wxWidgets source (static)

## Quick Start

The user provides one of:
- A URL: `https://example.com`
- A GitHub repo: `https://github.com/user/repo`
- A local path: `/home/user/myapp` or `./myapp`
- Multiple targets at once

Then follow the workflow below.

---

## Step 1: Detect Input Type and Gather Data

### Website (URL)
1. Use `web_extract([url])` to get page content
2. If site requires JavaScript, use `browser_navigate` + `browser_snapshot(full=True)`
3. Also check secondary pages: /about, /contact, any linked pages
4. Note: you cannot "run" accessibility scanners — analyze the HTML/CSS yourself

### GitHub Repository
1. Use `web_extract(["https://github.com/user/repo"])` for README and main page
2. Fetch relevant source files:
   - For web projects: look for HTML, CSS, JS/JSX/TSX files
   - For mobile: look for layout XML (Android), Swift/SwiftUI, Dart, JS (React Native)
   - For desktop: look for PyQt, wxWidgets, Electron HTML
3. Use `web_extract` on raw file URLs:
   `https://raw.githubusercontent.com/user/repo/main/path/to/file`
4. Check if there's an existing accessibility statement or docs

### Local Folder
1. Use `search_files(pattern="*.html", path="/path")` to find relevant files
2. Use `read_file` to read source files
3. Prioritize: HTML/JSX/TSX, layout XML (Android), Swift/Dart files
4. Check package.json / pubspec.yaml / build.gradle for accessibility deps

---

## Step 2: Identify Platform and Framework

Determine what you're auditing:
- **Web** → HTML/CSS/JS, check WCAG 2.1 + GOST checklist
- **Android** → layout XML + Kotlin/Java, check mobile checklist
- **iOS** → Swift/SwiftUI/ObjC, check mobile checklist
- **Flutter** → Dart widget files, check mobile checklist
- **React Native** → JS/TSX files, check mobile checklist
- **Electron** → HTML/CSS/JS (same as web + Electron specifics)
- **PyQt/wxWidgets** → Python files, limited static analysis possible
- **WPF/XAML** → XAML files (similar to Android XML, high viability)

Load the appropriate reference files for this platform:
- `references/web-checklist.md` for websites and Electron
- `references/mobile-checklist.md` for Android/iOS/Flutter/React Native
- `references/desktop-checklist.md` for native desktop (PyQt, wxWidgets, WPF)
- `references/gost-checklist.md` for Russian government sites
- `references/wcag-criteria.md` for WCAG 2.1 criterion-level detail
- `references/tools.md` for tooling recommendations

---

## Step 3: Run the Audit

### For Websites — check ALL of the following:

#### A. Perceivable
- [ ] All images have descriptive `alt` text (not empty, not "image", not filename) — WCAG 1.1.1
- [ ] Decorative images have `alt=""` and `role="presentation"` — WCAG 1.1.1
- [ ] Videos have captions — look for `<track kind="captions">` — WCAG 1.2.2
- [ ] Audio-only content has text transcript — check for transcript link near the player — WCAG 1.2.1
- [ ] Color is NOT the only way to convey information (check error states, required fields, graphs) — WCAG 1.4.1
- [ ] Text contrast ratio ≥ 4.5:1 (normal text), ≥ 3:1 (large text ≥18pt or 14pt bold) — WCAG 1.4.3 — NOTE: exact ratio requires color picker tool; flag suspicious low-contrast color pairs in CSS
- [ ] Non-text UI components (icons, borders, focus outlines, charts) have ≥ 3:1 contrast against adjacent colors — WCAG 1.4.11
- [ ] Orientation is not locked — check for CSS `orientation: landscape/portrait` locks or JS `screen.orientation.lock()` — WCAG 1.3.4
- [ ] `[MANUAL] Text can be resized to 200% without horizontal scrolling or loss of content` — WCAG 1.4.4 — cannot verify statically; flag `overflow: hidden` on text containers as risk
- [ ] `[MANUAL] Page content reflows at 320px width` — WCAG 1.4.10 — cannot verify without rendering; check for `min-width` values > 320px in CSS as risk
- [ ] `[MANUAL] No content flashes more than 3 times per second` — WCAG 2.3.1 — requires playback; note presence of `<video autoplay>`, animated GIFs, or rapid CSS animations as risk

#### B. Operable
- [ ] ALL functionality is keyboard-accessible (Tab, Enter, Space, Arrow keys) — WCAG 2.1.1
- [ ] No keyboard traps (user can always Tab away) — WCAG 2.1.2
- [ ] Visible focus indicator exists — check CSS does NOT have `outline: none` / `outline: 0` without a replacement — WCAG 2.4.7
- [ ] Focus indicator meets WCAG 2.2: ≥2px outline, ≥3:1 contrast vs adjacent color — check `:focus` CSS — WCAG 2.4.13
- [ ] Focused element not hidden behind sticky header/footer — check `position: sticky` / `position: fixed` elements — WCAG 2.4.11
- [ ] Skip navigation link exists ("Skip to main content") — WCAG 2.4.1
- [ ] Page has a meaningful `<title>` tag (not "Home", not empty) — WCAG 2.4.2
- [ ] `[MANUAL] Focus order is logical` — WCAG 2.4.3 — requires runtime; check for suspicious `tabindex` values > 0 as a risk indicator
- [ ] `[MANUAL] No time limits, or user can extend/disable them` — WCAG 2.2.1 — requires runtime; check for session timeout JS as risk
- [ ] `[MANUAL] Moving/auto-updating content can be paused/stopped/hidden` — WCAG 2.2.2 — requires runtime; flag `<video autoplay loop>` and `setInterval` animations as risk
- [ ] Drag-and-drop interactions have single-pointer (click/button) alternative — check `dragstart`/`drop` handlers — WCAG 2.5.7
- [ ] Click targets are ≥24×24 CSS px (small icon buttons, close buttons, pagination) — WCAG 2.5.8

#### C. Understandable
- [ ] `<html lang="...">` attribute is set correctly — WCAG 3.1.1
- [ ] Pages are consistent in navigation and labeling — WCAG 3.2.3 / 3.2.4
- [ ] Help links/contacts appear in consistent location across pages — WCAG 3.2.6
- [ ] Forms have descriptive labels for all inputs — WCAG 3.3.2
- [ ] Error messages are specific and describe how to fix the error — WCAG 3.3.1 / 3.3.3
- [ ] Instructions don't rely solely on sensory characteristics (color, shape, location) — WCAG 1.3.3
- [ ] Personal data fields use correct `autocomplete` attributes: `name`, `email`, `tel`, `street-address`, `postal-code`, `bday`, etc. — WCAG 1.3.5
- [ ] Forms don't ask for information already provided in the same session — WCAG 3.3.7
- [ ] CAPTCHA has an accessible alternative (audio, logic puzzle, or no CAPTCHA) — WCAG 3.3.8
- [ ] Abbreviations and jargon are explained (first use or via `<abbr>` tag)

#### D. Robust
- [ ] Valid HTML (no broken tags, proper nesting, no duplicate `id`) — WCAG 4.1.1
- [ ] ARIA roles, states, properties are used correctly — WCAG 4.1.2
- [ ] `aria-label` / `aria-labelledby` / `aria-describedby` are present where needed — WCAG 4.1.2
- [ ] No `aria-hidden="true"` on interactive/focusable elements — WCAG 4.1.2
- [ ] Buttons and links have accessible names — WCAG 4.1.2
- [ ] Form inputs have associated `<label>` (via `for` attribute or wrapping) — WCAG 1.3.1 / 4.1.2
- [ ] `role`, `aria-expanded`, `aria-selected`, `aria-checked` match actual state — WCAG 4.1.2
- [ ] Status messages (success, error, loading) use `role="status"` or `aria-live` so they are announced without moving focus — WCAG 4.1.3

#### E. Structure & Landmarks
- [ ] Exactly one `<h1>` per page
- [ ] Heading hierarchy is correct (h1→h2→h3, no skipping levels)
- [ ] ARIA landmarks: `<main>`, `<nav>`, `<header>`, `<footer>`, `<aside>` used
- [ ] Links have descriptive text (not "click here", "read more", "link")
- [ ] Tables use `<th>` with `scope` attribute, have `<caption>` if needed
- [ ] Lists use `<ul>`, `<ol>`, `<dl>` semantically

#### F. Special Elements
- [ ] iframes have descriptive `title` attribute — WCAG 4.1.2
- [ ] PDF links include file type and size in link text (e.g. "Annual Report (PDF, 2MB)") — WCAG 2.4.4
- [ ] PDFs on the site: flag untagged/scanned PDFs — tagged PDF required for screen reader access (PDF/UA / WCAG 1.1.1)
- [ ] PDF document language is set, tables have proper TR/TH/TD tag structure, images have Alt entries — check PDF source if available — WCAG 1.3.1 / 3.1.1
- [ ] `[MANUAL] Modals/dialogs trap focus and return focus on close` — requires runtime; check for `aria-modal="true"` and `role="dialog"` as static indicators
- [ ] Custom widgets (dropdowns, sliders, tabs, accordions) have correct ARIA: `role`, `aria-expanded`, `aria-controls`, `aria-selected` — WCAG 4.1.2
- [ ] Carousels and auto-rotating banners have pause controls — WCAG 2.2.2

### For Mobile App Source Code:

Load `references/mobile-checklist.md` and apply per-platform checks.

Key things to detect statically:
- **Android XML layouts**: Missing `android:contentDescription` on ImageView, ImageButton
- **Android Kotlin/Java**: Missing `setContentDescription()` calls, misuse of `importantForAccessibility`
- **iOS Swift/SwiftUI**: Missing `.accessibilityLabel()`, incorrect `.accessibilityHidden(true)`
- **Flutter**: Images without `semanticLabel` or `Semantics` wrapper, `GestureDetector` without Semantics
- **React Native**: `<Image>` missing `accessibilityLabel`, `<TouchableOpacity>` without label

Hard to check statically (note in report):
- Color contrast (requires rendering)
- Touch target sizes (requires layout computation)
- Focus traversal order (requires runtime)
- Screen reader announcement accuracy (requires device testing)

### For Desktop App Source Code:

Load `references/desktop-checklist.md`.

- **Electron**: Treat as web — check HTML/CSS/JS with web checklist
- **PyQt**: Look for `setAccessibleName()`, `setAccessibleDescription()` calls
- **wxWidgets**: Look for `SetName()`, `SetHelpText()` calls
- **WPF/XAML**: Check `AutomationProperties.Name`, `AutomationProperties.HelpText`

---

## Step 4: Produce the Report

Structure your report as follows:

```
## Accessibility Audit Report

**Target:** [URL / repo / path]
**Date:** [date]
**Platform:** [web / Android / iOS / Flutter / React Native / Electron / etc.]
**Standards checked:** [WCAG 2.1 AA / GOST R 52872-2019 / Mincifry Checklist]

---

### Executive Summary

**Score:** XX/100
**Grade:** [A/B/C/D/F]
**Critical issues:** N
**Warnings:** N
**Informational:** N

Overall assessment: [1-2 sentence summary]

---

### Critical Issues (must fix)

**[Category]**
- Issue: [description]
  Element: [tag/selector/code snippet if found]
  WCAG criterion: [e.g., 1.1.1 Non-text Content]
  Fix: [specific recommendation]

[repeat for each critical issue]

---

### Warnings (should fix)

[same format as above]

---

### Informational (good to know)

[same format as above]

---

### Passed Checks

[List what was checked and found to be OK]

---

### GOST / Mincifry Compliance (if applicable)

[Map findings to the official Russian checklist items from references/gost-checklist.md]

---

### What Cannot Be Checked Statically

[For mobile/desktop: list what requires device/runtime testing]

---

### Recommended Tools for Deeper Testing

[From references/tools.md — platform-appropriate tools]

---

### Next Steps

1. [Prioritized action items]
2. ...
```

---

## Scoring Formula

Calculate score as: `max(0, 100 - deductions)`

| Severity  | Deduction per issue |
|-----------|-------------------|
| Critical  | 10 points         |
| Warning   | 5 points          |
| Info      | 1 point           |

Grade scale:
- 90-100: A (Excellent)
- 80-89: B (Good)
- 70-79: C (Fair)
- 60-69: D (Poor)
- 0-59: F (Fail)

---

## Important Notes

### On Mobile/Desktop Apps — Honesty is Required
Static source code analysis can find ~40-60% of accessibility issues.
The following ALWAYS require running the actual app + screen reader:
- Actual screen reader behavior
- Color contrast (needs rendering)
- Touch target sizes
- Focus traversal order
- Dynamic content announcements
- Custom component behavior

Always state this clearly in the report.

### On Russian Standards
Russian government sites are governed by:
1. GOST R 52872-2019 (based on WCAG 2.1)
2. Mincifry order (Приказ Минцифры) — see `references/gost-checklist.md`

These mostly map to WCAG 2.1 AA requirements with some specific additions.

### On Completeness
If the target is large (many pages/files), focus on:
1. Main page / entry points
2. Key user flows (login, main functionality)
3. Any forms or interactive elements
4. Navigation structure

State what was and wasn't checked.
