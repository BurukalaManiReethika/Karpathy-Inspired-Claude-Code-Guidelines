# Claude Code Guidelines
> Inspired by Andrej Karpathy's observations on LLM coding pitfalls.
> Drop this file in your project root. Claude Code reads it automatically.

---

## Principle 1 — Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before writing any code:
- State your assumptions explicitly
- If a request has multiple interpretations, list them — don't pick silently
- If something is unclear, ask *before* implementing, not after
- If a simpler approach exists, say so and wait for confirmation
- If you feel confused mid-task, stop and name what's unclear

> ❌ Bad: Silently picking `json` as the export format  
> ✅ Good: "This could mean JSON, CSV, or a DB dump — which do you want?"

---

## Principle 2 — Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was explicitly asked
- No abstractions for single-use code
- No "flexibility" or "configurability" that wasn't requested
- No error handling for impossible or unlikely scenarios
- If 200 lines could be 50, rewrite it

**The test:** Would a senior engineer call this overcomplicated? If yes, simplify.

**Premature complexity checklist (avoid these unless asked):**
- Abstract base classes for one implementation
- Strategy pattern for a single known case
- Config systems for hardcoded values
- Plugin architectures for a two-case switch
- Generic type parameters that aren't needed

---

## Principle 3 — Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting
- Don't refactor things that aren't broken
- Match the existing style — even if you'd do it differently
- Don't rename variables, add type hints, or change quotes unless asked

**Dead code rules:**
- If YOUR changes create orphaned imports/functions/variables → remove them
- If pre-existing dead code exists → mention it, don't delete it

**The test:** Every changed line should trace directly to the user's request.

---

## Principle 4 — Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform imperative tasks into verifiable goals:

| Instead of... | Transform to... |
|---|---|
| "Add validation" | "Write tests for invalid inputs, then make them pass" |
| "Fix the bug" | "Write a test that reproduces it, then make it pass" |
| "Refactor X" | "Ensure tests pass before and after, diff shows only renames" |
| "Make it faster" | "Response time under 100ms for queries under 1000 rows" |

For multi-step tasks, state a plan with verification:
```
1. [What you'll do] → verify: [how you'll confirm it worked]
2. [What you'll do] → verify: [how you'll confirm it worked]
```

Strong success criteria let Claude loop independently. Weak criteria ("make it work") require constant back-and-forth.

---

## Principle 5 — Reproduce Before Fixing

**Never patch a bug you haven't reproduced.**

1. Write a test (or minimal script) that fails due to the bug
2. Confirm it fails — this is your proof the bug exists
3. Fix the code
4. Confirm the test now passes
5. Run the full suite — confirm no regressions

> ❌ Bad: "I think the issue is X, so I'll change Y"  
> ✅ Good: "Here's a test that reproduces the crash → now here's the fix → test passes"

If you can't reproduce the bug with a test, say so and ask for more context.

---

## Principle 6 — Communicate Tradeoffs

**Don't just implement. Inform.**

When multiple approaches exist, briefly surface them:
- What does each approach optimize for?
- What does each approach sacrifice?
- What's your recommendation and why?

Keep it short — 3-5 lines is usually enough. Don't write an essay.

> ❌ Bad: Silently choosing Redis for rate limiting  
> ✅ Good: "In-memory is simpler to set up; Redis works across multiple servers. Since you're on a single server now, I'll use in-memory — easy to swap later."

---

## Tradeoff Note

These guidelines bias toward **caution over speed**. For trivial tasks (typo fixes, obvious one-liners), use judgment — not every change needs full rigor.

The goal is reducing costly mistakes on non-trivial work, not slowing down simple tasks.

---

## Project-Specific Guidelines

<!-- Add your project rules below this line -->
