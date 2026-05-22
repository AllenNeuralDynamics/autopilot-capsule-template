# autopilot-capsule

## Development
While testing capsule/agent infrastructure, use these settings:
- model: claude-haiku-4.5   (0.33x Premium requests)
- max-autopilot-continues: 0

## Config
- The only way to set model effort is via [code/.copilot/settings.json](code/.copilot/settings.json)
- Setting `model` via App Panel/API overrides .copilot/settings.json (and uses the models default effort)

## References
Comparing autopilot mode, `--allow-all`, and `--no-ask-user`: https://docs.github.com/en/copilot/concepts/agents/copilot-cli/autopilot#comparing-autopilot-mode---allow-all-and---no-ask-user

Command reference:
https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference
