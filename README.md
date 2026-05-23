# codex-capsule

This is a base capsule for running an autonomous coding agent using OpenAI Codex CLI in non-interactive mode.

The input is a prompt, the output is anything the agent generates, with no expectation of human intervention.

## Authentication
The capsule needs the `OPENAI_API_KEY` secret to be set (try to run the capsule and you'll be prompted to add it).

See OpenAI's docs [here](https://platform.openai.com/api-keys) on how to create an API key, then see Code Ocean's docs [here](https://docs.codeocean.com/user-guide/compute-capsule-basics/secret-management-guide/adding-editing-a-secret-in-the-account-settings-page#adding-a-new-secret) on how to add it to your Code Ocean account as a "Custom Key".

## Defaults for development
The App Panel model field is optional. Leave it blank to use the Codex CLI default, or set it explicitly when you want repeatable model selection for a run.

## Config
The entrypoint is [code/run](code/run). It uses `results/.agents` as the run's `CODEX_HOME`, installs the bundled Code Ocean skill there, copies `AGENTS.md` into the agent workspace, and launches:

```bash
codex exec --dangerously-bypass-approvals-and-sandbox
```

The dangerous bypass flag is intended for this externally sandboxed Code Ocean environment. Do not reuse it on a normal workstation unless you understand the risk.

A Code Ocean "skill" is bundled which *should* guide the agent on the conventions for working in a Reproducible Run (e.g. writing to `results/`).

`AGENTS.md` can be used for other general rules that you want the agent to follow regardless of the prompt: coding style, tools to use, etc.


## References
Codex CLI docs: https://developers.openai.com/codex/cli
