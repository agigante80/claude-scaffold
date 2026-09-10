---
name: a-ticket-assertion-is-a-claim-check-it
description: the gate caught four false factual claims in my own tickets on 2026-09-10; run the grep, run the suite, and ask whether the criterion can fail
metadata:
  type: feedback
---

A ticket that asserts something about the tree is making a claim, and on 2026-09-10 the gate caught four of mine that were false. Not opinions: checkable facts, each wrong, each written with confidence.

- `check-restatements.sh` was named as an applicable guard for `code-reviewer.md`. Its `GATE_FILES` array covers `ticket-gate.md` and its companions and never touches that file or that plugin group.
- The public leak suite was described as 72 cases. It is 80, and CLAUDE.md carried the same stale number, which is where I got it.
- `check-private-leaks.sh` was described as having a reach statement to extend. It had none at all, so two acceptance criteria described a file state that did not exist.
- "Documentation impact: none beyond the agent" was false and CI would have failed: the README and CLAUDE.md carry that agent's marker version, word count and group semver inside GENERATED regions, and `--check` runs in the build.

Two more of the same shape: an acceptance criterion that anchored on "lines 80 to 85" of a file the edit itself moves, and two separate criteria that could not fail because the guard they invoked does not measure the thing being changed (`check-component-size.sh` counts the component file, and never a skill's `references/`).

**Why:** every one of these was cheap to check and expensive to leave. A ticket is implemented from, so a false premise in it becomes a wrong change, and the reader most likely to act on it is a future session with less context than the one that wrote it. The gate caught them here; nothing catches them in a repository without one.

**How to apply:** before writing a factual claim into a ticket body, RUN the thing. Grep the guard for the filename. Run the suite and read its count. Open the header and look for the statement. Ask whether the acceptance criterion can actually fail, and if it names a guard, check that the guard measures what is changing. An anchor that a change will move is not an anchor: state the criterion behaviourally instead.

Related: [[verify-against-installed-artifacts]], [[verify-provenance-before-publishing-a-comparison]], [[gate-new-tickets-from-now-on]].
