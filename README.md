# Bold Claim

A Claude skill for finding the **single contested sentence** that drives a product's GTM motion — not a tagline, not a description, a claim a competitor would push back on.

Most positioning drafts fail the same way: they describe a category instead of taking a stance inside it. This skill researches the competitive landscape, generates 5–7 claim candidates across six archetypes, scores them against a 25-point sharpness rubric, and produces a messaging doc anchored on the winning claim.

## Install

### Claude Code

```bash
git clone https://github.com/brainsparker/Bold-Claim.git ~/.claude/skills/bold-claim
```

Or, for a single project:

```bash
mkdir -p .claude/skills/bold-claim
curl -o .claude/skills/bold-claim/SKILL.md \
  https://raw.githubusercontent.com/brainsparker/Bold-Claim/main/SKILL.md
```

Claude Code picks up the skill on next launch.

### Claude.ai

Upload `SKILL.md` to a Project. The skill activates whenever the conversation matches the trigger phrases in the frontmatter.

## Use it

Trigger phrases:

- "What's the bold claim for [product]?"
- "Find the bold claim in this PRD"
- "Help me position [feature]"
- "What's the one sentence that defines this?"

Or paste a PRD, strategy doc, or project brief and ask how to pitch it.

## What you get back

1. A short internal read of the product (who, what changes, why now)
2. 4–8 web searches across competitors, adjacent claims, and contested terrain
3. 5–7 candidate claims scored on contestability, specificity, falsifiability, behavior change, and memorability
4. Top 3 surfaced for your pick
5. A messaging doc with: the claim, the antagonist, three proof points, why-now, behavior shift, surfaces it must win on, and 3–5 one-liner variants

## Full spec

See [`SKILL.md`](./SKILL.md).

## License

MIT — see [`LICENSE`](./LICENSE).
