---
name: concise
description: Use when implementing a feature or running an analysis and the deliverable should stay lean — before writing code, reports, or the final summary. Counters scope creep, bloated reports, and unasked extras.
---

# Concise Delivery

## Overview

Rigor goes into decisions; brevity goes into everything written. The deliverable matches the request's scope exactly — depth of verification stays, packaging shrinks.

## The Contract

Every deliverable has this shape:

**Scope.** The implementation contains exactly the requested features and outputs. An idea beyond scope becomes one proposal line at the end of the final message ("Worth adding: …"), never an implementation. This includes styling, extra endpoints, extra config, and tests for behavior nobody asked about.

**Reports and documents.** A findings document is three parts, in order:
1. Each finding as a bold one-liner followed by 1-3 sentences of evidence — the key number that supports it, not the procedure that produced it.
2. Decisions taken on the data/code and the one-line reason.
3. Recommendations, if any, as a short list.

Target: fits on one screen (~60 lines). One section per topic — a fact appears once. Executive summaries, numbered subsections, and methodology sections belong to documents the user explicitly requested at that depth.

**Analysis code.** One linear script computing the requested metrics. When a destructive decision needs verification (deduplication, dropping rows, correcting values), run the check, act on it, and record the result as a one-line comment at the decision point.

**Final message.** In order:
1. Outcome in 2-3 sentences: what works, what was found, what was verified.
2. Only the details that change what the reader does next.
3. The minimum commands to run/verify it.

## Quick Reference

| Situation | Do |
|---|---|
| Tempted to add a feature/style/endpoint | One proposal line at the end instead |
| Statistical check made a decision | Report conclusion + key number, once |
| Report growing past one screen | Merge sections; a fact appears once |
| Unsure how deep the report should go | The shape above; user asks if they want more |

## Common Mistakes

- **Depth in the wrong place:** running a rigorous check (good) and then writing a methodology section about it (bloat). The check earns one line.
- **Restating findings:** same fact in summary, section body, and conclusions. Pick the section it belongs to.
- **"While I'm here" tests:** tests cover requested behavior and its failure modes, not features that don't exist.
