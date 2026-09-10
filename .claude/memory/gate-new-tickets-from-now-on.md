---
name: gate-new-tickets-from-now-on
description: maintainer decision 2026-09-10; six runs cost 110k to 225k tokens each and found five defects in none of the tickets, but do not expect that ratio to hold
metadata:
  type: feedback
---

Maintainer decision, 2026-09-10: **run `/gate-ticket <N>` on every NEW ticket in this repository before implementing it.** Existing closed tickets are not retro-gated.

**Why:** #184 established that forge-kit ships a ticket gate and had never gated a ticket. Scanning the last thirty issues found not one gate review comment, and the only bodies containing `template-version` contained it in prose. The kit's most distinctive mechanism was unexercised on the repository that ships it, which is the same shape as the label taxonomy before #104: declared, documented, and never applied.

**How to apply:** gate before implementation, not after. Expect Step 0c to fire on anything filed with `gh issue create`, which is how tickets are filed here (see [[tickets-here-are-hand-filed-so-mechanics-all-fail]]): it synthesises the missing sections and REWRITES that ticket's body on the forge. That is the behaviour nobody here had seen on a live ticket, and it is the point of the exercise. Do not retro-gate the backlog: the same rewrite would mutate closed tickets whose work already shipped.

Related: [[develop-branch-workflow]], [[tickets-here-are-hand-filed-so-mechanics-all-fail]].

## The cost, measured 2026-09-10 over six runs

Between 110,000 and 225,000 subagent tokens per run, and nine to thirty-four minutes of wall clock.
Three tickets took six runs between them.

**What it bought, on that first day: five defects that were in none of the tickets under review**
(#188 the label taxonomy, which blocked every ticket here and shipped inside the phase; #189 the
stale plugin-cache resolution; #190 the checker's heading-level false positive; #192 the erasable
verdict region; and a stale test count in CLAUDE.md). It also stopped two of three tickets shipping
WRONG: one specified a check that this kit's own overnight guard would have denied, the other put
two contradicting rules in one file.

**Do not expect that ratio to hold.** Six runs found a great deal because nothing had ever been
pointed at this repository's own work, so they were draining a backlog of latent defects rather than
reviewing tickets. When that backlog is gone the same six runs will find much less.

**The amendment to watch for:** if it starts feeling heavy, the honest change is to gate what is
about to be IMPLEMENTED rather than what is about to be FILED. Filing a ticket costs nothing to get
wrong; implementing one costs a rewrite. That is not a reason to change the rule yet, and it is the
first thing to reach for when there is one.

Related: [[bounded-review-loop-in-practice]] for when to stop a gating loop.
