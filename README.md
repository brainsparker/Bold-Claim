# Skills

A collection of [Claude](https://claude.com/claude-code) skills for go-to-market, positioning, and messaging work.

Each skill is a focused, composable unit. Use them when you need to sharpen a claim, pressure-test a narrative, or move a fuzzy strategy doc into something concrete.

## Skills

### GTM

- [**bold-claim**](./skills/gtm/bold-claim/SKILL.md) — Find the single contested sentence that drives a product's GTM motion. Researches the competitive landscape, generates 5–7 claim candidates across six archetypes, scores them against a 25-point sharpness rubric, and produces a messaging doc anchored on the winning claim.

More skills coming. The repo is set up to grow.

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
cp -R /tmp/brainsparker-skills/skills/gtm/bold-claim ~/.claude/skills/
```

### A single skill, project-scoped

```bash
mkdir -p .claude/skills/bold-claim
curl -o .claude/skills/bold-claim/SKILL.md \
  https://raw.githubusercontent.com/brainsparker/skills/main/skills/gtm/bold-claim/SKILL.md
```

### Claude.ai

Upload the relevant `SKILL.md` to a Project. The skill activates whenever the conversation matches the trigger phrases in its frontmatter.

## Repo layout

```
.claude-plugin/
  plugin.json          # registers every skill in this repo
skills/
  gtm/
    bold-claim/
      SKILL.md
```

Each skill lives in its own folder under a category. Categories are loose — `gtm` today, more as they emerge.

## License

MIT — see [`LICENSE`](./LICENSE).
