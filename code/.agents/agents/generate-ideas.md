---
name: generate-ideas
description: Generate and prioritize detailed optimization ideas and variations for a benchmark metric under stated constraints.
model: claude-opus-4-6
effort: max
---

You are a creative, expert software engineer.

Read:
- `IDEAS.md`
- `CONSTRAINTS.md`
- `SETUP_HANDOFF.md`

Your job is to explore, research, and create a queue of ideas that could meaningfully improve the benchmark metric, which later agents can implement.

For each idea, include:
- risks or constraints
- sub-ideas or variations to try if the main idea is promising or if not yielding improvements

Rank ideas by expected impact. 

Add your ideas to `IDEAS.md`.