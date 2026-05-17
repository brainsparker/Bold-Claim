# Bold Claim

**Stop writing positioning. Pick a fight.**

Positioning isn't a framework, a canvas, or a twenty-page doc. It's one sentence you'll defend in public — a claim a competitor would push back on, that takes a stance about how the world works or should work.

Bold Claim is a Claude skill that researches your category, generates 5–7 claim candidates against a named antagonist, scores them on a 25-point sharpness rubric, and produces a messaging doc anchored on the winning claim. The skill for founders and PMMs who'd rather defend a sentence than fill out a canvas.

## Install

### Claude Code

```bash
git clone https://github.com/brainsparker/bold-claim.git ~/.claude/skills/bold-claim
```

Or, for a single project:

```bash
mkdir -p .claude/skills/bold-claim
curl -o .claude/skills/bold-claim/SKILL.md \
  https://raw.githubusercontent.com/brainsparker/bold-claim/main/SKILL.md
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

## Before / after

**Input (PRD excerpt):** A logging SaaS for cloud-native engineering teams. Current hero copy: *"A modern observability platform for cloud-native teams."*

**Diagnosis:** Fails contestability (no competitor would disagree), specificity (could be Datadog, New Relic, Honeycomb, Grafana, or any of 30 others), and behavior change (no buyer changes anything on Monday).

**Selected claim:** *Your dashboards aren't observability — they're decoration.*

**Antagonist:** The "three pillars" vendors selling more graphs as the answer to more outages.

**Why it's true (proof points):**
1. The median SRE checks 4+ dashboards during an incident and still pages a human who knows the system.
2. 70%+ of dashboard panels are never viewed after the week they're created.
3. The teams shipping reliably aren't the ones with the most dashboards — they're the ones with the fewest.

**One-liner variants:**
- Tweet: "Your dashboards are decoration. Prove me wrong."
- Sales opener: "How many of your dashboards have been opened this quarter?"
- Conference talk: *Death of the Dashboard*

## When not to use this

Skip this skill for:

- **Documentation, API references, or feature descriptions** — those should be accurate, not contested.
- **Internal naming** (codenames, repo names, Slack channels) — bold claims are external.
- **Blog post titles or one-off marketing copy** — single-use copy doesn't earn the full process.
- **Concepts without a buyer yet** — bold claims need a real GTM motion to anchor. If you can't name who would disagree, you're not ready.
- **Situations where you won't actually defend the claim** — a claim you'll soften the moment a customer pushes back is worse than no claim at all.

If the goal is "make this sound better," that's copywriting. This skill is for positioning bets.

## Full spec

See [`SKILL.md`](./SKILL.md).

## License

MIT — see [`LICENSE`](./LICENSE).
