# autopilot-capsule

This is a base capsule for running an autonomous coding agent using GitHub Copilot CLI's autopilot mode. 

The input is a prompt, the output is anything the agent generates, with no expectation of human intervention.

As an agent, Copilot may not be as good as Claude Code or Codex, but it can be authenticated easily with GitHub credentials to use the request allowance included in our org plan. It also has access to different model vendors.

## Authentication
The capsule just needs the `COPILOT_GITHUB_TOKEN` secret to be set (try to run the capsule and you'll be prompted to add it).

See GitHub's docs [here](https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/authenticate-copilot-cli#authenticating-with-environment-variables) on how to generate a token, then see Code Ocean's docs [here](https://docs.codeocean.com/user-guide/compute-capsule-basics/secret-management-guide/adding-editing-a-secret-in-the-account-settings-page#adding-a-new-secret) on how to add it to your Code Ocean account as a "Custom Key".

## Defaults for development
The capsule is set up for development first: it's easy to burn through premium requests while just testing your data, utility functions, prompts, skills etc. so the default model is set to the cheap and cheerful `claude-haiku-4.5` (0.33x at the time of writing). Just keep in mind that code generation, tool calling, context window size and basic ability to follow instructions will be significantly worse than flagship models like `claude-opus-4.6` or `gpt-5.5`. `claude-sonnet-4.6` is Copilot's default and is almost certainly the best bang for your buck if you want to launch many of these agents.

## Config
When you've finished developing, you can set the model you want in [code/.copilot/settings.json](code/.copilot/settings.json), which is currently the only way to set the "effort" level, and run the capsule with the model field blank. The effort levels are different across models - open a terminal and run `copilot` to explore the options.

Setting `model` via the App Panel/API always overrides `.copilot/settings.json` (and uses the models default effort).

`max-autopilot-continues` is a safety measure to prevent run-away agent loops that could burn through your request allowance in one go. It's 0 by default which means "carry out the prompt, and if it will cost more than 1 premium request, stop". This is fine for development and a lot of real tasks. If you want the agent to keep working in a loop (e.g. optimizing a metric until you stop the capsule), you'll need to increase this. More info [here](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/autopilot#things-to-consider). 

A Code Ocean "skill" is bundled which *should* guide the agent on the conventions for working in a Reproducible Run (e.g. writing to `results/`).

`AGENTS.md` can be used for other general rules that you want the agent to follow regardless of the prompt: coding style, tools to use, etc.


## References
Comparing autopilot mode, `--allow-all`, and `--no-ask-user`: https://docs.github.com/en/copilot/concepts/agents/copilot-cli/autopilot#comparing-autopilot-mode---allow-all-and---no-ask-user

Command reference:
https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference
