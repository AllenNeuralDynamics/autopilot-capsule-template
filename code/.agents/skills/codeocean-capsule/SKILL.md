---
name: codeocean-capsule
description: Always use when running within a Code Ocean capsule environment or reproducible run - check `env | grep -E "CO_COMPUTATION_ID"`. Also use this skill when writing any code for a Code Ocean capsule project - `.codeocean/` dir exists.
user-invocable: false
---

## Start here
If unclear, identify which mode this environment is running in `reproducible-run` or `interactive`:
```bash
[ -z "${TERM+x}" ] || [ "$TERM" = "dumb" ] && echo reproducible-run || echo interactive
```

### reproducible-run
- only write outputs for the user to `results` - anything else will be lost at exit.
- for reproducibility, always dump code that generated outputs to `results/code`.

### interactive (ignore if in reproducible run)
- a user is probably steering.
- only in interactive mode editing `code` and `data` is allowed - never in a reproducible run.
- `code/run` is the entry point for reproducible runs.
- the user may want to write to directories other than those listed below - just be aware of the 5 GB total capsule limit.

## Paths

| Purpose | Path | Storage |
|---------|------|---------|
| outputs of reproducible runs: figures, tables, reports, data, code | `results/` | Unlimited |
| large or temporary files, app caches, downloads, extracted archives | `scratch/` | Unlimited |
| code used during reproducible runs | `code/` | 5 GB capsule limit applies |
| read-only data assets, user uploads, artifacts | `data/` | 5 GB capsule limit applies |

## Guidelines
- create subdirectories within `results` to stay organized (e.g. `figures/`, `code/`).
- use absolute paths for clarity

## Gotchas
- the CPUs reported by the system will usually be incorrect: the environment variable `CO_CPUS` gives the correct number, if it exists; otherwise, fallback to the system count:
  ```bash
  NPROC="${CO_CPUS:-$(nproc)}"
  ```
- linux capsules usually run as root by default; `sudo` may not be installed (or necessary)

## Python
- if the `conda` base environment is available it is activated by default and should be used; otherwise, install and use `uv`:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
export PATH="/root/.local/bin:$PATH"
export UV_CACHE_DIR=/root/capsule/scratch/.cache
```
