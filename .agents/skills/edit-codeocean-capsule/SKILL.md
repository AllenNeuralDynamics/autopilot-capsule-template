---
name: edit-codeocean-capsule
description: Use this skill when writing code for a Code Ocean capsule, or when running within a capsule environment (CO_COMPUTATION_ID exists).
user-invocable: false
---

# Capsule editing for agents
## Paths

| Purpose | Path | Storage |
|---------|------|---------|
| outputs of Reproducible Runs: figures, tables, reports, data, code | `/root/capsule/results/` | Unlimited |
| large or temporary files, app caches, downloads, extracted archives | `/root/capsule/scratch/` | Unlimited |
| code used during Reproducible Runs | `/root/capsule/code/` | 5 GB capsule limit applies |
| read-only data assets, user uploads, artifacts | `/root/capsule/data/` | 5 GB capsule limit applies |

## Capsule modes
Identify which mode this environment is running in:
```bash
[ -z "${TERM+x}" ] || [ "$TERM" = "dumb" ] && echo reproducible-run || echo interactive
```
### reproducible-run
- only outputs written to `results` will be captured at exit for the user to inspect

### interactive (ignore if in reproducible-run)
- a user is probably steering
- editing `code` and `data` is allowed
- `code/run` is the entry point for Reproducible Runs
- the user may want to write to directories other than those listed above - just be aware of the 5 GB capsule limit

## Guidelines
- create subdirectories within `results` to stay organized (e.g. `results/figures`).
- use absolute paths for clarity

## Gotchas
- the CPUs reported by the system will usually be incorrect: the environment variable `CO_CPUS` gives the correct number, if it exists; otherwise, fallback to the system count:
  ```bash
  NPROC="${CO_CPUS:-$(nproc)}"
  ```
- linux capsules usually run as root by default; `sudo` may not be installed (or necessary)

## Code Patterns

### Python
- if the `conda` base environment is available it is activated by default and should be used; otherwise, install and use `uv`:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
export PATH="/root/.local/bin:$PATH"
export UV_CACHE_DIR=/root/capsule/scratch/.cache
```

```python
import os
from pathlib import Path

RESULTS_DIR = Path("/root/capsule/results")
SCRATCH_DIR = Path("/root/capsule/scratch")

## Save outputs
fig.savefig(RESULTS_DIR / "figure1.png", dpi=300)
df.to_csv(RESULTS_DIR / "summary.csv", index=False)

## Scratch for intermediates
cache_path = SCRATCH_DIR / "model_checkpoint.pt"
```

## R
```r
results_dir <- "/root/capsule/results"
scratch_dir <- "/root/capsule/scratch"

## Save outputs
ggsave(file.path(results_dir, "figure1.png"), plot = p, width = 8, height = 6)
write.csv(df, file.path(results_dir, "summary.csv"), row.names = FALSE)
```

## Bash (code/run)
```
#!/usr/bin/env bash
set -ex

## This is the master script for the capsule. When you click "Reproducible Run", the code in this file will execute.
python -u run_capsule.py "$@"
```
