---
name: gate-new-tickets-from-now-on
description: "maintainer decision 2026-09-10 after #184 found the gate had never run here; new tickets only, never retro-gate the closed backlog"
metadata:
  type: feedback
---

Maintainer decision, 2026-09-10: **run `/gate-ticket <N>` on every NEW ticket in this repository before implementing it.** Existing closed tickets are not retro-gated.

**Why:** #184 established that forge-kit ships a ticket gate and had never gated a ticket. Scanning the last thirty issues found not one gate review comment, and the only bodies containing `template-version` contained it in prose. The kit's most distinctive mechanism was unexercised on the repository that ships it, which is the same shape as the label taxonomy before #104: declared, documented, and never applied.

**How to apply:** gate before implementation, not after. Expect Step 0c to fire on anything filed with `gh issue create`, which is how tickets are filed here (see [[tickets-here-are-hand-filed-so-mechanics-all-fail]]): it synthesises the missing sections and REWRITES that ticket's body on the forge. That is the behaviour nobody here had seen on a live ticket, and it is the point of the exercise. Do not retro-gate the backlog: the same rewrite would mutate closed tickets whose work already shipped.

Related: [[develop-branch-workflow]], [[tickets-here-are-hand-filed-so-mechanics-all-fail]].
