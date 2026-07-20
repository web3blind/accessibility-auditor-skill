# Open GitHub accessibility issue → small PR workflow

Use this when the goal is not only to audit, but to turn a public accessibility issue into a safe, narrow upstream pull request.

## Candidate selection

Prefer issues that affect a real user flow and are still small enough for one focused PR:

- forms and validation feedback
- login, onboarding, checkout, or submission flows
- focus management and keyboard access
- dialogs, modals, dropdowns, selects, filters, or search
- screen reader announcements and status messages

Avoid tiny skip-link-only or typo-like cases when better candidates are available.

## Pre-coding verification gate

Before coding, verify:

1. Repository is active enough and not archived.
2. License and contribution context permit a PR.
3. The issue is open and concrete enough to map to source files.
4. The affected user flow is actually rendered by the files or components you plan to edit. Trace the real route, template, component, or shared-library stack from the issue to source before changing code. Do not assume that a similarly named legacy handler, shared helper, or old component owns the current flow.
5. Open and closed issues/PRs do not already contain an equivalent fix.
6. The fix can be limited to a component, helper, template, or test rather than a broad redesign.
7. The change improves WCAG semantics or focus behavior without unnecessary visual churn.

If one issue spans different rendering stacks or repositories, split the work into narrow PRs per actual owner instead of forcing one broad PR.

## Form-validation PR checklist

For validation/error work, check at minimum:

- visible label is programmatically associated with the control (`label[for]` + `id`, wrapping label, or framework equivalent)
- error text has a stable id when it is rendered
- invalid controls reference the error text with `aria-describedby` and preserve any existing described-by values
- `aria-invalid` is absent while valid and set to `true` only when invalid
- focus moves to the error summary or first invalid field after validation fails, when the user needs to discover errors
- dynamic status/error text uses appropriate live-region semantics without duplicate noisy announcements
- native `required`, input type, and constraints are preserved where appropriate

A good small PR usually includes a focused contract test that asserts the rendered/source-level semantics. If runtime screen-reader testing is not available, say that honestly in the PR body.

## PR communication

Keep the PR description concise:

- link the upstream issue
- describe the affected flow/component stack that was verified
- summarize behavior changes
- list exact validation commands and results
- label unrelated local/CI blockers clearly

Avoid claiming every form or app flow is fixed if the PR only covers one rendering stack or a subset of controls.
