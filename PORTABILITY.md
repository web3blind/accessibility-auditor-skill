# Portability Notes

This skill is meant to work across agent runtimes such as Hermes, OpenClaw, Codex, Claude Code, and similar environments.

## Core Principle

Keep the skill split conceptually into 2 layers:

1. **Portable core**
   - workflow
   - audit logic
   - references
   - report structure
   - scoring
   - honesty and coverage rules

2. **Runtime execution layer**
   - how the environment fetches pages
   - how it renders JS-heavy pages
   - how it reads/searches local files
   - how it runs approved optional audit tools

The portable core should describe:
- what to inspect
- what evidence to gather
- what to report
- what cannot be concluded safely

It should avoid hard-coding vendor-specific tool names unless they are shown only as examples.

## Capability Mapping Examples

Examples of capability mapping by runtime:

- **Fetch page content**
  - OpenClaw: `web_fetch`
  - other runtimes: any equivalent page-fetch capability

- **Render interactive pages**
  - OpenClaw: browser tool
  - other runtimes: browser automation, Playwright, or equivalent rendering path

- **Read/search source files**
  - OpenClaw: `read`, `exec`, local shell search
  - other runtimes: file-read and search capabilities available in that environment

- **Run optional audit tools**
  - any runtime: only if already available or explicitly allowed by the runtime/user policy

These mappings are examples, not requirements.

## Install Policy

Preferred behavior:
1. use the current environment first
2. produce the best useful partial audit immediately
3. if richer checks need more tooling, use only the approved allowlist
4. do not install arbitrary tooling outside that set
5. if installs are not appropriate, recommend the exact next-step tools and continue with partial coverage reporting

## Why this matters

A portable skill should not become:
- Hermes-only
- OpenClaw-only
- Codex-only
- Claude Code-only

It should stay reusable while still giving a predictable, safe, and practical user experience.
