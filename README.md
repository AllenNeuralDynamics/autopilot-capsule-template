# claude-code-capsule

This is a base capsule for running an autonomous coding agent using Anthropic Claude Code in non-interactive mode.

The input is a prompt, the output is anything the agent generates, with no expectation of human intervention.

## Authentication
For direct Anthropic API usage, the capsule needs the `ANTHROPIC_API_KEY` secret to be set (try to run the capsule and you'll be prompted to add it).

See Anthropic's Console [here](https://console.anthropic.com/settings/keys) to create an API key, then see Code Ocean's docs [here](https://docs.codeocean.com/user-guide/compute-capsule-basics/secret-management-guide/adding-editing-a-secret-in-the-account-settings-page#adding-a-new-secret) on how to add it to your Code Ocean account as a "Custom Key".

To use Amazon Bedrock instead, set `use-bedrock` to `1` in the App Panel/API. The runner will export `CLAUDE_CODE_USE_BEDROCK=1`; configure AWS credentials and `AWS_REGION` separately in the capsule environment.

## Defaults for development
The App Panel model and effort fields are optional. Leave them blank to use the Claude Code defaults or config, or set them explicitly when you want repeatable model and reasoning-depth selection for a run.

## Config
The entrypoint is [code/run](code/run). It uses `results/.claude` as the run's `CLAUDE_CONFIG_DIR`, installs the bundled Code Ocean skill there, copies `CLAUDE.md` into the agent workspace, and launches:

```bash
claude --dangerously-skip-permissions -p
```

The dangerous skip-permissions flag is intended for this externally sandboxed Code Ocean environment. Do not reuse it on a normal workstation unless you understand the risk.

A Code Ocean "skill" is bundled which *should* guide the agent on the conventions for working in a Reproducible Run (e.g. writing to `results/`).

`CLAUDE.md` can be used for other general rules that you want the agent to follow regardless of the prompt: coding style, tools to use, etc.


## References
Claude Code docs: https://code.claude.com/docs/en
