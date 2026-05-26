# How I Build

*PM Skills for 2026*

Product management in 2026 isn't strategy *or* build — it's both, in the same head, on the same day. Positioning, marketing, messaging, pricing, packaging on one side. Writing code, reviewing code, scaffolding new repos, understanding the market on the other. The job is to create value, not to ship blindly.

This repo is the collection of [Claude](https://claude.com/claude-code) skills I use to do that work. Each one is small, opinionated, and composable — you can run them from Claude Code, Claude.ai, or any agent that reads `SKILL.md`. Take them, fork them, see how I work.

## Skills

- [**bold-claim**](./skills/bold-claim/SKILL.md) *(positioning)* — Find the single contested sentence that drives a product's GTM motion. Researches the competitive landscape, generates 5–7 claim candidates across six archetypes, scores them against a 25-point sharpness rubric, and produces a messaging doc anchored on the winning claim.
- [**claim-review**](./skills/claim-review/SKILL.md) *(review)* — PM-lens code review. Scores a PR against the asserted claim across five dimensions (claim-aligned, surface-honest, felt-value, scope-honest, voice-aligned) and names the concrete gaps between what was promised and what the code ships. Composes with bold-claim.
- [**quickstart**](./skills/quickstart/SKILL.md) *(development)* — Scaffold a new CLI tool or script with my conventions. Interviews you for language and purpose, then sets up the directory, writes the starter files, lands the first commit. For the cases `create-*-app` doesn't cover.

More on the way — launch narratives, pricing positioning, customer-research synthesis, founder one-liners on the strategy side; repo hygiene and market-mapping skills on the build side. If there's a specific PM job you want a skill for, open an issue.

## Install

### As a Claude Code plugin (all skills)

Clone the repo into your Claude Code plugins directory:

```bash
git clone https://github.com/brainsparker/skills.git ~/.claude/plugins/brainsparker-skills
```

Claude Code reads [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) and registers every skill listed there on next launch.

### A single skill, globally

```bash
git clone https://github.com/brainsparker/skills.git /tmp/brainsparker-skills
cp -R /tmp/brainsparker-skills/skills/bold-claim ~/.claude/skills/
```

### A single skill, project-scoped

```bash
mkdir -p .claude/skills/bold-claim
curl -o .claude/skills/bold-claim/SKILL.md \
  https://raw.githubusercontent.com/brainsparker/skills/main/skills/bold-claim/SKILL.md
```

### Claude.ai

Upload the relevant `SKILL.md` to a Project. The skill activates whenever the conversation matches the trigger phrases in its frontmatter.

## Repo layout

```
.claude-plugin/
  plugin.json          # registers every skill in this repo
skills/
  bold-claim/
    SKILL.md
  claim-review/
    SKILL.md
  quickstart/
    SKILL.md
```

Each skill lives in its own folder under `skills/`.

## License

MIT — see [`LICENSE`](./LICENSE).
