# Session handoff: thirteen tickets, three phases, two releases

Date: 2026-09-10

## Summary

Cleared the whole board twice. Worked the plugin-CLI phase to completion, then opened and finished
two more phases that came out of it: the boundary with forge-kit's neighbours, and the half of the
governance layer that needs no Claude Code. Released v0.3.0 and v0.4.0.

## Done this session

- **Phase "What Claude Code now ships itself" closed**: #172 (marketplace staleness in `drift`),
  #169 (declared cross-group dependencies), #173 (`author` on every manifest), #170 (`plugin
  details` rejected as the metric), #171 (no per-plugin tags), #175 (reference-depth guard), #174
  (the always-on description cost).
- **Phase "Standing next to the neighbours" opened and closed**: #177 (`check-neighbour-overlap.sh`,
  duplicate fails and collision reports), #178 (**11 components and the whole `forge-kit-backend`
  group retired, 5,507 lines**), #179 (one coexistence table covering superpowers AND the
  marketplaces, in a tested script), #180 (no agent-name prefix, decided; dispatch-target check
  shipped anyway), #181 (README rewritten around the outer loop).
- **Phase "The unit the budget defends" opened and closed**: #176. All 20 of `adapt`'s fenced
  blocks classified; none can move; the line count is now reported and gates nothing.
- **Phase "The half that needs no Claude Code" opened and closed**: #182
  (`forge-gate-mechanics.sh`, the mechanical gate runnable without the harness) and #183
  (`docs/guides/without-claude-code.md`, and AGENTS.md now serves both audiences).
- **v0.3.0 and v0.4.0 released**, both tagged on green and published from the CHANGELOG section.
- New guards, all in CI with contract tests: `check-neighbour-overlap.sh` (+ its manifest and
  refresh), `check-reference-depth.sh`, `test-validate-plugins.sh` (the oldest structural guard
  finally has one), `forge-adapt-neighbour-disposition.sh`, `forge-gate-mechanics.sh`.

## In progress (where we left off)

Nothing is half-done. The tree is clean, `main` and `develop` are level, CI is green, no phase is
open.

## Next steps

1. **#184 is the live work and needs a phase.** Every ticket in this repository fails or refers
   every mechanical check. Read Step 2 and Step 3A of `ticket-gate.md` and establish whether the
   mechanics are fed the forge's body or a synthesised one. If the gate does not synthesise, then
   the rule "a mechanical failure must never be lost to a clean critic" has not been holding, and
   that becomes its own ticket rather than a quiet fix.
2. A release is NOT due: two entries in `## Unreleased` since v0.4.0.
3. The three dead `forge-kit-adapt` local registrations (projects deleted) are still in
   `~/.claude/plugins/installed_plugins.json` and are only removable by hand.

## Decisions and why

- **Retire rather than fork.** Five components were 1 to 10 lines from `wshobson/agents`
  originals. Maintaining a fork nobody had changed cost budget, markers, semvers and drift
  tracking, and bought nothing. `architect-review` stayed because `/full-review` dispatches it by
  name, and that exception is in `.neighbour-allow` with its reason.
- **`full-review` is the counter-example, not an offender.** Same ancestor, 173 lines diverged, and
  what diverged is the iteration contract, which its upstream has none of. That is the shape this
  kit should have wherever it touches a neighbour.
- **Duplicate fails, collision reports.** A guard that treated every shared name as a defect would
  be switched off. The threshold is measured: duplicates differ by 1 to 10 lines, the nearest real
  divergence is 103.
- **The always-on cost and the line count are REPORTED, never budgeted.** A description too short
  stops a component being found, and a hard line limit would fail components for a number
  Anthropic calls a tip.
- **No agent-name prefix** (#180): Claude Code already namespaces subagent types by plugin.
- **The ratchet was raised once and given back the same day.** #172 needed 14 words; #178's
  retirement returned them; #179 then took `adapt` to 7209 by scripting the coexistence rule.

## Open questions / blocked on

- #184's central question, above. It is the only thing here that questions something the repo
  already believed.
- Whether `forge-gate-mechanics.sh` should distinguish "never template-shaped" from "missing a
  section". Depends on #184's answer; the ticket says so.

## Key context to reload

- `docs/roadmap.md` (four phases closed today, each with its close review)
- `.claude/memory/tickets-here-are-hand-filed-so-mechanics-all-fail.md` and
  `.claude/memory/verify-provenance-before-publishing-a-comparison.md` (both written this session)
- `scripts/check-neighbour-overlap.sh` and `docs/neighbours.tsv` (the boundary, and its evidence)
- `gh issue view 184`
- `docs/guides/without-claude-code.md` (the portability claim, now narrowed and true)
