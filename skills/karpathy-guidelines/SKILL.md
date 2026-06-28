---
name: karpathy-guidelines
description: Six principles for better Claude Code behavior — think before coding, keep it simple, make surgical changes, define success criteria, reproduce bugs before fixing, and surface tradeoffs. Derived from Andrej Karpathy's observations on LLM coding pitfalls.
---

# Karpathy Code Guidelines

Apply these six principles to every coding task. They exist to prevent the most common and costly LLM coding failures.

---

## Principle 1 — Think Before Coding

Before writing any code:

- State your assumptions explicitly
- If a request has multiple valid interpretations, list them — never pick one silently
- Ask for clarification before implementing, not after making mistakes
- If a simpler approach exists, say so and wait for confirmation
- If you feel confused mid-task, stop and name what's unclear

**Examples of what to say:**
- "This could mean X or Y — which do you want?"
- "I'm assuming [Z] — is that right before I proceed?"
- "There's a simpler way to do this: [approach]. Want me to go that route instead?"

---

## Principle 2 — Simplicity First

Write the minimum code that solves today's problem. Nothing speculative.

**Never add, unless explicitly asked:**
- Abstract base classes for a single known implementation
- Strategy/Factory patterns for one case
- Configuration systems for hardcoded values
- Caching before a performance problem is measured
- Validation before bad data appears
- Notifications, events, or hooks that weren't requested

**The test:** Would a senior engineer call this overcomplicated? If yes, simplify.

If 200 lines could be 50, rewrite it.

---

## Principle 3 — Surgical Changes

Touch only what the task requires.

**When editing existing code:**
- Don't "improve" adjacent code, comments, or formatting
- Don't refactor things that aren't broken
- Match the existing code style — even if you'd do it differently
- Don't rename variables, add type hints, or change quote style unless asked

**Dead code rules:**
- If YOUR changes create orphaned imports, functions, or variables → remove them
- If pre-existing dead code exists → mention it in a comment, don't delete it

**The test:** Every changed line must trace directly to the user's request.

---

## Principle 4 — Goal-Driven Execution

Transform imperative tasks into verifiable goals before starting.

| Instead of | Transform to |
|---|---|
| "Add validation" | "Write tests for invalid inputs, make them pass" |
| "Fix the bug" | "Write a test that reproduces it, make it pass" |
| "Refactor X" | "Ensure tests pass before and after, diff shows only renames" |
| "Make it faster" | "Response under 100ms for queries under 1000 rows" |

For multi-step tasks, state a plan with verification:
```
1. [Action] → verify: [specific check]
2. [Action] → verify: [specific check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant back-and-forth.

---

## Principle 5 — Reproduce Before Fixing

Never patch a bug you haven't confirmed exists.

**Always follow this sequence:**
1. Write a failing test (or minimal script) that reproduces the bug
2. Confirm it fails — this proves the bug is real
3. Fix the code
4. Confirm the test now passes
5. Run the full test suite — confirm no regressions

If you cannot reproduce the bug, say so and ask for more context rather than guessing at a fix.

---

## Principle 6 — Communicate Tradeoffs

When multiple implementation approaches exist, briefly surface them before choosing.

**Cover:**
- What each approach optimizes for
- What each approach sacrifices
- Your recommendation and why (1 sentence)

Keep it to 3–5 lines. Not an essay.

**Example:**
```
Two options:
- In-memory: simpler, zero deps, resets on restart
- Redis: survives restarts, works across instances, needs infra

Since you're on a single server, I'll use in-memory — easy to swap later.
```

---

## When These Principles Apply

**Full rigor required:** Any task touching auth, payments, data integrity, migrations, APIs, or multi-file refactors.

**Use judgment:** Trivial tasks (typo fixes, obvious one-liners, variable renames) don't need full ceremony.

The goal is preventing costly mistakes on non-trivial work — not slowing down simple tasks.
