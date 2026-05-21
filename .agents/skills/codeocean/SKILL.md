---
name: codeocean
description: Use this skill when the env var CO_CAPSULE_ID exists, indicating that we're running in a Code Ocean capsule or from within a reproducible run (CO_COMPUTATION_ID exists). Also use this skill when the user's prompt requires editing code in a Code Ocean capsule.
user-invocable: false
---

# Code Ocean 

## Paths

| Purpose | Path | Storage | Notes |
|---------|------|---------|-------|
| **Outputs** (figures, tables, reports, data) | `/root/capsule/results/` | Unlimited | This is what Code Ocean captures as a "result". The user can only see outputs that are saved here. |
| **Scratch / temp artifacts** (large intermediate files, caches, downloads) | `/root/capsule/scratch/` | Unlimited | Cleared at capsule exit. Changes cannot be seen by user. |
| **Source code** | `/root/capsule/code/` | 5 GB limit applies. Changes cannot be seen by user |
| **Input data** (read-only) | `/root/capsule/data/` | |

## Rules

1. **Never write outputs to `/root/capsule/code/` or relative paths** — always use absolute `/root/capsule/results/` for anything that should be captured.
2. **Use `/root/capsule/scratch/` for large intermediates**: model checkpoints during training, downloaded archives, extracted files, intermediate CSVs, cache dirs, temp images before compositing, etc.
3. **Create subdirectories** within `results/` to stay organized (e.g. `results/figures/`).
4. **Never hardcode the user's home directory** or assume a working directory — use the absolute paths above.

## Code Patterns

### Python
```python
import os
from pathlib import Path

RESULTS_DIR = Path("/root/capsule/results")
SCRATCH_DIR = Path("/root/capsule/scratch")

# Save outputs
fig.savefig(RESULTS_DIR / "figure1.png", dpi=300)
df.to_csv(RESULTS_DIR / "summary.csv", index=False)

# Scratch for intermediates
cache_path = SCRATCH_DIR / "model_checkpoint.pt"
```

### R
```r
results_dir <- "/root/capsule/results"
scratch_dir <- "/root/capsule/scratch"

# Save outputs
ggsave(file.path(results_dir, "figure1.png"), plot = p, width = 8, height = 6)
write.csv(df, file.path(results_dir, "summary.csv"), row.names = FALSE)
```

### Bash (code/run)
```bash
#!/usr/bin/env bash
set -euo pipefail

# Run analysis
python /root/capsule/code/analysis.py
```

## Common Mistakes to Avoid (Gotchas)

- `./output/` or `output/` — wrong, use `/root/capsule/results/`
- `~/results/` — wrong, use absolute path
- Saving large intermediate files to `/root/capsule/code/` — use `/root/capsule/scratch/`
- Writing to `/root/capsule/data/` — read-only
- Using `tempfile` or `/tmp` for anything you want to inspect after a run — use `/root/capsule/scratch/` instead
- the CPUs reported by the system will usually be incorrect: the environment variable `CO_CPUS` gives the correct number, if it exists; otherwise, fallback to the system count:
  ```bash
  NPROC="${CO_CPUS:-$(nproc)}"
  ```
- the Docker container runs as root by default; `sudo` is usually not installed (or neccessary)
