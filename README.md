# Karpathy-Inspired Claude Code Guidelines

> A single `CLAUDE.md` file that fixes how Claude Code behaves — derived from Andrej Karpathy's observations on LLM coding pitfalls.

---

## The Problem

Karpathy put it plainly:

> *"The models make wrong assumptions on your behalf and just run along with them without checking. They don't manage their confusion, don't seek clarifications, don't surface inconsistencies, don't present tradeoffs, don't push back when they should."*

> *"They really like to overcomplicate code and APIs, bloat abstractions... implement a bloated construction over 1000 lines when 100 would do."*

> *"They still sometimes change/remove comments and code they don't sufficiently understand as side effects, even if orthogonal to the task."*

These aren't edge cases. They're the default behavior.

---

## The Solution

Six principles in one `CLAUDE.md` file — placed in your project root, read automatically by Claude Code.

| Principle | What It Fixes |
|---|---|
| **Think Before Coding** | Silent assumptions, hidden confusion, skipped tradeoffs |
| **Simplicity First** | Overengineering, premature abstraction, bloated PRs |
| **Surgical Changes** | Drive-by refactoring, style drift, touching unrelated code |
| **Goal-Driven Execution** | Vague tasks, no success criteria, unclear done state |
| **Reproduce Before Fixing** | Patches without confirmation, no regression safety |
| **Communicate Tradeoffs** | Silent architecture decisions, no alternatives surfaced |

---

## The Six Principles

### 1. Think Before Coding
State assumptions explicitly. If a request has multiple interpretations, list them. Ask before implementing — not after making mistakes. If something is unclear mid-task, stop and name it.

### 2. Simplicity First
Write the minimum code that solves the problem. No speculative features, no abstractions for a single use case, no "configurability" that wasn't asked for. If 200 lines could be 50, rewrite it.

### 3. Surgical Changes
Touch only what the task requires. Match existing code style — even if you'd do it differently. Mention pre-existing dead code, don't silently delete it. Clean up only what your changes create.

### 4. Goal-Driven Execution
Transform "fix the bug" into "write a test that reproduces it, then make it pass." Give Claude verifiable success criteria and it can loop to completion on its own.

### 5. Reproduce Before Fixing
Write a failing test first. Confirm the bug exists. Fix. Confirm the test passes. Run the full suite. Never patch a bug you haven't reproduced.

### 6. Communicate Tradeoffs
When multiple approaches exist, briefly surface them — what each optimizes, what it sacrifices, and your recommendation. 3–5 lines. Not an essay.

---

## Key Insight

From Karpathy:

> *"LLMs are exceptionally good at looping until they meet specific goals... Don't tell it what to do, give it success criteria and watch it go."*

The upgrade from "do X" to "success looks like Y, loop until you get there" is the highest-leverage change you can make.

---

## Install

**Option A — Per-project (recommended)**

```bash
# New project
curl -o CLAUDE.md https://raw.githubusercontent.com/BurukalaManiReethika/Karpathy-Inspired-Claude-Code-Guidelines/main/CLAUDE.md

# Existing project (append)
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/BurukalaManiReethika/Karpathy-Inspired-Claude-Code-Guidelines/main/CLAUDE.md >> CLAUDE.md
```

**Option B — Claude Code Plugin**

```
/plugin marketplace add forrestchang/andrej-karpathy-skills
/plugin install andrej-karpathy-skills@karpathy-skills
```

---

## Customization

These guidelines are designed to be merged with your own project rules. Add a section at the bottom of `CLAUDE.md`:

```markdown
## Project-Specific Guidelines

- Use TypeScript strict mode
- All API endpoints must have integration tests
- Follow error handling patterns in `src/utils/errors.ts`
- Never use `any` type — use `unknown` and narrow it
```

---

## How to Know It's Working

- **Fewer unnecessary diff lines** — only requested changes appear
- **Clarifying questions before implementation** — not after mistakes
- **Simpler code the first time** — no rewrites due to overengineering
- **Clean, focused PRs** — no drive-by refactoring
- **Bugs fixed with tests** — not blind patches

---

## Files

```
CLAUDE.md          ← Drop this in your project root
README.md          ← This file
Example            ← Real before/after code examples for all 6 principles
.claude-plugin/    ← Plugin definition for Claude Code marketplace
```

---

## License

MIT
