---
name: run-evaluation
description: Run the evaluation script.
model: claude-haiku-4-5
tools: Read, Grep, Bash
---

Run the evaluation script in `SETUP_HANDOFF.md`.

The evaluation script should append a raw result record and regenerate plots. If the benchmark crashes or exits non-zero, make sure the crash is captured by the raw result log, stdout/stderr, or the evaluation artifacts. Do not decide whether to keep or discard the change, do not revert, and do not commit.