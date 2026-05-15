# Accessibility Auditor portability upgrade plan

## Goal
Keep the skill universal across agent runtimes by separating portable audit logic from runtime-specific tool names, while preserving practical UX for zero-setup and richer audits.

## Planned changes
1. Rewrite `SKILL.md` to use capability-level instructions instead of Hermes-specific tool names.
2. Add controlled tool-extension policy:
   - use existing environment first
   - optional approved audit-tool allowlist for richer checks
   - no arbitrary installs outside the allowlist
3. Fix reference file names so the workflow matches the actual `references/` tree.
4. Update `README.md` so the project is described as portable, not Hermes-only.
5. Run a self-review to ensure the skill stayed practical and not overengineered.

## Constraints
- Keep references mostly unchanged.
- Do not turn the skill into vendor-specific documentation.
- Preserve graceful degradation and honest coverage reporting.
- Keep report format and scoring familiar.

## Definition of done
- Core workflow is runtime-agnostic.
- Approved extension tooling is explicit.
- No fake or missing file references remain.
- README and SKILL tell the same story.
- Skill remains practical for companies and developers.
