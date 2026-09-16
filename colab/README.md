# Claude Code in Google Colab

Run the Claude Code CLI and the Claude Agent SDK inside a Colab runtime, so Claude can read, write
and execute files on the VM instead of just returning text into a cell.

**[▶ Open the notebook in Colab](https://colab.research.google.com/github/alexbui96/alexbui96/blob/claude/claude-google-colab-60npvy/colab/claude_code_in_colab.ipynb)**
— `claude_code_in_colab.ipynb`

## Quick start

Three cells is the whole setup.

```python
# 1. Install (native binary, no Node.js needed)
!curl -fsSL https://claude.ai/install.sh | bash

# 2. Put ~/.local/bin on PATH for later cells
import os
os.environ['PATH'] = os.path.expanduser('~/.local/bin') + ':' + os.environ['PATH']

# 3. Key from Colab Secrets (sidebar 🔑, name it ANTHROPIC_API_KEY, enable notebook access)
from google.colab import userdata
os.environ['ANTHROPIC_API_KEY'] = userdata.get('ANTHROPIC_API_KEY')
```

Then:

```python
!claude --bare -p 'Summarize README.md' --allowedTools 'Read'
```

## Requirements

- An Anthropic **Console API key** (`sk-ant-...`) from <https://platform.claude.com>. Colab has no
  browser-based OAuth login, so a Console key is the practical path.
- A Claude **Pro, Max, Team, Enterprise or Console** account — the free claude.ai plan does not
  include Claude Code.
- **No GPU.** Claude Code does no local inference; a CPU runtime is correct and cheaper on quota.

## Flag cheat sheet

| Flag | Why it matters in Colab |
| --- | --- |
| `-p` | Non-interactive. The only workable mode — cells have no TTY. |
| `--bare` | Skips hooks, plugins, MCP, `CLAUDE.md`. Faster and reproducible; reads `ANTHROPIC_API_KEY` directly. |
| `--allowedTools 'Read,Edit,Bash(pytest *)'` | A `-p` run starts in Manual mode, so anything not pre-approved is denied. |
| `--permission-mode acceptEdits` | Lets Claude write files unattended. |
| `--permission-prompts none` | Nothing waits for an approval nobody will give. |
| `--max-turns 15` | Caps a confused run before it burns budget. |
| `--output-format json` | Returns `result`, `session_id`, `num_turns`, `total_cost_usd`. |
| `--output-format stream-json --verbose` | Live event stream, so a long run isn't a blank cell. |
| `--resume "$SESSION_ID"` | Continues a previous session with its full context. |
| `--model claude-sonnet-5` | `claude-opus-5`, `claude-sonnet-5`, `claude-haiku-4-5`, or aliases `opus`/`sonnet`/`haiku`. |

## Agent SDK

```python
!pip install -q claude-agent-sdk
```

The SDK drives the CLI under the hood — the install above is still required.

The one Colab-specific trap: Colab already runs an event loop, so `asyncio.run(main())` (which every
SDK example ends with) raises `RuntimeError: asyncio.run() cannot be called from a running event
loop`. Use top-level `await main()` instead.

## Troubleshooting

| Symptom | Fix |
| --- | --- |
| `claude: command not found` | Re-run the `PATH` cell. After *Disconnect and delete runtime*, re-run the installer too. |
| `RuntimeError: asyncio.run() cannot be called from a running event loop` | Use `await main()`, not `asyncio.run(main())`. |
| Run ends with nothing done | A tool wasn't pre-approved. Add it to `--allowedTools`, or pass `--permission-mode acceptEdits`. |
| Cell hangs forever | Add `--permission-prompts none` and `--max-turns`. |
| Files vanished | Colab reclaims the VM after idle/~12h. Push to git or mount Drive before disconnecting. |
| Unexpected spend | Check `total_cost_usd` in the JSON output; drop to `claude-haiku-4-5` while iterating. |

## Notes

- Colab runs as **root**, so `acceptEdits` plus an explicit `--allowedTools` list is the safer default;
  there is no second line of defense in the VM.
- Clear notebook outputs before committing. A key echoed into a cell output lives in the `.ipynb` forever.

## Reference

- [Claude Code docs](https://code.claude.com/docs/en/overview)
- [CLI reference](https://code.claude.com/docs/en/cli-reference)
- [Run Claude Code programmatically](https://code.claude.com/docs/en/headless)
- [Agent SDK (Python)](https://code.claude.com/docs/en/agent-sdk/python)
