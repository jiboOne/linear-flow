# Workspace facts

Snapshot taken 2026-10-28 from the Linear MCP. The workspace is managed by
Terraform; these change through the catalogue, not through Claude. Re-query
when a call fails and tell the user what changed.

## Workspace

- Name: OMNO — https://linear.app/omno
- GitLab group: `gitlab.com/omno-limited/corebankos` (backend repos under
  `backend-services/`). Backend repos' default branch is `main`.

## Teams

| Key | Name | Parent | Lane |
|---|---|---|---|
| `COR` | CoreBankOS | — | parent team; project lead team |
| `BAC` | Backend | COR | Backend (Go) |
| `MOB` | Mobile | COR | iOS, Android |
| `FRO` | Frontend | COR | Web, backoffice |
| `QA` | QA | COR | QA automation, manual QA |
| `PRO` | Product | COR | Product, design |
| `PLA` | Platform | — | platform engineering |

## GitLab integration mode

| Team | Mode | Evidence |
|---|---|---|
| `BAC` | `manual` | 2026-10-29: chat-service MR !20, titled `Draft: feat: BAC-4 …`, never attached to BAC-4 and the issue stayed Todo. |
| others | `connected` (unverified) | no MR observed yet; switch to `manual` on the first miss. |

`connected` means Linear's GitLab integration attaches MRs and moves
statuses; linear-flow only re-reads and reports. `manual` means linear-flow
attaches the MR and sets In Progress / In Review / In QA itself (see the
"Status modes" rule in the skill). Flip a team back to `connected` once the
integration is installed for the group and a fresh MR attaches on its own.

## Statuses on BAC today

Backlog, Todo, In Progress, Done, Canceled, Duplicate.

**Missing vs. the target workflow:** Triage, In Review, In QA. Until they
exist, /ship leaves the issue in In Progress, and merge moves it straight to
whatever the team's merge automation says (or nothing).

## Labels today

- **Type** group (single select, exactly one): Feature, Bug, Chore, Spike,
  Tech debt. (`Improvement` is retired — never apply it.)
- **Area** group (Accounts, Cards, Payments, KYC, SCA, Backoffice): not
  created yet.
- **Flags** group (`security`, `agent-ok`, `blocked`, `client-request`):
  not created yet. Until `blocked` exists, use blocked-by relations only.

## People and roles

- Product owner / project lead: Aslan Inaishvili ("Alex",
  alex@corebankos.com) — owns Triage, Backlog, Todo, priorities.
- The person running Claude is the default assignee for issues they break
  down or start; use `me` in MCP calls.

## Projects in flight

- `P-COR-5` UBO - Support Center — target 2026-11-30, teams BAC, MOB, FRO,
  PRO, QA. Backend issues BAC-1 … BAC-12 (chat-service). BAC-6 … BAC-11 are
  estimated above 5 points and are split candidates.
