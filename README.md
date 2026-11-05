# claude-sessions

Terminal browser for your [Claude Code](https://claude.com/claude-code) conversations. List them, read them, restore one (`claude --resume`), start a new one or delete one. Works on Linux, macOS and Windows.

Single Python file, standard library only (curses). No dependencies on Linux and macOS; Windows needs `windows-curses`, because its Python has no curses.

![Conversation list](docs/list.png)

![Conversation viewer](docs/view.png)

*(Screenshots use sample conversations.)*

## Install

### Linux and macOS

```bash
mkdir -p ~/.local/bin && curl -fsSL https://raw.githubusercontent.com/PericlesSavio/claude-sessions/main/claude-sessions -o ~/.local/bin/claude-sessions && chmod +x ~/.local/bin/claude-sessions
```

Requires Python 3 and `~/.local/bin` in your `PATH`. Optional alias:

```bash
echo 'alias cs="claude-sessions"' >> ~/.bashrc
```

### Windows

In PowerShell:

```powershell
python -m pip install windows-curses
$dir = "$HOME\.local\bin"; New-Item -ItemType Directory -Force $dir | Out-Null
$url = "https://raw.githubusercontent.com/PericlesSavio/claude-sessions/main"
"claude-sessions", "claude-sessions.cmd" | ForEach-Object { Invoke-WebRequest "$url/$_" -OutFile "$dir\$_" }
```

Requires Python 3 and `%USERPROFILE%\.local\bin` in your `PATH` (the Claude Code native installer already uses this folder). Run it in PowerShell, cmd or Windows Terminal; in Git Bash, use `winpty claude-sessions.cmd`. Optional alias:

```powershell
Add-Content $PROFILE 'Set-Alias cs claude-sessions'
```

## Usage

```bash
claude-sessions            # open the browser
claude-sessions --version
```

| Key | Action |
|---|---|
| `↑` `↓` / `j` `k`, `PgUp` `PgDn`, `g` `G` | move |
| `Enter` | view the conversation (scrollable, only your and Claude's text) |
| `n` | new conversation: asks for the folder (starts with the current one) and runs `claude` there |
| `r` | restore: `cd` to the original folder and run `claude --resume <id>` |
| `d` | delete (asks `[y/N]`) |
| `/` | filter by title, folder or id (`Esc` clears) |
| `q` | quit |

Inside the viewer: `r` restore, `d` delete, `q` back.

## Notes

- Sessions are read from `~/.claude/projects` (or `$CLAUDE_CONFIG_DIR/projects`).
- `n` only accepts a folder that already exists.
- Delete removes the session `.jsonl` and its same-named folder permanently; there is no trash.

## Version

0.2.0
