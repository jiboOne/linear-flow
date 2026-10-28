# linear-flow

Linear and GitLab wrapper around [go-toolkit](https://gitlab.com/omno-limited/corebankos/backend-services/go-toolkit),
following the CoreBankOS delivery workflow: Git moves the board, Claude does
the admin, people decide, merge and sign off.

| Skill | Use |
|---|---|
| `/linear-flow:shape <project or PRD link>` | PRD/BRD (artifact, Claude Doc, Linear doc) → system design via go-toolkit if needed → `docs/specs/…-slices.md` |
| `/linear-flow:breakdown <project>` | Slices doc, project brief, specs/plans → Linear issues (preview, then create); stops and suggests `shape` when the sources are too thin |
| `/linear-flow:start <ID>` | Issue → go-toolkit brainstorm/plan/execute, branch `feat/bac-142-slug`, linked draft MR |
| `/linear-flow:ship` | go-toolkit verification gate → MR ready with `Fixes <ID>`, reviewers requested |
| `linear-flow:using-linear-flow` | Shared rules; also handles "BAC-142 is blocked by BAC-138", "log a bug on …", "what's next for me" |

## Prerequisites

- go-toolkit installed (`go-toolkit@corebankos`).
- Linear MCP connected in Claude Code:
  `claude mcp add --transport http linear-server https://mcp.linear.app/mcp`, then `/mcp` to sign in.
- `glab` recommended (`brew install glab && glab auth login`). Without it,
  MRs are created with git push options and reviewers are added by hand.
- Linear ↔ GitLab integration enabled with MR status automations per team.

## Install locally

```bash
claude plugin marketplace add ~/Developer/Projects/linear-flow
claude plugin install linear-flow@linear-flow-local
```

## Known gaps in the workspace (2026-10-28)

BAC has no Triage, In Review or In QA status, and no Area or Flags label
groups. These come from the Terraform catalogue. linear-flow skips those
transitions and labels and says so.
