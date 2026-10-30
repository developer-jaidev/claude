# START HERE — Video Studio project

Four files. Use them in this order.

| File | What it is | What you do with it |
|---|---|---|
| `0_START_HERE.md` | This guide | Read once |
| `CLAUDE.md` | The project's brain: every tool, command, rule and the psychology playbook | Put it in your project folder. Claude Code reads it automatically every session |
| `1_SETUP_PROMPT.md` | One-time install of every tool | Paste into Claude Code once |
| `2_EDIT_REEL_IMG_1541.md` | The edit brief for your reel | Paste after setup is done |

## Steps

1. Open Ubuntu (WSL) from the Windows Start menu.
2. Make the project folder: `mkdir -p ~/video-studio && cd ~/video-studio`
3. Copy `CLAUDE.md`, `1_SETUP_PROMPT.md` and `2_EDIT_REEL_IMG_1541.md` into it. In Windows File Explorer the folder is at `\\wsl$\Ubuntu\home\<your-ubuntu-name>\video-studio`.
4. Start Claude Code in that folder: `claude`
5. Paste the whole of `1_SETUP_PROMPT.md`. Answer its questions (Gemini key, Higgsfield login, which optional keys you have). It takes 1–2 hours, mostly downloads.
6. Restart Claude Code when it asks, and let it finish the test.
7. Paste `2_EDIT_REEL_IMG_1541.md` (change the video path first). Approve its plan by typing `go`.

## Using a claude.ai Project instead of Claude Code?

The tools only run in Claude Code on your laptop. In a claude.ai Project you can still upload `CLAUDE.md` as project knowledge so that chat plans edits and writes prompts the same way, then paste those prompts into Claude Code.

## Every new video after this

Start Claude Code in `~/video-studio` and say:

> "New video. Footage: `<path>`. Platform: `<Reel / Short / YouTube>`. Recipe: `<A / B / C / D>`. Script: `<paste or 'transcribe it'>`."

Claude follows `CLAUDE.md` from there.

## Every new tool after this

Paste the link and say "analyse this tool and add it to CLAUDE.md". It will return a tool card and update the file.
