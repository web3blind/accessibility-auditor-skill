# Additional Checks — Beyond WCAG 2.1 AA

Practical checks that complement the main WCAG checklist.
These are detectable in source code or HTML — no organisational/legal content.

---

## WCAG 2.2 — New Criteria (not in WCAG 2.1)

Check these in addition to WCAG 2.1 AA:

| Criterion | What to Check in Code/CSS |
|-----------|--------------------------|
| 2.4.11 Focus Not Obscured | Focused element not entirely hidden by sticky headers/footers. Check: `position: sticky` or `position: fixed` elements that could overlap focused content. |
| 2.4.13 Focus Appearance | Focus indicator meets size (≥2px outline) and contrast (≥3:1) requirements. Check CSS `outline`, `box-shadow` on `:focus` — `outline: none` without replacement is a failure. |
| 2.5.7 Dragging Movements | Drag-and-drop interactions have single-pointer alternatives. Check: `dragstart`/`drop` event handlers — is there a click/button alternative? |
| 2.5.8 Target Size (Minimum) | Click targets ≥24×24 CSS px (except inline text links). Check: small icon buttons, close buttons, pagination links. |
| 3.2.6 Consistent Help | Help links/contacts appear in consistent location across pages. |
| 3.3.7 Redundant Entry | Forms don't ask for info already provided in the same session. |
| 3.3.8 Accessible Authentication | CAPTCHA has accessible alternative (audio, logic puzzle). |

---

## PDF Documents — PDF/UA Checks (ISO 14289-1)

When a site links to or serves PDF files, check these in the HTML context:

**What to flag in HTML:**
- `<a href="*.pdf">` without indication of file type and size in link text
- PDF links where the linked document is known to be untagged/scanned image

**What to flag in the PDF itself (if accessible via source):**
- No tag structure (untagged PDF = invisible to screen readers)
- Images without `Alt` entry
- Tables without proper TR/TH/TD tag structure
- No `Lang` entry on document
- Security settings blocking AT access
- Scanned images without OCR text layer

**Quick check:** Download the PDF → open in Adobe Acrobat → Tools → Accessibility → Full Check. Or note in report: "PDF not verified — manual check required."

---

## Modals and Dialogs — Accessible Pattern Checks

Applies to any site with modal windows, dialog boxes, popups, drawers.

**Role and labelling (WCAG 4.1.2):**
```html
<!-- Required: role="dialog" or role="alertdialog" (for destructive/urgent) -->
<div role="dialog" aria-modal="true" aria-labelledby="modal-title">
  <h2 id="modal-title">Confirm deletion</h2>
  ...
</div>
```
- `role="dialog"` or `role="alertdialog"` must be present
- `aria-labelledby` pointing to visible heading, OR `aria-label` if no visible title
- `aria-modal="true"` signals to screen readers that background is inert

**Focus management (WCAG 2.1.2):**
```javascript
// On open — focus must move INTO the dialog:
modal.querySelector('button, [href], input, [tabindex]').focus();
// or set tabindex="-1" on container and call .focus() on it

// On close — focus must RETURN to the trigger element:
triggerButton.focus();
```
- Flag: modal opens without any `.focus()` call in JS near open logic
- Flag: no `tabindex="-1"` on modal container when it has no focusable children

**Keyboard interaction (WCAG 2.1.1):**
- Escape key closes the modal — check for `keydown` handler with `key === 'Escape'`
- Tab/Shift+Tab cycle only within the modal (focus trap) — check for focus trap logic
- Flag: no Escape key handler found near modal open/close logic

**Close button (WCAG 4.1.2):**
```html
<!-- Bad — icon-only, no name: -->
<button>×</button>

<!-- Good: -->
<button aria-label="Close dialog">×</button>
```

**Background inertness (WCAG 1.3.1):**
```html
<!-- When modal is open, background content must be hidden from AT: -->
<div id="main-content" aria-hidden="true">...</div>
<!-- Modern alternative: -->
<main inert>...</main>
```
- Flag: no `aria-hidden="true"` or `inert` on background when modal is open

**Quick static checklist:**
- `role="dialog"` or `role="alertdialog"` present ✓
- `aria-modal="true"` on container ✓
- `aria-labelledby` or `aria-label` with title ✓
- Close button has `aria-label` ✓
- `Escape` key handler in JS ✓
- `.focus()` called on open and close ✓
- Background gets `aria-hidden="true"` or `inert` on open ✓

---

## BBC Mobile Accessibility — Practical Code Checks

Applicable to any mobile app or responsive web:

- **Persistent visible labels:** Form fields must have a visible `<label>` — not just `placeholder`. Placeholder disappears on input and is not read by all screen readers.
  ```html
  <!-- Bad: -->
  <input type="email" placeholder="Email address">

  <!-- Good: -->
  <label for="email">Email address</label>
  <input type="email" id="email" placeholder="name@example.com">
  ```

- **Touch target size:** Interactive elements should be at least 44×44px (CSS). Check small icon buttons:
  ```css
  /* Flag if smaller than 44x44: */
  .icon-btn { width: 20px; height: 20px; } /* too small */

  /* Fix: */
  .icon-btn { min-width: 44px; min-height: 44px; }
  ```

- **Dynamic content announcements:** Content that updates without page reload (counters, status messages, live data) needs `aria-live`:
  ```html
  <div aria-live="polite" aria-atomic="true">
    <!-- dynamic content here -->
  </div>
  ```

---

## Apple HIG — Practical iOS/macOS Code Checks

- **Dynamic Type support:** All text must use scalable units. In SwiftUI: use `.font(.body)` not fixed pixel sizes. In UIKit: use `UIFontMetrics`.
  ```swift
  // Bad — fixed size:
  label.font = UIFont.systemFont(ofSize: 16)

  // Good — scales with user settings:
  label.font = UIFontMetrics.default.scaledFont(for: UIFont.systemFont(ofSize: 16))
  label.adjustsFontForContentSizeCategory = true
  ```

- **Reduce Motion:** Animations must check `UIAccessibility.isReduceMotionEnabled`:
  ```swift
  if !UIAccessibility.isReduceMotionEnabled {
      // run animation
  }
  // SwiftUI:
  @Environment(\.accessibilityReduceMotion) var reduceMotion
  ```

---

## Google Material / Android — Practical Code Checks

- **Minimum touch target 48×48dp:**
  ```xml
  <!-- Bad: -->
  <ImageButton android:layout_width="24dp" android:layout_height="24dp" />

  <!-- Good: use padding or minWidth/minHeight: -->
  <ImageButton
      android:layout_width="24dp"
      android:layout_height="24dp"
      android:minWidth="48dp"
      android:minHeight="48dp" />
  ```

- **Live regions for dynamic content:**
  ```xml
  <TextView
      android:accessibilityLiveRegion="polite"
      android:text="@{viewModel.statusMessage}" />
  ```
