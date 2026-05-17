---
name: bold-claim
description: Identify the single bold claim that drives GTM strategy and messaging for a product, feature, or project. Use this skill whenever the user says "bold claim", "find the bold claim", "what's the claim for X", or asks for positioning, GTM narrative, the "one sentence" that defines a product, the "why does this exist," or messaging that will get attention in a crowded market. Also trigger when the user shares a PRD, strategy doc, or project brief and asks how to position it, sell it, pitch it, or what the headline should be. This skill researches the competitive market, generates multiple claim candidates with a sharpness rubric, and produces a final messaging doc anchored on the winning claim.
---

# Bold Claim

## What this skill does

A bold claim is the single contested sentence that drives a product's entire GTM motion. Not a tagline. Not a description. A claim — something a competitor would push back on, that takes a stance about how the world works or should work, and that forces buyers to either agree or disagree.

This skill takes context about a product, feature, or project, researches the market, and produces the bold claim plus the messaging derivatives that follow from it.

Examples of bold claims (for reference):

- "The default search layer for the agent stack" (contested: every search vendor wants this)
- "AI needs a canonical identity layer — DNS for brands" (contested: assumes a missing primitive)
- "Stripe for X" (contested: asserts category dominance via analogy)
- "The fastest way to ship production agents" (contested: every framework claims speed)
- Weak examples (do not produce these): "A modern search API for developers", "AI-powered enterprise platform", "Fast, reliable, scalable"

The difference between a bold claim and a description: a bold claim has an antagonist. If no competitor would disagree, it's not bold.

## Inputs

Accept either:

- **Loose context**: pasted docs, PRD text, Linear/Notion content, or conversation history about the product
- **A pointer**: Linear project ID, Notion page URL, file upload

If the pointer is provided, fetch it. If multiple sources are referenced, read them all before proceeding.

If the context is thin (less than ~200 words of substantive product detail), ask one targeted clarifying question before researching. Specifically ask for: who the user is, what they do today instead, and what the product does differently. Do not proceed without these three.

## Process

### Step 1: Extract the working hypothesis

From the input context, write a one-paragraph internal summary covering:

- **What it is** (product/feature/project)
- **Who it's for** (specific user, not "developers" or "enterprises")
- **What changes** (the behavior shift this creates)
- **Why now** (what's true today that wasn't 2 years ago)

This is internal — do not show the user yet. It's the substrate for everything else.

### Step 2: Research the market

Always run web research. Search for:

1. **Direct competitors** — who else solves this problem? Pull their headline claims from homepages.
2. **Adjacent claims** — what is the dominant narrative in this category right now? What are the loudest voices saying?
3. **Contested terrain** — what claims are competitors *avoiding*? Sometimes the bold claim is the one no one wants to make.
4. **Recent shifts** — has anything in the last 6-12 months created new space (a launch, a failure, a category move)?

Use 4-8 web searches. Quote competitor taglines and homepage hero copy when relevant. Capture the actual words, not paraphrases — the bold claim has to be sharper than the existing landscape, and that requires knowing the landscape verbatim.

**Metaphor check.** If the input context already uses a structural metaphor ("DNS for X," "Stripe for Y," "GitHub of Z"), search specifically for whether that metaphor is already claimed in the adjacent category. A metaphor that sounds fresh internally is often already taken externally. If it's taken, the candidates must avoid it or reclaim it explicitly against the incumbent. Do not let the user keep a metaphor that a competitor or adjacent player has already planted a flag on.

**Antagonist identification.** Before generating candidates, write a single sentence: "The bold claim must be sharper than [specific incumbent or dominant framing]." Name names. "Sharper than llms.txt" is useful. "Sharper than the existing market" is not. This sentence anchors Step 3.

### Step 3: Generate claim candidates

Generate **5-7 candidate claims**. Do not stop at 3 — the first 2-3 are almost always descriptive. The sharper ones come later. Force yourself past the obvious framings.

**Use the user's existing framing as C1.** If the input context contains a working tagline or claim, generate it verbatim as the first candidate — labeled and rejected explicitly as "the descriptive starting point." This makes it visible *why* the other candidates are sharper, and prevents the user's existing language from quietly anchoring the rest of the candidates.

Vary the candidates across these archetypes:

- **Category claim**: "X is the new Y" / "the default for Z"
- **Antagonist claim**: "Most X is broken because Y" / "Stop doing X, start doing Y"
- **Asymmetric truth claim**: "The thing everyone believes about X is wrong"
- **New primitive claim**: "X needs a missing layer/protocol/standard for Y"
- **Inevitability claim**: "X will happen — the only question is who builds it"
- **Reframe claim**: "X isn't about Y, it's about Z"

Each candidate is one sentence. Maximum 12 words for the main clause. A two-sentence claim is allowed only if the second sentence is the punch (e.g., "Setup, then payoff"). Long inevitability claims ("X is happening — the only question is…") consistently fail on memorability; use sparingly and only if the trade-off is worth it.

**Memorability test.** After drafting candidates, read each one out loud once, wait ten seconds, and try to recall it. If you can't reproduce it close to verbatim, dock its memorability score. Claims that fail this test will fail in the wild — sales reps won't remember them, developers won't repeat them, the press won't quote them.

### Step 4: Score each candidate

Score each candidate against this rubric (1-5 each, no half points):

| Dimension | Question |
|---|---|
| **Contestable** | Would a competitor push back on this? If no, score 1. |
| **Specific** | Is it about *this* product, or could it apply to anything in the category? |
| **Falsifiable** | Could we be wrong? Is there a future where this claim looks foolish? |
| **Behavior-changing** | If a buyer believes it, do they do something different? |
| **Memorable** | Could someone repeat it correctly 24 hours later? |

Total each candidate (out of 25). Reject anything below 18. If nothing scores above 18, generate another round — do not present weak claims.

Show the user the top 3 candidates with their scores and a one-line rationale each. Ask them to pick or push back.

### Step 5: Build the messaging doc

Once a claim is selected, produce a short doc with:

**The Claim**
The single sentence, exactly as it should appear.

**The Antagonist**
One sentence naming what we are *against*. Every bold claim implies an opponent — make it explicit. ("We believe X" requires "as opposed to Y.")

**Why It's True**
Three proof points. These are evidence-based — data, behavior, market shifts, technical reality. Not feature lists.

**Why It Matters Now**
One paragraph on the timing. What's true in 2026 that makes this claim land? Why would it have failed in 2024?

**What Changes If People Believe It**
Two or three sentences on the behavior shift. What does a buyer do differently? What does the market do differently? This is the GTM hook.

**Where This Shows Up**
A short list of artifacts that need to carry the claim: homepage hero, sales pitch opening line, founder podcast soundbite, recruiting copy, etc. Be concrete about *where* the claim has to win.

**One-Liners**
3-5 variations of the claim for different surfaces (tweet, sales deck, conference talk title, etc.). Keep them tight.

## Style

Plain declarative prose. No bullets inside the messaging doc body except where the structure calls for them. The doc should read like a memo, not a deck. Argument over description.

The user prefers direct, opinionated writing — match that. If a candidate is weak, say so. If the input context is too thin to find a bold claim, say so and ask for what's missing.

## Anti-patterns to avoid

- **Adjective stacking**: "Fast, secure, scalable" is not a claim. Reject any candidate that's mostly adjectives.
- **Category-of-one fluff**: "The world's first AI-native X" — no one believes "first" claims and they don't change behavior.
- **Internal language**: Claims using terms only employees use (architecture names, internal codenames) fail. The claim has to land cold.
- **Hedged claims**: "We help X do Y better" is not a claim. Cut the hedges.
- **Feature claims masquerading as positioning**: "The only X with Y feature" is a feature, not a claim. The claim is about what Y *means*, not that Y exists.
- **The "everything platform"**: If the claim could describe 5 different products, it's not specific enough.

## When the input is a strategy doc vs. a product

If the input is a **product or feature**, the claim is about what the product asserts.

If the input is a **strategy doc or initiative** (e.g., a GTM motion, a partnership program, a category bet), the claim is about what the *strategy* asserts — what truth about the market it's betting on. Adjust the antagonist and proof points to be market-level rather than product-level.

If the input is a **company-wide bet**, the claim should clear a higher bar — it should be the thing the company is willing to be wrong about publicly. These are rarer and harder. Push the user to confirm that's the scope before proceeding.
