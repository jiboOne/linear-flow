# Issue body template

Title: what the issue delivers, in plain words. No platform prefix, no
slice number. Example: "Attachments: upload tickets, storage callback, send
and read with files".

Description (Markdown). Omit a section that would be empty.

```markdown
**Status of the work:** built and gated on branch `feat/...`; needs the MR
opened against `main`, review and merge.
<!-- Only for work that already exists on a branch. -->

**What it delivers**
- Concrete behaviour, by surface: API operations, events, jobs, limits,
  error codes. Enough that a reviewer can tell when it is complete.

**Acceptance**
- Testable checks, each one observable from outside the code:
  "Expired ticket → 409; duplicate callback is a no-op."
- One manual check when it helps QA: "Run the flow with curl against
  cmd/fakestorage."

**References:** spec and plan paths in the repo, TDD/PRD sections,
decision IDs, the contract issue this builds against.
```

Fields, not body: estimate, assignee, team, project, labels, status,
blocked-by relations.
