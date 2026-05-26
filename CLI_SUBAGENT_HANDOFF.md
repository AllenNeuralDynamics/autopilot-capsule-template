- **Scope**
  - Claude Code
  - GitHub Copilot CLI
  - Codex CLI

| Question | Claude Code | GitHub Copilot CLI | Codex CLI |
|---|---|---|---|
| JSON subagent config | Yes, inline with `--agents` | No | No |
| Persistent subagent config format | Markdown + YAML frontmatter | Markdown + YAML frontmatter | TOML |
| Select named agent on CLI | Yes, `--agent` | Yes, `--agent` | No documented flag |
| Run named agent with prompt | Yes | Yes | Prompt Codex to spawn/use agent |
| Per-agent model | Yes | Yes | Yes |
| Per-agent effort | Yes | No documented per-agent field | Yes |
| CLI system prompt override | Yes | No documented direct override | Yes, via config override |

- **Claude Code**
  - Persistent agents:
    - `~/.claude/agents/`
    - `.claude/agents/`
  - Dynamic JSON agents:
    - `--agents`
  - Named agent invocation:
    - `claude --agent name "prompt"`
    - `claude --agent name -p "prompt"`
  - System prompt override:
    - `--system-prompt`
    - `--system-prompt-file`
    - `--append-system-prompt`
    - `--append-system-prompt-file`
  - Agent settings:
    - `name`
    - `description`
    - `tools`
    - `disallowedTools`
    - `model`
    - `permissionMode`
    - `maxTurns`
    - `skills`
    - `mcpServers`
    - `hooks`
    - `memory`
    - `background`
    - `effort`
    - `isolation`
    - `color`
    - `initialPrompt`
  - System prompt behavior:
    - Named subagent does not get full regular Claude Code system prompt.
    - Named subagent gets its own custom prompt plus Claude Code-added environment context.
    - Named subagent still gets memory/project context such as `CLAUDE.md`, except Explore/Plan mode caveats.
    - Forked subagent inherits parent system prompt, tools, and history.

| Claude Code effort | Notes |
|---|---|
| `low` | Model-dependent |
| `medium` | Model-dependent |
| `high` | Model-dependent |
| `xhigh` | Model-dependent |
| `max` | Model-dependent |

- **GitHub Copilot CLI**
  - Persistent agents:
    - `.github/agents/`
    - `.claude/agents/`
    - `~/.copilot/agents/`
    - plugin agent directories
  - Dynamic JSON agents:
    - Not documented
  - Named agent invocation:
    - `copilot --agent name --prompt "..."`
    - `copilot -p "..." --agent name`
  - System prompt override:
    - No documented `--system-prompt` equivalent
    - Supports custom instruction files
    - Supports `--no-custom-instructions`
  - Agent settings:
    - `name`
    - `description`
    - `infer`
    - `mcp-servers`
    - `model`
    - `tools`
  - System prompt behavior:
    - Hidden/base prompt layering is not documented.
    - Custom agent Markdown body supplies behavior/instructions.
    - Custom instructions are automatically added unless disabled.
    - Do not assume custom agents replace Copilot's hidden base prompt.

| GitHub Copilot CLI effort | Notes |
|---|---|
| CLI/session effort | Supported via `--effort` / `--reasoning-effort` |
| Per-agent effort | No documented field |

- **Codex CLI**
  - Persistent agents:
    - `~/.codex/agents/`
    - `.codex/agents/`
  - Config format:
    - TOML
  - Dynamic JSON agents:
    - Not documented
  - Named agent invocation:
    - No documented `--agent` equivalent
    - Ask Codex in the prompt to spawn/use an agent by name
  - System prompt override:
    - No dedicated `--system-prompt` flag
    - `-c model_instructions_file=/path/to/file`
    - `-c developer_instructions='...'`
  - Agent settings:
    - `name`
    - `description`
    - `developer_instructions`
    - `nickname_candidates`
    - `model`
    - `model_reasoning_effort`
    - `sandbox_mode`
    - `mcp_servers`
    - `skills.config`
  - System prompt behavior:
    - Custom agent usually keeps regular Codex built-in instructions.
    - `developer_instructions` adds agent-specific instructions.
    - `model_instructions_file` replaces built-in model instructions.

| Codex effort | Notes |
|---|---|
| `minimal` | Model-dependent |
| `low` | Model-dependent |
| `medium` | Model-dependent |
| `high` | Model-dependent |
| `xhigh` | Model-dependent |

- **Bottom line**
  - Best JSON subagent support:
    - Claude Code
  - Best command-line named-agent support:
    - Claude Code
    - GitHub Copilot CLI
  - Best per-agent model + effort support:
    - Claude Code
    - Codex CLI
  - Weakest system prompt override support:
    - GitHub Copilot CLI
  - Most explicit subagent system-prompt isolation:
    - Claude Code

- **Sources**
  - Claude Code CLI reference:
    - https://code.claude.com/docs/en/cli-reference
  - Claude Code subagents:
    - https://code.claude.com/docs/en/sub-agents
  - GitHub Copilot CLI command reference:
    - https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference
  - GitHub Copilot custom agents:
    - https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
  - GitHub Copilot custom agents configuration:
    - https://docs.github.com/en/copilot/reference/custom-agents-configuration
  - Codex CLI reference:
    - https://developers.openai.com/codex/cli/reference
  - Codex subagents:
    - https://developers.openai.com/codex/subagents
  - Codex config reference:
    - https://developers.openai.com/codex/config-reference
