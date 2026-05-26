---
name: claim-review
description: Review a pull request, diff, or shipped feature through a PM lens — does this code actually deliver what we claimed it would? Use this skill whenever the user says "claim review", "PM review", "review against the positioning", "does this match the claim", "review this PR for product alignment", or asks whether a shipped feature actually delivers the asserted value. Also trigger when the user is about to merge a PR or cut a release and wants a gut-check that the implementation matches the strategy doc, the bold claim, or the marketing copy. This is not a code-quality review — it checks alignment between code and positioning, not bugs or style. Composes with bold-claim: if a bold-claim doc is in the conversation, use it as the alignment yardstick.
---

# Claim Review

## What this skill does

A claim review is a code review with a different question. Most code reviews ask: is this code clean, fast, safe? A claim review asks: **does what this code actually does match what we said it does?**

Every product asserts something — a bold claim, a positioning sentence, a launch promise. Engineering ships code that's supposed to deliver on that assertion. The gap between the two is where products quietly fail: the claim says "no setup required" and the PR adds a config file. The claim says "for developers" and the new UI is a wizard. The claim says "the fastest X" and this PR makes one path 2ms faster while cold-start regresses.

This skill is for closing that gap before the PR merges.

What this skill is **not**:

- Not a code-quality review (style, bugs, complexity — use a real code reviewer or a tool like CodeRabbit)
- Not a security review (use a security-focused tool)
- Not a perf review (use profiling and benchmarks)
- Not a "should we ship this" vote — it's a lens, not a gate

## Inputs

Accept any of:

- A PR URL or `gh pr view` output
- A diff (`git diff main...HEAD`)
- A single file or function the user wants reviewed in context
- A branch name, with the comparison base inferred from the repo (default: `main`)

Also needs the **yardstick** — the assertion this code is supposed to deliver on:

- If a `bold-claim` doc is in the conversation, use it directly.
- If the user has shared a positioning sentence, PRD claim, or launch promise, use that.
- If neither is present, ask one targeted question: "What's the claim or positioning this PR is supposed to deliver on? One sentence is enough." Do not proceed without it. Without a yardstick, this skill is just a generic code reviewer.

## Process

### Step 1: Read what the PR actually does

Pull the diff. Write a one-paragraph internal summary of the **behavior shift** the PR creates — not the implementation, the user-facing change.

- What did the system do before this PR?
- What does it do after?
- Who experiences the change, and where?
- What's the new public surface (API endpoint, UI element, CLI flag, error message, config key)?

This is internal — do not show the user. It's the substrate for the alignment check.

### Step 2: Restate the yardstick

In one sentence, restate the claim, positioning, or promise this PR is supposed to deliver on. If the claim is multi-clause, pick the clause most relevant to *this* PR.

If the yardstick and the PR are obviously about different things ("the PR is a CI fix, the claim is about product speed") — flag that immediately and ask the user whether a claim review is what they want, or whether a normal code review is more appropriate. Do not invent alignment where there isn't any.

### Step 3: Walk the rubric

Score the PR against five dimensions (1–5 each, no half points):

| Dimension | Question |
|---|---|
| Claim-aligned | Does this PR move us toward the claim, away from it, or sideways? Sideways = 2. Toward = 4–5. Away = 1. |
| Surface-honest | Does the public surface (API, UI, error, config) carry the asserted positioning? Or does it leak the complexity we claim to hide? |
| Felt-value | Will a real user *experience* the asserted value because of this PR? Or does the value only exist in marketing copy? |
| Scope-honest | Is the PR doing exactly what the spec said? Sneaking in adjacent work? Half-shipping a feature? |
| Voice-aligned | Do the names, copy, and errors match the product's voice and positioning? |

Total each candidate (out of 25). Below 18 → revisions needed before merge. Above 22 → ship it. 18–22 → flag the specific dimension that's weak and let the user call it.

### Step 4: Identify the gap

For any dimension scoring below 4, name the specific gap. Quote the actual code, copy, or commit message — not a paraphrase. The gap has to be concrete:

- "Line 47 of `src/api/handler.ts` adds a required `apiKey` parameter, but the claim is 'no auth needed for first 100 requests'."
- "The error message `Error: Invalid input` in `validate.ts:12` does not carry the product's voice — the rest of the codebase uses second-person ('We couldn't parse what you sent. Try…')."

If you can't name a concrete gap with a line number or quoted string, the dimension probably isn't actually weak — re-score.

### Step 5: Produce the review doc

Output a short review doc:

**Verdict.** Ship / revise / re-scope. One sentence.

**Score.** The five-dimension table with totals.

**The gap.** For each dimension scoring below 4, the concrete gap with a quoted line. If everything scored ≥4, write "No gap — the implementation matches the claim."

**Suggested changes.** For each gap, the smallest change that would close it. Not "refactor X" — "rename `apiKey` to `accessToken` and make it optional below the 100-request threshold."

**What this review does not cover.** A one-line reminder: "This is a claim review, not a code-quality review. Bugs, perf, security, and style are out of scope — run those separately."

## Style

Plain, direct prose. Quote code verbatim. No vague feedback ("consider X", "maybe think about Y"). Every gap is a specific line and a specific change.

Match bold-claim's tone: if the PR is misaligned, say so. If the claim doesn't match what's being built, say *that* — sometimes the claim is wrong, not the code. A claim review can legitimately conclude "rewrite the claim, the code is correct."

## Anti-patterns to avoid

- **Drifting into code-quality review:** "This function is too long" is not a claim-alignment finding. Stay in the lens.
- **Vague alignment claims:** "This doesn't feel on-brand" is not a finding. Quote a specific line and explain the mismatch.
- **Approving on aesthetics:** A PR that ships clean code but doesn't deliver the claim still fails the review.
- **Inventing alignment:** If the PR and the claim are about different things, say so and stop. Don't force a connection.
- **Scoring everything 5:** If you've never returned a sub-20 score, you're not actually reviewing. Be willing to fail PRs.
- **Skipping the yardstick:** Without a stated claim or positioning, this skill is just a generic code reviewer. Refuse to run without the yardstick.

## When the input is a feature spec vs. a PR

If the input is a **PR** (post-implementation), the question is: does this match what we said?

If the input is a **feature spec or PRD** (pre-implementation), the question flips: does the spec describe behavior that, if shipped exactly, would deliver the claim? Same rubric, applied to the spec instead of the diff. This catches misalignment before any code is written.

If the input is a **shipped feature with no diff** (e.g., "review the new onboarding flow against our claim"), walk the actual user-facing surface — open it, use it, narrate what a user would experience, and apply the rubric to that experience. Code is irrelevant in this case; the lived surface is the artifact.
