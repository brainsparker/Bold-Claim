---
name: quickstart
description: Scaffold a new CLI tool or script repo with opinionated conventions. Use this skill whenever the user says "quickstart", "new repo", "new project", "scaffold a CLI", "scaffold a script", "init project", "starting a new tool", or asks how to begin a small Node, Python, or Bash utility from scratch. Also trigger when the user is in an empty or near-empty directory and asks to set up a new tool, when they say "I'm going to build a script for X", or when they're moving past a one-off experiment into a real repo. This skill interviews the user about language and purpose, then directly creates the directory, writes starter files (script + README + .gitignore + CLAUDE.md), and lands the first commit.
---

# Quickstart

## What this skill does

A quickstart is for the case `create-*-app` doesn't cover: a small CLI, a personal utility, a script that's going to grow into something. Not a web app, not a framework. One file or a handful, in Node, Python, or Bash, with the conventions I'd want every time but never want to type out from scratch.

This skill executes commands directly in the target directory. It does not output a runbook — it runs the steps. By the time it finishes, you have a directory with starter files, a first commit, and a printed next-step list.

Examples of what this skill is good for:

- A Bash script that parses production logs
- A Node CLI that wraps an internal API
- A Python utility for a personal data workflow
- A repo that's currently a single `.sh` file and needs to become structured

This skill is **not** for: Next.js apps, marketing pages, Claude/AI apps (those scaffolds belong in separate skills, deferred for now), web apps with frameworks, or anything `create-next-app` / `cookiecutter` already does well.

## Inputs

Accept either:

- A direct invocation: "scaffold a Bash script for X", "new Node CLI for Y", "quickstart a Python tool for Z"
- A vaguer one: "I want to start a new script", "let's spin up a repo for this"

The skill needs three things before doing anything: **language** (Node / Python / Bash), **project name** (kebab-case directory name), and **one-line purpose** (what the tool does). If any of these are missing from the input, ask for them before scaffolding. Do not proceed without all three.

Also clarify, if not obvious from the request:

- **Target directory** — where on disk should this live? Default: a sibling of the current working directory, named after the project.
- **Distribution** — local-only, or eventually published (npm, PyPI, Homebrew)? Affects packaging.

## Process

### Step 1: Interview

If the request is thin, ask 3–5 questions and wait for answers before doing anything:

1. Language? (Node / Python / Bash)
2. Project name? (kebab-case)
3. One-line purpose?
4. Will this be published, or stay local?
5. Does it need persistent config or state on disk? (Most scripts don't — default no.)

Do not over-interview. If the user already gave you language + purpose in the initial message, skip to confirmation: "I'll set up `<name>` as a <language> script for <purpose>. Target: `<path>`. Sound right?" — then proceed unless they push back.

### Step 2: Scaffold the directory

Run, in order:

```bash
mkdir <target-path>
cd <target-path>
git init -b main
```

Write a language-appropriate `.gitignore`:

- **Node:** `node_modules/`, `.env*`, `dist/`, `*.log`
- **Python:** `__pycache__/`, `*.pyc`, `.venv/`, `.env*`, `dist/`, `*.egg-info/`
- **Bash:** `.env*`, `*.log`, `.DS_Store`

### Step 3: Write the starter files

Branch by language. Each language has one canonical starter set.

**Node:**

```
<name>/
  package.json     # name, version, type: module, bin entry, no deps
  index.js         # shebang, minimal argv parsing, --help, placeholder behavior
  README.md        # purpose, usage example, install instructions if published
  .gitignore
```

`package.json` defaults to `"type": "module"`. The `"bin"` field maps the project name to `index.js`. No `commander` / `yargs` unless the script has more than 3 flags — write the argv parse inline. `chmod +x index.js`.

**Python:**

```
<name>/
  pyproject.toml         # project metadata, script entry, no deps
  <name>/__main__.py     # argparse, --help, placeholder behavior
  README.md
  .gitignore
```

Use a package directory named after the project (kebab-case → snake_case). `pyproject.toml` defines a `[project.scripts]` entry mapping the project name to `<name>.__main__:main`.

**Bash:**

```
<name>/
  <name>          # the script itself, executable, no extension
  README.md
  .gitignore
```

The script opens with `#!/usr/bin/env bash` and `set -euo pipefail`. Include a `usage()` function and a `--help` flag from line 1, even if there are no other flags yet. `chmod +x` the script.

### Step 4: Write `CLAUDE.md`

Every new repo gets a `CLAUDE.md` at the root. Keep it short — 20–40 lines. Anchor it on what Claude needs to know to work in *this specific repo*, not generic best practices.

Default sections:

- **Purpose** — one sentence on what this tool does (pulled from the interview).
- **How to run** — the exact command (e.g., `./<name> --help` or `python -m <name>`).
- **Conventions** — language-specific: "Node, ESM only, no deps unless asked"; "Python, stdlib-only unless asked"; "Bash, `set -euo pipefail`, POSIX-compatible where reasonable."
- **Out of scope** — what Claude should *not* add by default: tests, CI, lint config, framework dependencies, README badges.

### Step 5: Initial commit + next steps

Run:

```bash
git add -A
git commit -m "initial scaffold"
```

Then print a short next-steps list to the user:

- How to run the script (exact command, copy-pasteable)
- How to add a dependency if needed (`npm install`, `pip install`, etc.)
- How to publish, if distribution was set to published
- A pointer to `CLAUDE.md` if Claude will be working on this repo

Stop. Do not add features. Do not write tests. Do not configure CI. Hand off.

## Style

Execute commands directly — do not narrate every step. Show the user the structure after it exists, not before. One sentence per phase: "Scaffolding `foo-tool` as a Bash script…" → run the commands → "Done. Run `./foo-tool --help` to start."

Opinionated defaults baked in:

- Always include `--help` from the first commit, even with no other flags.
- Always set the executable bit on scripts.
- Always include a usage example in `README.md`.
- Always write `.gitignore` even for tiny repos.
- Always make the first commit before handing back.
- Never install dev dependencies unless asked.
- Never write tests, CI, or lint config unless asked.

## Anti-patterns to avoid

- **Reaching for `create-*-app`:** This skill exists specifically for the not-create-app case. If the user wants Next.js, hand off to the relevant Vercel skill instead of scaffolding from scratch.
- **Over-scaffolding:** No `src/`, `lib/`, `tests/`, `docs/` directories on day one. One file at the root until there's a reason for more.
- **Framework creep:** Don't add a framework where a script will do. A Bash script that runs is better than a Node CLI that doesn't yet.
- **Premature testing infra:** No Jest, Pytest, GitHub Actions, or pre-commit config in the first commit. Add them when the user needs them.
- **Heavy README:** No badges, no contribution guide, no roadmap. The first README is purpose, one usage example, install instructions if published. Three sections, ~30 lines.
- **Asking when you can act:** If the user said "scaffold a Bash log parser called `logsniff`," do not ask "what language?" — they already told you.

## When the language isn't obvious

If the user describes the *purpose* but not the language, infer:

- "Parse logs" / "automate something on this machine" / "wrap a CLI" → **Bash** by default, unless logic is complex enough that argument parsing alone would be painful.
- "Talk to an API" / "process JSON heavily" / "build a tool I'll publish on npm" → **Node**.
- "Data manipulation" / "anything with pandas, numpy, ML libs" / "interactive script" → **Python**.

Confirm the inference in one sentence before scaffolding: "This sounds like a Bash job — going with that unless you'd rather Node or Python." Then proceed unless the user redirects.
