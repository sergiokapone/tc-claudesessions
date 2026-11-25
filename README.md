## ClaudeSessions 1.0 — Total Commander plugins for Claude Code sessions

Claude Code (Anthropic's CLI) saves every conversation as a `*.jsonl` file in its `projects` folder. Those files are large, unreadable by eye and have no names. **ClaudeSessions** makes them usable inside Total Commander. It is **one DLL that works as three plugins**: copy it as `.wlx64` (Lister), `.wfx64` (file system) or `.wdx64` (content). Total Commander loads only the functions it needs from each copy. 32-bit (`.wlx/.wfx/.wdx`) and 64-bit builds are included. Only system DLLs are used, no other software is required. MIT license.

### File system plugin "Claude sessions" (WFX)
A virtual folder in *Network Neighborhood* (the "Network" button of the drive bar).
- **Finds the Claude Code data by itself**: `CLAUDE_CONFIG_DIR`, a `Programs\Claude\data` layout, `%USERPROFILE%\.claude`, or `Path=` in the ini.
- **One subfolder per project**, named after the real project path (`D › Projects › my-app`); inside it the sessions as `2026-11-20 11-14  Session title [id].jsonl` (sorted by name = chronological).
- **Columns**: prompts, model, date, size; plus Title, Started, LastActive, Project, Id for your own column sets. Info is read quickly (head and tail of the file) and cached; the prompt count (needs the whole file) is calculated in the background.
- **Enter = resume the session**: opens a terminal in the project folder and runs `claude --resume <session id>` (Windows Terminal if present, otherwise cmd). Configurable: terminal, launcher, or your own command line with `{cwd} {id} {claude}`. Enter can also be set to copy instead.
- **F3** shows the conversation, **F5** copies the `.jsonl` (or a Markdown version with `ExportMd=1`), **Alt+Enter** shows session properties.
- **Read-only**: sessions are never deleted, renamed or moved from here.

### Lister plugin (WLX)
F3 on any `*.jsonl` shows the conversation in its own terminal-style window:
- colours per role (you / Claude / tools / errors), box-drawing headers with the session title, project, model and dates;
- tool calls (`>`) with their results, light Markdown (headings, lists, code blocks, **bold**, `code`), long lines wrap;
- **R** cycles tool results (hide / short / full), **T** shows or hides the model's thinking, Ctrl+F / F7 search, N / P next and previous file;
- right click: the same options, Copy, Select all and **Save as Markdown…**;
- light/dark theme and language (English, Russian, Ukrainian) follow Total Commander. Big sessions (800 KB+) open in well under a second.

### Content plugin (WDX)
Title, Started, LastActive, Messages (prompts), Project, Model, Id for `*.jsonl` files in ordinary folders too (search, sort, columns, tooltips).

### Install
Download one of the installers (`ClaudeSessions-WFX/WLX/WDX-1.0.zip`), open it in Total Commander (Enter) and confirm, or take `ClaudeSessions-1.0.zip` with everything and register the files by hand. Lister detect string: `EXT="JSONL"`. Settings: `ClaudeSessions.ini` next to the DLL (see `ClaudeSessions.ini.example`).

### Notes
- Sessions can contain private data (paths, command output, file contents); a Markdown export contains it too. Share exports with care.
- Resuming needs the original project folder to exist (Claude Code finds a session by the folder it was started in).
- Tested with 64-bit Total Commander; the 32-bit build comes from the same source and has had less testing.
- Bug reports and ideas: GitHub Issues.
- If it is useful to you, you can support the work: https://send.monobank.ua/jar/7EiyaxfeWZ
