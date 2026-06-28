# Claude Code Guidelines
> Karpathy-Inspired · v2.0 · 6 Principles · Drop in project root

---

## 1 — Think Before Coding
Don't assume. Don't hide confusion. Surface tradeoffs.

- State assumptions explicitly before implementing
- List multiple interpretations — never pick one silently
- Ask before coding, not after mistakes
- Push back when a simpler approach exists
- Stop mid-task if confused — name what's unclear

---

## 2 — Simplicity First
Minimum code that solves today's problem. Nothing speculative.

- No features beyond what was asked
- No abstractions for a single use case
- No "flexibility" that wasn't requested
- No error handling for impossible scenarios
- If 200 lines could be 50 → rewrite it

**Avoid unless asked:** abstract base classes, strategy patterns, config systems, caching, plugin hooks, event buses.

---

## 3 — Surgical Changes
Touch only what the task requires.

- Don't improve adjacent code, comments, or formatting
- Don't refactor things that aren't broken
- Match existing style — even if you'd do it differently
- Mention pre-existing dead code — don't delete it
- Remove only what YOUR changes made orphaned

**Every changed line must trace directly to the request.**

---

## 4 — Goal-Driven Execution
Define success criteria. Loop until verified.

Transform tasks into verifiable goals:
- "Fix the bug" → "Write a test that reproduces it, make it pass"
- "Add validation" → "Write tests for invalid inputs, make them pass"
- "Refactor X" → "Tests pass before and after, diff shows only renames"

For multi-step work, state a plan:
```
1. [action] → verify: [check]
2. [action] → verify: [check]
```

---

## 5 — Reproduce Before Fixing
Never patch a bug you haven't confirmed.

1. Write a failing test that reproduces the bug
2. Confirm it fails (bug is real)
3. Fix the code
4. Confirm test passes
5. Run full suite — no regressions

If you can't reproduce → say so, ask for more context.

---

## 6 — Communicate Tradeoffs
Surface options briefly before choosing.

For any architectural decision, state:
- What each option optimizes
- What it sacrifices
- Your pick + one-line reason

3–5 lines max. Not an essay.

---

## Scope

**Full rigor:** auth, payments, data integrity, migrations, APIs, multi-file refactors.  
**Use judgment:** typo fixes, one-liners, obvious variable renames.

---

## Project-Specific Rules

<!-- Add your project rules below -->
