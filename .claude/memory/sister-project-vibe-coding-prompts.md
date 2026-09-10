---
name: sister-project-vibe-coding-prompts
description: the ON-RAMP for people starting with AI, so duplication is by design; ticket pass done 2026-09-10, and its short prompts are its best ones
metadata:
  type: reference
---

agigante80/vibe-coding-prompts is a sister project by the same author: a library of 14 versioned, platform-agnostic AI meta-prompts. It shares forge-kit's DNA (version-bump CI gate, no-dashes sentinel, docs standardization) and solved several problems forge-kit has not: a GENERATED README index with a `--check` CI gate (`scripts/update_prompt_index.py`), a per-prompt word budget with live counts, SHA-pinned actions in its own CI, and a two-stage pre-commit/pre-push hook split.

A full cross-review ran 2026-08-28. Filed there: #51 (OWASP Top 10:2025 cited but categories never listed), #52 (no SBOM or build provenance anywhere), #53 (new prompt: AI/LLM security, OWASP LLM Top 10), #54 (new prompt: AGENTS.md generator), plus a research comment on their existing #41 (accessibility). Filed here from what they do better: [[generated-index-and-size-budget]] covers #96 and #97; #98 covers CI self-hardening.

**Why:** the two repos solve the same governance problem from opposite ends (prose prompts pasted into a chat vs Claude-native components installed into a project), so each is the other's best source of borrowable mechanism and of honest scope comparison.

**How to apply:** before proposing anything to them, read their CLOSED issues first: every prompt already had a critical-review issue (#4 to #15) and #33 to #44 are existing prompt proposals, so duplicates are easy to file by accident. Their authoring standard is `docs/prompt-creation-guide.md`.

## The audience, stated by the maintainer 2026-09-10, and it changes the review

**It is the ON-RAMP: for people starting with AI-assisted development, and it has real users.** So
duplication with forge-kit is fine by design, and "more prompts" is the product rather than scope
creep. Judge a proposal by whether someone in their first months needs it, not by whether forge-kit
already covers the subject.

The two projects are two points on one path: prompts you paste, then components that fail a build.
forge-kit's README now names it as a Related project, and its `without-claude-code.md` guide names
it for the case that guide cannot cover, which is having no AI CLI at all.

## The pass done 2026-09-10

Closed six proposals as out of audience with reasons and a reopening trigger (#36, #38, #39, #40,
#42, #44: performance, migrations, validation, DB optimisation, monorepo, tutorial authoring).
Rewrote six into implementable tickets, ordered by what a beginner hits first: #43 docker compose,
#35 review checklist, #37 error tracking, then #34, #41, #33. Filed three: **#55** the README is an
index rather than an on-ramp, **#56** the 1600-word cap is enforced by nothing while ten prompts sit
within 45 words of it, and **#57** the graduation signpost pointing at forge-kit, written as a
signpost and not a funnel.

**Two findings worth remembering.** The word counts cluster at 1555 to 1598 with four outliers at
865 to 1033, and **the four short ones are the best prompts**: `github-actions-cicd-generator`
reached version 3.0.0 by getting SHORTER. And #51 is still the sharpest open item on either board: a
prompt that cites OWASP Top 10:2025, never lists the categories, and so lets the model fall back to
2021 while looking current.
