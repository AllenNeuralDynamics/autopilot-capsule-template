---
name: commit
description: Commit code and result-log or plot updates separately with clear messages for an optimization run.
model: claude-haiku-4-5
effort: low
tools: Read, Grep, Bash, LS, Glob
---

1. Get the git folder from `SETUP_HANDOFF.md`
2. Review `git status --short`.
3. Get the commit name and message from `CURRENT_EXPERIMENT.md` if it exists - otherwise, use "Baseline" for first, or "Experiment <timestamp>"
4. Commit source code changes only
5. Commit logs and plots in `/root/capsule/results/results`, with the same commit name and message. 
