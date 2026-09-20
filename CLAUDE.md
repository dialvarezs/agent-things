# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

If the project has no CLAUDE.md but has an AGENTS.md, treat AGENTS.md as the CLAUDE.md.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- Remove imports/variables/functions that YOUR changes made unused. Leave pre-existing dead code; mention it.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan with a verify step per item.

## 5. Contain Test/Experiment Artifacts

Never scatter test output in `$HOME` root or the project tree. Scratch files go in the session scratchpad, or under `~/claude_experiments/<task>/` if they must persist or be exec-capable. Clean up when done, or tell the user where the artifacts are.

## 6. Token Economy

Context size per turn is the main cost: every message re-reads the whole context. Keep it small.

- Keep tool output short: pipe long commands through `head`, `tail`, `grep`, or `wc`. Never dump full logs, diffs, or big files into context. Read only the lines you need.
- Suggest `/compact` when context passes ~200k tokens, and `/clear` when the task changes.
- Subagents: pick the model by task, not by inheritance. `haiku` for search/read/summarize/run-a-command, `sonnet` for implementation against a clear spec, `opus` only for architecture, cross-file refactors, or ambiguous diagnosis. Use `Explore` for codebase searches instead of `general-purpose`. If the subagent's definition sets a model, leave it. `fork` always inherits the parent model.
- Ask subagents for a digest, never for raw file contents.
