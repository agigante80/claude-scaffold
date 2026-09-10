---
name: generated-index-and-size-budget
description: "#96/#97 shipped, #150 set an orchestrator number, #174 added the always-on cost and #176 kept words as the unit; scripting a rule is the only lever that shrinks adapt"
metadata:
  type: project
---

Two structural weaknesses sit behind a large share of the review findings this repo keeps producing, both tracked as tickets (#96, #97) and both borrowed as diagnoses from [[sister-project-vibe-coding-prompts]]:

1. **The component inventory is hand-maintained in four places** (CLAUDE.md plugin table, README tables, forge-adapt's `references/*.md` maps, plugin.json descriptions) and nothing checks it against the tree. It drifted four separate times in the 2026-08-28 session, caught only by review agents. The extractor already exists (`scripts/forge-adapt-catalogue.sh`); only the rendering half and a `--check` gate are missing.

2. **There is no size budget for components.** `adapt/SKILL.md` is 7,357 words and `ticket-gate.md` is 5,794, against a 1,600-word cap for a whole prompt in the sister project. At that size the same rule ends up stated in four places and updated in two, which is precisely the finding shape that fired the review trip wire three times.

**Why:** both convert a recurring human-caught defect class into something mechanical, which is the repo's own stated preference (mechanical enforcement over prose persuasion, recorded in the CLAUDE.md boundary paragraph).

**How to apply:** when a review finds "this table is stale" or "this rule is stated in N places", treat it as an instance of one of these two, not as an isolated fix. Land #96 before #97 (the index provides the visibility the budget needs), and fix #95 before either, or the generated index will publish `vnone` for the adapt skill.

## Evidence: the drift keeps arriving on a cadence

Running `/init` against this repo is a **review pass, not a rewrite**, and three consecutive passes have each found multiple inaccuracies in a CLAUDE.md that reads as authoritative:

- **2026-09-04** (PR #100, commit `15956d3`): 4 gaps, including a Workflow section that told the reader to push straight to main while the validation section three screens up said both range guards are PR-only.
- **2026-09-06** (same PR, commit `50a27ca`): 5 more gaps, including a stale one-line CI description and an absolute "gate in the shell, not the interpreter" rule that `overnight-continue` had already violated on purpose. See [[hook-install-model]].
- **2026-09-06, again** (same PR, commit `da12cc9`): a third pass on the same day found 3 more, including a CI suite count that was one low and a two-branch description of `enforcement_enabled()` that actually has three. The third branch is the one this repo's own dogfooding depends on, so the text invited a reader to add a redundant `.claude/no-dashes` or to call the wiring broken. **Three passes, three sets of findings, none of them the same.** See [[hook-install-model]].

## A third instance of the same class: declarative files with no applier

Weakness 1 is usually stated as "the inventory is prose". The sharper form is **a declarative
file that nothing applies and nothing checks.** Found 2026-09-06 while triaging the backlog:
`.github/labels.yml` declares 18 labels and GitHub held 4. The missing set included `security`,
`critical` and `api`, which are not decoration but the executable inputs to `ticket-gate`'s lens
table, so **the kit's most distinctive mechanism was unexercisable on the repo that ships it**.
`docs/guides/labels.md` said only "create all labels using `gh label create`", a manual
instruction someone runs once. Labels created and #104 filed for the missing sync script plus
`--check`. Treat any `.yml` or `.md` in this repo that describes host or project state as
suspect until something applies it: labels today, the component inventory in #96, the same shape.

CLAUDE.md is itself a hand-maintained inventory, and it is 4,433 words, so it is an instance of **both** weaknesses at once. Treat a periodic `/init` accuracy pass as maintenance to schedule, not as evidence that the last pass was careless. The prose parts (hook shapes, enforcement reasoning) drift as readily as the tables, so a generated index would fix only half of it.

## Outcome, 2026-09-07: both landed, and the budget half has now hit its floor

#96 and #97 both shipped. The generated index removed the four-inventory drift class outright.
The budget's ratchet worked exactly as intended for seven consecutive fixes to `ticket-gate.md`,
each paying its own way out of duplication the work exposed (PASS defined twice, a thin check
stating its purpose three times, one rationale across two steps, the same `gh issue edit` snippet
in three places, an unexecutable carry-forward rule). That took it 5486 to 5209 while ADDING
behaviour, which is the strongest evidence the diagnosis above was right: the size WAS the
duplication.

Then it ran out. An eighth fix found no duplication left (a seven-word-shingle scan returns only
one symmetric table and one required restatement), and the baseline was raised once, 5209 to 5265,
by maintainer decision rather than by an agent's initiative. That is the only raise in the numbers'
history and it is recorded in both `check-component-size.sh` and CLAUDE.md.

**What this changes:** the payment technique is exhausted for this component, so #150 (successor to
the closed #109) now needs a capability decision or a policy change, not more compression.
Scripting prose is the one lever that worked without cost: #149 turned Step 3A's 544 words into a
68-test executable and made the removed part more trustworthy, not less. See
[[shipped-asset-path-resolution]] for the trap that shipping such an asset opens.

## Outcome, 2026-09-10: the decision was made, and then the question changed twice

#150 landed as a POLICY change with its number stated: an ORCHESTRATOR (mechanically, an agent
whose `tools:` declares `Agent`) gets 4000 with a 6000 ceiling, and the metric was re-derived to
charge an agent for what it PRELOADS. `ticket-gate` went 6355 to 5709 across that work without
losing a capability.

Then two tickets asked whether the budget measures the right thing at all, and both answers are
now in `check-component-size.sh` rather than in anyone's head:

- **#174**: the budget measured the ON-INVOKE cost (the body) and was silent about the ALWAYS-ON
  cost (the description, paid every session for a component you never invoke). That is now
  reported and deliberately NOT budgeted, because a description too short stops the component
  being found. The tree went 14,711 to 12,339 characters of description with all 48 quoted trigger
  phrases intact, by deleting sentences each component's body already carried.
- **#176**: the unit is WORDS, which nobody outside this repo uses, while Anthropic states 500
  LINES. All 20 of `adapt`'s fenced blocks were classified before anything moved: sixteen are
  commands the skill runs, four are templates it emits, none is reference material. Nothing could
  move, so the line count is reported beside the words and gates nothing.

**The lever that has ever worked is still the same one.** Converting a rule into a tested script
(#149) has now shrunk `adapt` four times, including twice in one day, and in #179 it was the only
reason a second half of a rule could be added at all: as prose it would not have fitted. When this
file needs to grow, that is the move, not a baseline request.
