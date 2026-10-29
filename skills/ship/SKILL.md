---
name: ship
description: "Use when implementation on a Linear-linked branch is complete and should go to review - '/ship', 'send BAC-142 for review', 'mark the MR ready'. Runs go-toolkit's verification gate, then marks the MR ready with the issue linked and requests reviewers so Linear moves it to In Review. Never merges unless the user explicitly asks."
---

# Ship

**Announce at start:** "I'm using linear-flow:ship to send <ID> for
review."

Load `linear-flow:using-linear-flow` first.

`/ship` stands in for option 1 of `go-toolkit:finishing-a-development-branch`
(open the MR). Do not also present that skill's menu. Its other rules still
apply: base and prefix confirmation, never `codex/`, never tag releases,
merge only on explicit request, cleanup only after merge.

## 1. Identify the issue

From the branch name (`feat/bac-142-...`), else the MR title, else ask.
`get_issue` it for title, labels and acceptance.

## 2. Run the gate

Run `go-toolkit:verification-before-completion` in full on the tree you
are about to push. If it fails, report the failures and stop. A green run
earlier in the session doesn't count.

For non-Go lanes, run the repo's own test and lint commands from its
`CLAUDE.md` or README instead; if none are documented, ask.

## 3. Check the acceptance list

Walk the issue's **Acceptance** bullets. For each, point to the test or
the manual check that covers it. Any bullet not covered: tell the user
before marking the MR ready — they decide whether to ship anyway.

## 4. Mark the MR ready

Push, then update the existing MR (create it if /start was skipped, as in
linear-flow:start step 4, but not as a draft):

- Title: `<type>: <ID> <summary>` — no `Draft:` prefix.
- Description:

  ```markdown
  Fixes <ID>

  ## What changed
  <summary>

  ## Spec and plan
  docs/specs/...  docs/plans/...

  ## Verification
  <gate summary: build, vet, unit, integration, lint, coverage on changed lines>

  ## Acceptance
  - <each acceptance bullet> — <covering test or check>

  <security note when labelled: "Security-labelled: needs two human approvals.">

  🤖 Generated with [Claude Code](https://claude.com/claude-code)
  ```

  No `Co-Authored-By` trailer in the description.

With `glab`: `glab mr update <id> --ready --title ... --description ...`.
Without it: the push-option form in linear-flow:using-linear-flow.

If the MR was created in this step (no /start), run the "Status modes"
sync for *draft MR created* right away — attach the MR and, in `manual`
mode, set In Progress — before going on to reviewers.

## 5. Request review

Ask who reviews unless the user already said (one reviewer; two when
`security`). With `glab`: `glab mr update <id> --reviewer <user>[,<user>]`.
Without it, give the MR URL and ask the user to add reviewers.

## 6. Check Linear and report

Apply the "Status modes" rule from linear-flow:using-linear-flow: in
`manual` mode attach the MR URL (if not already attached) and set In
Review when the team has that status; in `connected` mode re-read the
issue and check the MR is attached and the status is In Review, reporting
if not (never drag a card). Report the MR URL, the gate summary, and the
issue status. Stop here.

## After review

- Review feedback → `go-toolkit:receiving-code-review`; push fixes to the
  same branch. The MR and issue stay linked; nothing to update in Linear.
- **Merge only when the user explicitly asks to merge this MR.** Then
  follow go-toolkit:finishing-a-development-branch's merge and cleanup
  steps exactly (squash message without trailers, verify main, remove the
  worktree). Immediately after the merge, apply the "Status modes" rule:
  in `manual` mode set In QA when the team has that status; in `connected`
  mode re-read the issue and report its status. If the user merged in the
  GitLab UI and tells you, do the same sync then. Never set Done — QA does
  that after sign-off.
