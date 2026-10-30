# ONE-TIME SETUP PROMPT

Paste everything below into Claude Code (inside WSL Ubuntu), from your project folder `~/video-studio`.

---

You are setting up my video-editing studio on my Windows laptop. Work inside WSL 2 (Ubuntu). Read `./CLAUDE.md` first — it explains every tool and how I work. Then install, configure and test everything below, in order. After each step, run its check and tell me PASS or FAIL in one line. If something fails twice, note it, try the fallback, and move on. Ask me only when you need a key, a login or a decision.

## STEP 0 — Check my machine

- Confirm we are in WSL 2 Ubuntu (not plain Windows). If not, tell me exactly how to open Ubuntu and stop.
- Report: Ubuntu version, free disk space (I need about 15 GB), RAM, CPU cores, and whether an NVIDIA GPU is visible (`nvidia-smi`).
- Find my Windows user folder under `/mnt/c/Users/` and remember it.

## STEP 1 — System packages

- `sudo apt update && sudo apt install -y git ffmpeg jq build-essential python3 python3-venv python3-pip curl unzip`
- Install Node.js 22 LTS with nvm (HyperFrames needs Node 22+; check `node -v`).
- Install `pipx`, then `pipx install auto-editor`.
- Check: `ffmpeg -version`, `node -v`, `python3 --version`, `auto-editor --version`.

## STEP 2 — claude-video-effects

- `git clone https://github.com/Vibha-Ramprakash/claude-video-effects ~/.claude/skills/effects`
- `pip install -r ~/.claude/skills/effects/requirements.txt` (use a venv if needed).
- Read its SKILL.md and README so you know all 45 effects and how timing works.
- Check: the skill folder exists and `/effects` will be available after a restart.

## STEP 3 — ghost-editor

- `git clone https://github.com/kurbaitaev/ghost-editor ~/.claude/skills/ghost-editor`
- Follow its `docs/INSTALL.md` exactly (ffmpeg, Node, Python, Whisper, OpenCV; sounds, music and emoji download ~3 min).
- Ask me for my free Gemini API key (I get it from aistudio.google.com/apikey). Store it where INSTALL.md says. Never print it back.
- Read `SKILL.md`, `docs/PLAYBOOK.md` and `docs/HOW-IT-WORKS.md`.
- It is built for Apple-silicon Macs. On WSL, note which parts don't work (e.g. the macOS caption check) and tell me.
- Check: render its smallest example, or a 10-second test of my own clip, in the clean preset.

## STEP 4 — claude-shorts

- `git clone https://github.com/AgriciDaniel/claude-shorts.git ~/tools/claude-shorts && cd ~/tools/claude-shorts && bash setup.sh && bash install.sh`
- Read `SKILL.md` and `references/` (scoring rubric, caption styles, platform specs).
- Check: `/shorts` is registered after restart; preflight runs on a test clip.

## STEP 5 — OpenMontage

- `git clone https://github.com/calesthio/OpenMontage.git ~/tools/OpenMontage && cd ~/tools/OpenMontage && make setup`
  (If make is missing, use the manual commands in its README.)
- Read `AGENT_GUIDE.md`, `PROJECT_CONTEXT.md`, `CLAUDE.md` and `PROMPT_GALLERY.md`.
- In `.env`, set a budget cap of $5 and per-action approval at $0.50. Ask me which optional keys I have (Pexels, Pixabay, Unsplash are free; ElevenLabs, FAL, Kling are paid). Leave the rest empty.
- Check: `make demo` (or `python render_demo.py`) renders a zero-key demo; then run the capability check:
  ```
  python -c "from tools.tool_registry import registry; import json; registry.discover(); print(json.dumps(registry.support_envelope(), indent=2))"
  ```
- Show me how to open the Backlot board (`python -m backlot open`).

## STEP 6 — earshot (sound ears + sound bank)

- `git clone https://github.com/Leonxlnx/earshot ~/tools/earshot && cd ~/tools/earshot`
- `python3 -m venv .venv`
- `.venv/bin/python -m pip install torch --index-url https://download.pytorch.org/whl/cpu`
- `.venv/bin/python -m pip install -e ".[mcp,llm,dev]"`
- `.venv/bin/python -m earshot doctor --fetch` then `.venv/bin/python -m earshot doctor --load` (downloads ~1.1 GB of models once).
- Add it as an MCP server for every project:
  `claude mcp add earshot --scope user -e EARSHOT_THREADS=3 -- $HOME/tools/earshot/.venv/bin/python -m earshot mcp`
- Link its two skills: `ln -s ~/tools/earshot/skills/earshot ~/.claude/skills/earshot` and `ln -s ~/tools/earshot/skills/real-sound ~/.claude/skills/real-sound`
- Read `docs/SFX.md`, `docs/LIMITS.md` and `docs/INTEGRATION.md`.
- Check: `earshot sfx list --kind whoosh` and `earshot measure` on any WAV.

## STEP 7 — Real SFX (Clipwing)

- Get the skill from https://clipwing.pro/skills/downloads/real-sfx.skill (a zip) or from the source at https://github.com/Clipwing/skills (folder `skills/real-sfx`). Install it to `~/.claude/skills/real-sfx`.
- Read its SKILL.md and README. Point its sound library at `~/SFX`.
- Check: it lists its 78 bundled CC0 UI sounds.

## STEP 8 — Higgsfield MCP (AI images and video)

- `claude mcp add --transport http --scope user higgsfield https://mcp.higgsfield.ai/mcp`
- Tell me to run `/mcp`, choose Higgsfield and sign in (browser login, no API key). If the browser doesn't open from WSL, give me the URL to open in Windows.
- Check: `claude mcp list` shows it connected. List the available tools and my credit balance. Do NOT generate anything yet.

## STEP 9 — HyperFrames (motion graphics engine)

- `npx skills add heygen-com/hyperframes` — install the core skills (hyperframes, hyperframes-cli, hyperframes-media, hyperframes-creative, hyperframes-registry).
- Check: `/hyperframes` is available after restart.

## STEP 10 — Openverse (free licensed media, no install)

- Test: `curl -s "https://api.openverse.org/v1/audio/?q=whoosh&license=cc0&page_size=3" | jq '.results[] | {title, creator, license, url}'`
- Do the same for `/v1/images/?q=london%20street`.
- Remember: log title, creator, licence and URL for anything used.

## STEP 11 — Sound library

Build `~/SFX` exactly as described in CLAUDE.md section 3:

- Folders `whoosh`, `hit`, `ui`, `riser`, `foley`, `ambience`, `signature`, `_rejects`, `_inbox`; files `_licences.csv` and `catalogue.csv`.
- Fill it: copy Real SFX's 78 CC0 UI sounds; render a starter kit from earshot's bank (4 whooshes, 3 hits, 6 UI sounds, 2 risers, 1 reverse swell); search Openverse for CC0 foley and ambience (motorbike start and pass-by, Tube doors, footsteps, keys, kettle, camera shutter, city street, rain, cafe, wind, train). Show me the list before downloading more than 40 files.
- Convert to 48 kHz 24-bit WAV, trim, fade tails, rename as `category_description_length.wav`, catalogue with earshot, move bad files to `_rejects`.
- Create an inbox script (`~/SFX/process_inbox.sh`) that does all of that for anything I drop into `_inbox`.
- Create an earshot kit: `earshot kit init --preset launch -o ~/SFX/kit.json` and `earshot kit render ~/SFX/kit.json --out ~/SFX/kit`.

## STEP 12 — Restart and full test

- Tell me to restart Claude Code so new skills load. After I say "restarted", list every skill and MCP server you can see.
- Make a 15-second test: a short clip (or a title card if I have no clip) with 3 list items appearing and a reveal. Use `/effects todo`, captions, 4 sounds from `~/SFX`, and run `earshot critique`. Show me the result.

## STEP 13 — Report

Give me one table: tool · installed (yes/no) · tested (pass/fail) · what's missing · fallback.
Then list the keys/logins still needed. Update CLAUDE.md section 2 with anything you learned that differs from what's written (real commands, paths, limits on WSL).

**Rules:** work on copies; never delete my files; never print my keys; ask before any paid generation.
