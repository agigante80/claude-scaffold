---
name: verify-provenance-before-publishing-a-comparison
description: "2026-09-10: five near-duplicates were credited to Anthropic and are wshobson/agents; read known_marketplaces.json before naming a publisher"
metadata:
  type: feedback
---

Measured before checking the source, and published the answer. On 2026-09-10 I compared this tree against the marketplaces installed on the maintainer's machine, found five components effectively identical to files shipped elsewhere, and wrote them up as belonging to "the official plugins". They are `wshobson/agents`, added as the `claude-code-workflows` marketplace and the upstream forge-kit's specialist agents were forked from. Anthropic's own marketplace overlaps differently and mostly with different implementations.

The measurement was right. The attribution was not, and it reached a public README and two ticket bodies before `~/.claude/plugins/known_marketplaces.json` was read, which takes one command and settles it.

**Why:** a comparison is an accusation about provenance, and provenance is a separate fact from similarity. A marketplace NAME says nothing about who publishes it: `claude-code-workflows` sounds first-party and is a community collection; superpowers is distributed THROUGH Anthropic's marketplace from `obra/superpowers`. Getting this wrong in public is worse than not publishing, because the correction chases the claim.

**How to apply:** before writing who ships something, read `~/.claude/plugins/known_marketplaces.json` and quote the `repo` field. Do it in the same breath as the diff, not after someone asks. If the finding is going into a ticket or a README, put the source repository in the sentence rather than the marketplace directory name.

Related: [[claude-plugin-cli-facts]], [[research-before-presenting-a-judgment-call]].
