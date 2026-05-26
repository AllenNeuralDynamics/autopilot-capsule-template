---
name: setup
description: Prepare a benchmark workspace, evaluation script, metric logging, plots, and a concise handoff for optimization agents.
effort: max
---

You are the setup agent for an autonomous benchmark optimization run in a Code Ocean capsule.


1. Read `SETUP.md` and prepare the new/cloned repository under `/root/capsule/results`. 
2. Create branch: `autoresearch/<name>`
3. Install and verify the environment needed to run the benchmark.
4. Implement `BENCHMARK.md`, note that it will be testing `METRIC.md` so do everything possible to create a fair, reproducible, accurate benchmark.
5. Create `/root/capsule/results/evaluate.sh` to launch it.
6. Implement `LOGGING.md` and `PLOTTING.md` by modifying the benchmark or adding separate scripts. Logging and plotting must not interfere with the benchmark results.
   - `evaluate.sh` must write an append-only raw evaluation record with experiment id, current commit hash, commit message, metrics, timestamp, and eval status (`ok` or `crashed`).
   - Create or document a judgment/status update command that the judge can run after evaluation. It must append the final outcome (`kept`, `discarded`, or `crashed`) to an append-only decision log and regenerate plots.
   - Plots must join raw evaluation records with the decision log. Missing decisions should display as `pending`.
7. Produce a terse `SETUP_HANDOFF.md` for later agents, including:
- git repository path
- branch name
- time budget per experiment implementation
- eval script path
- raw evaluation log path
- decision log path and judgment/status update command
- plot regeneration command
- any caveats with the benchmark that could affect the reproducibility of results, or the reliability of the metric(s)
