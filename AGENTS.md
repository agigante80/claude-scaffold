# forge-kit: agent instructions

forge-kit is an AI-assisted project governance scaffold: a template repository of agents,
skills, commands, hooks, and issue-template governance. It is not a buildable application;
there is no package manager and no application test runner. Validation is the script suite
under `scripts/` (see the commands list in CLAUDE.md).

**Two different questions, two different files. This one is a pointer to both, by design: do
not duplicate content into it.**

- **Changing this repository?** [CLAUDE.md](CLAUDE.md) is authoritative. Read it in full first.
  Its rules (version markers, template lockstep, the no-dashes policy) apply to every agent
  working here, not only Claude Code.
- **Using forge-kit's governance in some OTHER project, without Claude Code?**
  [docs/guides/without-claude-code.md](docs/guides/without-claude-code.md) is the entry point:
  which rules are portable, what to copy, what you can run, and what you do not get.
