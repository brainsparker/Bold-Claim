# GTM Skills for Product Builders

[Claude](https://claude.com/claude-code) skills for the positioning, messaging, and narrative work that founders, PMs, and product engineers can't outsource.

You shipped the product. Now you need a sentence that makes a stranger care, a launch post that doesn't sound like every other launch post, and a homepage that takes a stance. These skills help with that part — the part that doesn't get easier just because the code works.

Each skill is small, opinionated, and composable. Run them from Claude Code, Claude.ai, or any agent that reads `SKILL.md`.

## Skills

- [**bold-claim**](./skills/gtm/bold-claim/SKILL.md) — Find the single contested sentence that drives a product's GTM motion. Researches the competitive landscape, generates 5–7 claim candidates across six archetypes, scores them against a 25-point sharpness rubric, and produces a messaging doc anchored on the winning claim.

More on the way — launch narratives, customer-research synthesis, pricing positioning, founder one-liners. If there's a specific GTM job you want a skill for, open an issue.

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

Each skill lives in its own folder under a GTM sub-category. Sub-categories will grow as the collection does.

## License

MIT — see [`LICENSE`](./LICENSE).
