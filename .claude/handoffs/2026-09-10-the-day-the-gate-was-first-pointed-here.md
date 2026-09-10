# Session handoff: the day the gate was first pointed at this repository

Date: 2026-09-10

Second close of the same session. The first is
`2026-09-10-thirteen-tickets-three-phases-and-two-releases.md` and covers everything up to the
cross-agent phase. This one covers what came after.

## Summary

Decided to start gating tickets, pointed the gate at this repository for the first time, and spent
the rest of the session finding out what that costs and what it catches. Reviewed the sister project
and did a full pass on its tracker. Two more phases opened and closed.

## Done this session (since the first close)

- **#184 answered and closed.** The gate is sound: Step 0c synthesises a body and writes it back to
  the forge before Step 3A runs. What was true is that **the gate had never been run here**, on any
  ticket. That became a maintainer decision: gate every NEW ticket, never retro-gate the backlog.
- **Sister project reviewed and its tracker reworked** (`agigante80/vibe-coding-prompts`): six
  proposals closed as out of audience with reasons, six rewritten into implementable tickets, three
  filed (#55 on-ramp, #56 word cap, #57 the graduation signpost pointing here).
- **Phase "Borrowing back from the on-ramp" opened and closed**: #185 (leak guard reach statements),
  #186 (overnight premise check), #187 (the sweep rule), #188 (the label taxonomy).
- **v0.4.0 released** earlier in the session, before the first close.
- forge-kit's README now names the sister project, and `without-claude-code.md` names it for the
  case that guide cannot cover.

## In progress

Nothing. Tree clean, `main` and `develop` level at `d0e38bf`, CI green, no phase open.

## Next steps

1. **#189 first.** P1, the cheapest of the four, and it corrupted three of four gate runs today:
   `find ~/.claude/plugins -name check-ticket-mechanics.sh | head -1` selects among four copies and
   picked a stale one. All four installed copies are component v4; only the tree is v5. The
   resolution order to implement is in the ticket's second comment.
2. **#192 next.** The gate's verdict region is erasable by an ordinary body edit, which I did twice
   today without noticing, and it means the trip wire can never fire. A stopping rule that cannot
   fire is worse than one that is absent.
3. #190 (heading-level false positive) and #191 (the deferred history mode) after those.
4. Any of them needs a phase opened first.
5. In the sister project, **#51 is the sharpest open item on either board**: a prompt citing OWASP
   Top 10:2025 without listing the categories, so the model falls back to 2021 while the prompt
   looks current.

## Decisions and why

- **Gate new tickets, never retro-gate.** Step 0c rewrites bodies, and doing that to closed,
  implemented work is destructive.
- **Add area labels that fit this repository** (`components`, `tooling`, `governance`) rather than
  mislabelling forge-kit's own work as `backend`. The label routes the review set, so a false one is
  a lie the machinery acts on.
- **Stop gating at two rounds.** Both round 2s found defects in the round-1 fix, everything was
  classed significant with nothing fundamental, so the contract licensed no third round. Everything
  unfixed became a ticket.
- **Ship #185's outcome B, defer A.** Reading a length-delimited stream by declared bytes is
  mandatory and cannot be done under this repo's bash 3.2 rule. That contradiction is #191.
- **Duplication with the sister project is fine.** It is the on-ramp and has real users.

## Open questions

- Whether "gate every new ticket" should become "gate what is about to be implemented". Not yet: two
  data points is not a pattern, and today's ratio was excellent. The memory records what to watch.
- Whether #189's fix should prefer the repository's own tree when the gate runs inside a forge-kit
  checkout. I think yes, and the ticket argues it, but it is a resolution-order decision worth a
  second opinion.

## Key context to reload

- `gh issue list --repo agigante80/forge-kit --state open` (four, all Backlog)
- `.claude/memory/gate-new-tickets-from-now-on.md` (the decision and its measured cost)
- `.claude/memory/a-ticket-assertion-is-a-claim-check-it.md` (four false claims of mine, and how to
  avoid the fifth)
- `.claude/memory/bounded-review-loop-in-practice.md` (the contract governs gating loops too)
- `docs/roadmap.md`, the last two phase close reviews
