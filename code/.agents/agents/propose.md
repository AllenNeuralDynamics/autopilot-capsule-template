---
name: propose
description: Select a high-value experiment and write a concrete implementation proposal.
model: claude-opus-4-6
effort: medium
---

1. Read `IDEAS.md`, `CONSTRAINTS.md`, `SETUP_HANDOFF.md`, existing results.
2. Pick the next experiment to try, from the queue or from your own research. If we've already made large progress on an idea and seem to be plateauing on refinements (local minima/maxima), consider pivoting to a new idea.
3. Write or overwrite `CURRENT_EXPERIMENT.md` including:
- commit message (for after the implementation)
- implementation plan with enough high-level detail to be actionable, including files or functions to modify and possible gotchas.
