# Karpathy-Inspired Claude Code Guidelines

> A single `CLAUDE.md` — and a proper Claude Code plugin — that fixes how AI coding agents behave.  
> Derived from Andrej Karpathy's observations on LLM coding pitfalls.

---

## Why This Exists

On January 26, 2026, Karpathy described what he found after switching from 80% manual coding to 80% agent-driven coding:

> *"The models make wrong assumptions on your behalf and just run along with them without checking. They don't manage their confusion, don't seek clarifications, don't surface inconsistencies, don't present tradeoffs, don't push back when they should."*

> *"They really like to overcomplicate code and APIs, bloat abstractions... implement a bloated construction over 1000 lines when 100 would do."*

> *"They still sometimes change/remove comments and code they don't sufficiently understand as side effects, even if orthogonal to the task."*

This repo turns those observations into six enforceable principles.

---

## The Six Principles

| # | Principle | Fixes |
|---|---|---|
| 1 | **Think Before Coding** | Silent assumptions, missing clarification, hidden confusion |
| 2 | **Simplicity First** | Overengineering, premature abstraction, bloated PRs |
| 3 | **Surgical Changes** | Drive-by refactoring, style drift, touching unrelated code |
| 4 | **Goal-Driven Execution** | Vague tasks, no success criteria, unclear done state |
| 5 | **Reproduce Before Fixing** | Blind patches, no test coverage, hidden regressions |
| 6 | **Communicate Tradeoffs** | Silent architecture decisions, no alternatives surfaced |

---

## Karpathy's Core Insight

> *"LLMs are exceptionally good at looping until they meet specific goals... Don't tell it what to do, give it success criteria and watch it go."*

Principle 4 (Goal-Driven Execution) operationalizes this: transform every task from an imperative instruction into a verifiable goal with a defined done state.

---

## Install

### Option A — Per Project (fastest)

```bash
# New project
curl -o CLAUDE.md https://raw.githubusercontent.com/BurukalaManiReethika/Karpathy-Inspired-Claude-Code-Guidelines/main/CLAUDE.md

# Existing project (append)
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/BurukalaManiReethika/Karpathy-Inspired-Claude-Code-Guidelines/main/CLAUDE.md >> CLAUDE.md
```

Claude Code reads `CLAUDE.md` automatically at session start. No other setup needed.

### Option B — Claude Code Plugin (all projects)

```
/plugin marketplace add BurukalaManiReethika/Karpathy-Inspired-Claude-Code-Guidelines
/plugin install karpathy-code-guidelines@karpathy-guidelines
```

This installs the skill globally — available in every project without a local `CLAUDE.md`.

---

## Repo Structure

```
CLAUDE.md                              ← Drop this in your project root
README.md                              ← This file
Example                                ← Before/after code for all 6 principles
skills/
  karpathy-guidelines/
    SKILL.md                           ← Full skill loaded by Claude Code plugin system
.claude-plugin/
  plugin.json                          ← Plugin metadata (name, version, author, source)
  marketplace.json                     ← Marketplace listing definition
```

---

## How to Know It's Working

- **Clarifying questions come before implementation** — not after mistakes
- **Diffs are clean** — only lines that were asked to change, change
- **Code is simple the first time** — no rewrites due to overengineering
- **Bugs come with tests** — not blind patches
- **Architecture decisions are explained** — not silently chosen

---

## Customization

Add project-specific rules at the bottom of your `CLAUDE.md`:

```markdown
## Project-Specific Rules

- TypeScript strict mode — no `any`, use `unknown` and narrow it
- All API endpoints require integration tests before merge
- Follow error handling in `src/utils/errors.ts`
- Never use `console.log` — use the structured logger in `src/lib/logger.ts`
```

Global principles + local rules = agent that knows both the universal standards and your codebase's specific laws.

---

## Tradeoff Note

These guidelines bias toward **caution over speed**. For trivial tasks (typo fixes, obvious one-liners), full rigor is unnecessary overhead.

The target is non-trivial work — anything touching auth, payments, data integrity, APIs, or multi-file changes — where a wrong silent assumption can cost hours.

---

## License

MIT
