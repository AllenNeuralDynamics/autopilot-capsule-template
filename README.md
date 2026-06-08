# claude-code-capsule

This is a base capsule for running an autonomous coding agent using Anthropic Claude Code in non-interactive mode.

The input is a prompt, the output is anything the agent generates, with no expectation of human intervention.

## Authentication
For direct Anthropic API usage, the capsule needs the `ANTHROPIC_API_KEY` secret to be set (try to run the capsule and you'll be prompted to add it).

See Anthropic's Console [here](https://console.anthropic.com/settings/keys) to create an API key, then see Code Ocean's docs [here](https://docs.codeocean.com/user-guide/compute-capsule-basics/secret-management-guide/adding-editing-a-secret-in-the-account-settings-page#adding-a-new-secret) on how to add it to your Code Ocean account as a "Custom Key".

To use Amazon Bedrock instead, set `use-bedrock` to `1` in the App Panel/API. The runner will export `CLAUDE_CODE_USE_BEDROCK=1`; configure AWS credentials and `AWS_REGION` separately in the capsule environment.

## Defaults for development
The App Panel model, effort, and max-budget-usd fields are optional. Leaving them blank will use Claude Code's defaults (or any config file it finds in `CLAUDE_CONFIG_DIR`).

The capsule is set up for development first: it's easy to burn through tokens while just testing your data, utility functions, prompts, skills etc. so the default model is set to the cheap and cheerful `claude-haiku-4.5`. Just keep in mind that tool calling, context window size and basic ability to follow instructions and fix problems will be significantly worse than `opus` or `sonnet`. `claude-sonnet-4.6` is Copilot's default and is almost certainly the best bang for your buck if you want to launch many of these agents.

## Notes
`code/.agents` and `code/CLAUDE.md` are copied to `results/.claude` and used as the run's `CLAUDE_CONFIG_DIR`.

A Code Ocean "skill" is bundled which *should* guide the agent on the conventions for working in a Reproducible Run (e.g. writing to `results/`).

`CLAUDE.md` can be used for other general rules that you want the agent to follow regardless of the prompt: coding style, tools to use, etc.


## References
Claude Code docs: https://code.claude.com/docs/en
