# Slices doc template

Modelled on `chat-service/docs/superpowers/specs/2026-09-25-chat-service-slices.md`.

```markdown
# <service or initiative> — implementation slices

Date: YYYY-MM-DD
Status: Draft | Approved (YYYY-MM-DD)
Linear: <project ID and link>
Derives from: <PRD/BRD title, version/date, link> · <system design path or TDD link> · <other sources>

## Purpose

One paragraph: what this initiative delivers, and that this document cuts
it into vertical slices, each one Linear issue, each verifiable by hand
before the next starts. Section references (§) point at the design;
FR/NFR/BR at the PRD.

## Ground rules

- Local verification stack and test expectations.
- Stubs for dependencies that live in other repos, and which slice needs them.
- How open questions are treated (the design's or PRD's stated defaults).

## Open questions

| # | Question | Owner | Assumed default |
|---|---|---|---|

## Dependency order

Which slices are strictly sequential, which run in parallel (`11 ∥ 12–14`),
and why.

## Phase A — <name>

### Slice 1 — <deliverable in plain words>
- **Scope.** The behaviour by surface: operations, events, jobs, limits,
  error codes. FR/§ references.
- **Done.** Observable acceptance checks.
- **Manual check.** One way to see it working by hand.
- **Size.** 1 | 2 | 3 | 5 points. **Lane:** Backend | Mobile | Frontend | QA.
- **Needs.** Slices or other teams' work it depends on.

## Coverage

- PRD requirements not covered by any slice, and why.
- Out of scope, as the PRD or the product owner stated it.
```

When a slice is later built, append a **Built as** note under it (spec and
plan paths, deviations), as chat-service does, so the doc stays the map.
