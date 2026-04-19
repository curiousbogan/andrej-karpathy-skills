---
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes. Covers thinking before coding, simplicity, surgical changes, goal-driven execution, plus Windows/Railway environment gotchas and project context.
license: MIT
---

# Karpathy Guidelines (Customized)

Behavioral guidelines to reduce common LLM coding mistakes, derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876) and customized for this workspace.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

## 5. Platform & Environment

**Windows + Git Bash has sharp edges. Know them.**

- Git Bash silently converts Unix paths — use `MSYS_NO_PATHCONV=1` when passing Unix paths to CLI tools.
- Before any Railway CLI operation, run `railway status` to confirm linked project/service.
- Railway CLI timeouts are normal — retry before investigating.
- Each OpenClaw instance needs its own unique Telegram bot token.

## 6. Project Context

**Know the landscape before touching anything.**

- `sentinel-v2` — Python 3.12 FastAPI orchestrator (replaces Node.js legacy)
- `strategy-factbase` — OpenClaw with 4 agents (Ares/Scout/Nova/Atlas)
- `SentinalClawing` — Legacy production (being replaced)
- Check deployed services before assuming. Don't mix Node.js patterns into Python projects.
