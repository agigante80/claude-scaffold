---
name: tickets-here-are-hand-filed-so-mechanics-all-fail
description: "hand-filed via gh issue create, so no template-version marker and no ### headings; Step 3A returns 0 pass on every ticket (#184 asks which side is wrong)"
metadata:
  type: project
---

Every issue in this repository fails or refers every mechanical check in the ticket gate's Step 3A. Not some of them. Sampled #109, #129, #150 and #182 on 2026-09-10, the first day this was runnable outside the agent (#182): each returns `0 pass`.

Two structural causes, neither per-ticket:

- **No body carries the `template-version` marker.** #88, #103, #127 and #155 each contain zero occurrences.
- **No body uses the `### <label>` headings the checker matches.** `section_of()` in `check-ticket-mechanics.sh` matches `^### ` exactly, which is what GitHub renders from a FORM submission. Tickets here are filed with `gh issue create --body-file`, in hand-written markdown.

**Why it matters:** `ticket-gate.md` states that "every FAIL is a blocking item ... a mechanical failure must never be lost to a clean critic", and tickets here have nonetheless been gated to PASS. So either Step 2's auto-synthesis rewrites the body before Step 3A sees it, in which case the mechanics are fed something the forge never stored, or the strongest rule in the gate's own documentation has not been holding. #184 is open to answer which.

**How to apply:** do not read a run of `forge-gate-mechanics.sh` against a ticket in THIS repo as a judgement on that ticket's quality. The content is usually all there; the machine-checkable shape is not. When demonstrating the tool, say so, as `docs/guides/without-claude-code.md` does. And do not "fix" it by loosening the checker: its heuristics are deliberately narrow, and #149's whole argument is that a check which guessed would reject compliant tickets.

Related: [[bounded-review-loop-in-practice]], [[gh-cli-cannot-read-tmp]].
