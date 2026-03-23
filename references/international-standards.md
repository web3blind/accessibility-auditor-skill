# International Accessibility Standards Reference

## Quick Summary Table

| Standard | Region | Mandatory | WCAG Basis | Unique Features |
|----------|--------|-----------|-----------|----------------|
| Section 508 | USA federal | Yes | WCAG 2.0 AA | Hardware, kiosks, authoring tools, Functional Performance Criteria |
| ADA Title II (2024) | USA state/local | Yes | WCAG 2.1 AA | Tiered deadlines, archived content exceptions, safe harbor |
| EN 301 549 v3.2.1 | EU | Yes (public) | WCAG 2.1 AA | Hardware, software, documents, 14 chapters beyond web |
| European Accessibility Act (EAA) | EU | Yes (private from Jun 2025) | WCAG 2.1 AA via EN 301 549 | First EU law covering private sector digitally |
| Equality Act 2010 | UK | Yes (reasonable adjustment) | No specific version | Broad service provider obligation, no prescribed standard |
| Public Sector Bodies Regulations 2018 | UK public sector | Yes | WCAG 2.1 AA | Accessibility statement required |
| BS 8878:2010 | UK | No (voluntary) | WCAG 2.0 | Lifecycle process, not just technical criteria |
| AODA | Canada/Ontario | Yes | WCAG 2.0 AA | Multi-year plans, staff training, employment/transport standards |
| ACA | Canada/federal | Yes | WCAG 2.1 AA | Federal organisations, banks, telecoms |
| DDA 1992 | Australia | Yes (complaint-based) | WCAG 2.0/2.1 AA | No proactive regulator, complaint to AHRC |
| JIS X 8341-3:2016 | Japan | Yes (govt) | WCAG 2.0 AA | Japanese-specific conformance claim format |
| BITV 2.0 | Germany | Yes (federal/state govt) | WCAG 2.1 AA | Sign language video (DGS) + easy language (Leichte Sprache) REQUIRED |
| RGAA 4.1 | France | Yes (public + large private >250M€) | WCAG 2.1 AA | 106 criteria, fines up to €20k, accessibility declaration required |

---

## Web / ICT Standards — Detailed

### USA — Section 508 (Rehabilitation Act)

- **Full name:** Section 508 of the Rehabilitation Act of 1973 (revised 2017–18)
- **Applies to:** All U.S. federal agencies (development, procurement, maintenance of ICT)
- **Mandatory:** Yes
- **WCAG basis:** WCAG 2.0 Level AA
- **Unique beyond WCAG:**
  - Functional Performance Criteria (FPC) — usability for people with sensory, motor, and cognitive disabilities
  - Hardware: kiosks, ATMs, copiers, physical ICT devices
  - Authoring tool accessibility requirements
  - Support documentation and services accessibility
  - Telecommunications products (overlap with Section 255)
  - Closed functionality provisions (e.g., devices with no AT support)
  - Covers **procurement**, not just new development
- **URL:** https://www.section508.gov | https://www.access-board.gov/ict/

---

### USA — ADA Title II (2024 DOJ Rule)

- **Full name:** Americans with Disabilities Act of 1990, Title II — Final Rule (March 2024)
- **Applies to:** State and local government entities; Title III (courts only) for private businesses
- **Mandatory:** Yes
- **WCAG basis:** WCAG 2.1 Level AA
- **Unique beyond WCAG:**
  - Tiered compliance deadlines: large entities 2 years, small entities 3 years from publication
  - Exceptions: archived content, preexisting conventional documents, third-party content, individualized documents, password-protected documents
  - Safe harbor for content already meeting WCAG 2.1 AA
  - Title III for private businesses still court-interpreted (no federal regulation yet)
- **URL:** https://www.ada.gov/resources/2024-03-08-web-rule/

---

### EU — EN 301 549 v3.2.1

- **Full name:** EN 301 549 "Accessibility requirements for ICT products and services" (ETSI, 2021)
- **Applies to:** EU public sector (mandatory); private sector via EAA from June 2025
- **Mandatory:** Yes (for public sector)
- **WCAG basis:** WCAG 2.1 Level AA (Chapters 9 and 10)
- **Unique beyond WCAG — 14 chapters covering:**
  - Chapter 6: Two-way voice communication products
  - Chapter 7: Video/audio products
  - Chapter 8: Hardware — physical access, biometrics, operable parts
  - Chapter 9: Web content (= WCAG 2.1 AA)
  - Chapter 10: Non-web documents
  - Chapter 11: Non-web software applications
  - Chapter 12: Authoring tools
  - Chapter 13: ICT with relay and emergency service access
  - Closed functionality, support documentation, services
- **URL:** https://www.etsi.org/deliver/etsi_en/301500_302000/301549/03.02.01_60/en_301549v030201p.pdf

---

### EU — European Accessibility Act (EAA)

- **Full name:** EU Directive 2019/882 — European Accessibility Act
- **Applies to:** ALL EU private sector companies selling products/services in the EU — **from June 28, 2025**
- **Mandatory:** Yes (from June 2025)
- **WCAG basis:** WCAG 2.1 AA via EN 301 549
- **Unique features:**
  - First EU law extending mandatory accessibility to **private sector**
  - Covers: e-commerce, banking, passenger transport, e-books, audiovisual media, telecom, computers, smartphones, ATMs, ticketing machines, e-readers
  - Accessible packaging and instructions required
  - Micro-enterprises exempt (<10 employees, <2M€ turnover)
  - Proportionality / fundamental alteration exemption
  - Each EU member state must set enforcement and penalties
- **URL:** https://ec.europa.eu/social/main.jsp?catId=1202

---

### UK — Equality Act 2010 + Public Sector Regulations 2018

- **Equality Act:** General anti-discrimination law; all service providers must make "reasonable adjustments" for disabled users; no specific WCAG version mandated
- **Public Sector Bodies Accessibility Regulations 2018:** WCAG 2.1 AA mandatory for UK public sector websites and apps; accessibility statement required
- **URL:** https://www.legislation.gov.uk/ukpga/2010/15/contents | https://www.legislation.gov.uk/uksi/2018/952/made

---

### UK — BS 8878:2010

- **Full name:** BS 8878:2010 Web Accessibility — Code of Practice (BSI, voluntary)
- **Mandatory:** No
- **WCAG basis:** WCAG 2.0
- **Unique features:**
  - Covers entire product **lifecycle**, not just technical conformance
  - Requires accessibility **policy** and **user involvement** (especially disabled users)
  - Framework for deciding which AT, which WCAG level, documented decision trail
  - Procurement guidance
  - Process-based (organizational), not criteria-based
- **URL:** https://www.bsigroup.com/en-GB/standards/BS-8878/ (purchase required)

---

### Canada — AODA + ACA

- **AODA (Accessibility for Ontarians with Disabilities Act):** Ontario provincial law; WCAG 2.0 AA; applies to all Ontario employers
- **ACA (Accessible Canada Act, 2019):** Federal law; WCAG 2.1 AA; federal government, banks, telecoms, interprovincial transport
- **Unique beyond WCAG:**
  - Documented organizational accessibility policies
  - Multi-year accessibility plans (updated every 5 years), published online
  - Mandatory accessibility training for all staff and volunteers
  - Separate standards: customer service, employment, transportation, public spaces
  - Annual/biennial compliance reporting
  - Accessible formats on request
- **URL:** https://www.ontario.ca/laws/statute/05a11 | https://www.canada.ca/en/employment-social-development/programs/accessible-people-disabilities/act-summary.html

---

### Australia — DDA 1992

- **Full name:** Disability Discrimination Act 1992
- **Mandatory:** Yes as general anti-discrimination law; complaint-based only
- **WCAG basis:** WCAG 2.0 AA (AHRC advisory notes); WCAG 2.1 AA for government (Digital Service Standard)
- **Unique features:**
  - No specific web regulation — relies on complaint mechanism to AHRC
  - If conciliation fails → Federal Court
  - No proactive audit regulator for private sector websites
  - Government agencies additionally bound by Digital Service Standard (Criterion 9)
- **URL:** https://humanrights.gov.au/our-work/disability-rights/disability-discrimination

---

### Japan — JIS X 8341-3:2016

- **Full name:** JIS X 8341-3:2016 — Guidance on Web Accessibility (日本工業規格)
- **Mandatory:** Yes for government websites (Cabinet Office directive); voluntary for private sector
- **WCAG basis:** WCAG 2.0 Level AA
- **Unique features:**
  - Japanese-specific conformance claim format (standardized declaration procedure)
  - Guidance on Japanese language encoding, character sets, ruby text
  - Government websites must publish conformance claims in prescribed format
  - Maintained by JSA (Japanese Standards Association)
- **URL:** https://www.w3.org/WAI/policies/japan/ | https://accessible.jp/en/

---

### Germany — BITV 2.0

- **Full name:** Barrierefreie-Informationstechnik-Verordnung 2.0 (BITV 2.0)
- **Mandatory:** Yes for federal and state government bodies
- **WCAG basis:** WCAG 2.1 AA (via EN 301 549)
- **Unique requirements — BEYOND WCAG:**
  - **Annex 2 — Sign Language Video:** Website must provide a DGS (Deutsche Gebärdensprache) video explaining its content and navigation
  - **Annex 2 — Easy Language:** Key content must have a Leichte Sprache (easy-to-read) version
  - BIK BITV-Test: German-specific 60-step testing procedure
  - Mandatory accessibility statement (Erklärung zur Barrierefreiheit)
  - State-level enforcement by disability commissioners
- **URL:** https://www.gesetze-im-internet.de/bitv_2_0/ | https://www.bundesfachstelle-barrierefreiheit.de/

---

### France — RGAA 4.1

- **Full name:** Référentiel Général d'Amélioration de l'Accessibilité (RGAA) v4.1
- **Mandatory:** Yes — public sector + private companies with >250M€ annual revenue
- **WCAG basis:** WCAG 2.1 AA
- **Unique requirements:**
  - 106 test criteria across 13 themes (more specific implementation tests than WCAG)
  - Mandatory **Accessibility Declaration** (Déclaration d'Accessibilité) published on each site
  - Mandatory **multi-year accessibility plan** (Schéma Pluriannuel)
  - Annual progress reports
  - Conformance rate percentage displayed on homepage
  - **Fines up to €20,000 per non-compliant site per year**
  - Extends to **large private companies** (unique in Europe)
  - DINUM (Interministerial Digital Directorate) enforces
- **URL:** https://accessibilite.numerique.gouv.fr/ | https://www.numerique.gouv.fr/publications/rgaa-accessibilite/

---

## PDF Accessibility

### PDF/UA — ISO 14289-1

- **Full name:** ISO 14289-1:2014 — Document management applications — Electronic document file format enhancement for accessibility for use by persons with disabilities
- **What it covers:** Technical requirements for accessible PDF documents usable with assistive technologies
- **Referenced by:** Section 508, EN 301 549, WCAG (1.1.1, 1.3.1)
- **Key unique requirements:**
  - All real content must be tagged (PDF tag structure tree)
  - Tag tree must accurately reflect logical reading order
  - Natural language declared at document level (and overridden for language changes)
  - Figures must have `Alt` entry (alternative text)
  - Tables must use TR/TH/TD tags with `scope` and `headers` attributes
  - Decorative content marked as artifacts (AT skips them)
  - Unicode mapping required for all characters (text-to-speech requires this)
  - Document title in properties, set to display in title bar
  - `PDF/UA-1` identifier in XMP metadata
  - Security must not block AT from reading content
  - Links and form fields must have tab order matching logical structure
- **URL:** https://www.iso.org/standard/64599.html | https://www.pdfa.org/pdfua/

---

## Mobile App Accessibility

### WCAG 2.1 — Mobile-Specific Criteria

Key criteria added in WCAG 2.1 specifically for mobile:
- **1.3.4 Orientation** — content not locked to portrait/landscape
- **1.3.5 Identify Input Purpose** — autocomplete attributes on personal data fields
- **2.5.1 Pointer Gestures** — multi-finger gestures must have single-pointer alternatives
- **2.5.2 Pointer Cancellation** — pointer-down actions cancellable
- **2.5.3 Label in Name** — visible label text included in accessible name
- **2.5.4 Motion Actuation** — device motion features have non-motion alternatives
- **1.4.10 Reflow** — 400% zoom without horizontal scroll

### BBC Mobile Accessibility Guidelines

Publicly published, platform-specific for native iOS and Android apps:
- Grouped actionable items: related elements grouped into single focusable units
- Swipe gestures must have alternatives
- Interactive elements minimum 44×44pt touch target
- Custom components expose correct roles, states, values via platform APIs
- Dynamic content changes announced via accessibility notifications
- Forms: persistent visible label (not just placeholder text)
- Video/audio: captions, audio description, accessible media controls
- URL: https://www.bbc.co.uk/accessibility/forproducts/guides/mobile/

### Apple Human Interface Guidelines — Accessibility

- All interactive elements: `accessibilityLabel`, `accessibilityHint`, `accessibilityTraits`, `accessibilityValue`
- `accessibilityCustomActions` for complex gesture functionality
- **Dynamic Type:** all text must scale with user font size settings (`UIFontMetrics`)
- **Reduce Motion:** animations suppressed/substituted when setting enabled
- **Increase Contrast / Differentiate Without Color:** alternate assets required
- Switch Control and Full Keyboard Access: all actions reachable without touch
- Haptics complement but don't replace visual/audio feedback
- URL: https://developer.apple.com/design/human-interface-guidelines/accessibility

### Google Material Design — Accessibility

- Touch targets: minimum **48×48dp** with 8dp spacing between targets
- `contentDescription` on all ImageViews and icon-only buttons
- `importantForAccessibility="no"` for decorative elements
- `android:labelFor` to link labels to form fields
- `accessibilityLiveRegion`: ASSERTIVE for critical, POLITE for non-critical dynamic content
- Typography: `sp` units (scales with system font size)
- Contrast: 4.5:1 for text, 3:1 for large text and UI components
- Support both gesture navigation and button navigation on Android
- URL: https://m3.material.io/foundations/accessibility/overview

---

## Desktop Software Accessibility

### ISO 9241-171:2008 — Ergonomics of Human-System Interaction: Software Accessibility

- International standard; principles-based (not AT-API specific)
- **Key coverage:** input, output, navigation, timing, customization, window management
- Apps must respect system-wide accessibility settings (high contrast, sticky keys, filter keys)
- Window management: works when resized, minimized; content not clipped
- No information by color/sound/motion alone
- Flicker between 3–50Hz must be avoidable
- Documentation and help must itself be accessible
- URL: https://www.iso.org/standard/40727.html

### Section 508 — Software Chapter (E207)

- Non-web software must conform to WCAG 2.0 AA applied to software context
- **502 — Interoperability with AT:**
  - Software must not disrupt or interfere with AT
  - Must expose: object info, row/column, actions, focus, state, boundary, name, role, value, relationships, events
- **503 — Applications:**
  - Must use (not override) system display preferences
  - Caption/audio description controls at same menu level as other media controls
- In practice: requires compatibility with Windows MSAA, IAccessible2, UI Automation
- URL: https://www.access-board.gov/ict/

---

## Gaming Accessibility

### Game Accessibility Guidelines (GAG)

- Community-developed, widely adopted, three tiers: Basic / Intermediate / Advanced
- Covers: motor, cognitive, vision, hearing, speech
- **Selected Basic (must-have):**
  - Remappable controls
  - Pause function
  - Subtitles/captions with speaker identification
  - Visual indicators for all audio cues
  - Adjustable difficulty
- **Selected Intermediate:**
  - Support alternative input devices (switch, eye tracking)
  - High contrast modes
  - Adjustable text size
  - Individual audio channel control
- **Selected Advanced:**
  - Full colorblind modes
  - Screen reader support for menus
  - Auto-save at any point
- URL: https://gameaccessibilityguidelines.com

### XR Association — Developers Guide (VR/AR/MR Accessibility)

Unique to XR environments:
- Locomotion options (teleport vs. smooth); seated/standing toggle; vignette during movement
- All interactions reachable from seated position
- Alternatives to head-gaze input; controller-only interaction must work
- Critical info not at edge of field of view
- In-world text: minimum angular resolution (≥0.7° arc)
- 3D audio spatialization must have visual alternatives
- UI should be world-anchored or body-anchored (not head-locked)
- Voice and gaze alternatives to controller input
- Photosensitivity warnings (Epilepsy Foundation guidelines)
- Session pause; no mandatory time pressure in VR
- URL: https://xra.org/research/developers-guide-v2/

### Microsoft Xbox Accessibility Guidelines (XAG)

- Required: remappable controls, visual indicators for all audio
- Custom difficulty sliders (not just preset levels)
- Mental health: content warnings, skip distressing content, session time reminders
- Xbox platform accessibility feature tags for game listings
- URL: https://learn.microsoft.com/en-us/gaming/accessibility/xbox-accessibility-guidelines/

---

## AI / Chatbot Accessibility (Emerging)

No ISO or W3C standard specifically covers AI/chatbot accessibility yet (as of 2026), but:

### Applied Standards

- **WCAG 2.1/2.2** applies to chat interface itself (web/app-based)
- **ARIA live regions** (`role=log`, `aria-live=polite`) for new message announcements
- **W3C COGA** (Cognitive and Learning Disabilities) guidance: plain language, consistent navigation, support for users needing more time

### Key Requirements (Industry Practice)

- Chat windows must not auto-focus away from AT focus position
- New messages announced via ARIA live regions
- Typing indicators accessible (not only visual)
- File attachment controls keyboard/screen reader accessible
- Session timeouts extendable (WCAG 2.2.1)
- Voice-based chatbots must provide text alternatives for all interactions
- Multimodal AI (image + text input) must not require vision to operate
- AI-generated images should have accurate auto-generated alt text

### Emerging / In Development

- **W3C RQTF** is developing AI accessibility user requirements
- **EN 301 549 v4.0** (in development) expected to expand coverage to AI interfaces and XR
- **EU AI Act (2024+):** high-risk AI systems must be accessible per EN 301 549

---

## How to Use in an Audit

When auditing a target, map findings to the relevant standard:

- **Russian government site** → GOST R 52872-2019 + Mincifry checklist (see `gost-checklist.md`)
- **EU public sector site** → EN 301 549 / Web Accessibility Directive
- **EU private company site (2025+)** → European Accessibility Act (EAA)
- **US federal site** → Section 508 (WCAG 2.0 AA + Functional Performance Criteria)
- **US state/local government** → ADA Title II (WCAG 2.1 AA)
- **UK public sector** → Public Sector Bodies Regulations 2018 (WCAG 2.1 AA)
- **French site** → RGAA 4.1 (mention accessibility declaration requirement)
- **German federal site** → BITV 2.0 (flag sign language video and easy language requirements)
- **Canadian Ontario site** → AODA (WCAG 2.0 AA + policy/training requirements)
- **Japanese government site** → JIS X 8341-3:2016 (WCAG 2.0 AA)
- **Australian government site** → DDA + Digital Service Standard (WCAG 2.1 AA)
- **PDF documents** → PDF/UA (ISO 14289-1)
- **Video game** → Game Accessibility Guidelines
- **VR/AR app** → XR Association guidelines
