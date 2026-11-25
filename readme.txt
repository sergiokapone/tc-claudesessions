ClaudeSessions 1.0 - Total Commander plugins for Claude Code sessions (32 and 64 bit)
====================================================================================

Claude Code keeps every conversation as a *.jsonl file (folder "projects" in its
data directory). ClaudeSessions makes them pleasant to work with in Total Commander.
One DLL does three jobs; copy it under the extension you need:

  ClaudeSessions.wlx64  Lister plugin   - F3 on a session shows the conversation
  ClaudeSessions.wfx64  File system     - the "projects" folder as a virtual folder
  ClaudeSessions.wdx64  Content plugin  - columns for *.jsonl files

(32-bit builds: ClaudeSessions.wlx / .wfx / .wdx.)

FILE SYSTEM (WFX)  "Claude sessions" in Network Neighborhood
  - The projects folder is found automatically (CLAUDE_CONFIG_DIR, a "Programs\Claude"
    layout, %USERPROFILE%\.claude, or Path= in the ini).
  - One subfolder per project (named after the project path), inside it the sessions
    as "2026-11-20 11-14  Title [id].jsonl", newest last when sorted by name.
  - Columns: prompts, model, date, size; also Title, Started, LastActive, Project, Id.
  - F3 = view the conversation, F5 = copy the .jsonl (or a Markdown version, see ExportMd),
    Alt+Enter = properties.
  - Enter on a session = resume it: opens a terminal in the project folder and runs
        claude --resume <session id>
    (Windows Terminal if available, else cmd; configurable, see below).
  - Read-only: sessions are never deleted, renamed or moved from here.

LISTER (WLX)
  Shows the conversation in its own window, terminal style: colours per role, box-drawing
  headers, tool calls (>) and their results, light Markdown (headings, lists, code blocks,
  bold, `code`), long lines wrap. Light/dark theme and language (English, Russian,
  Ukrainian) follow Total Commander.
  Keys: R cycles tool results (hide / short / full), T shows or hides the model's
  thinking, Ctrl+F / F7 search, N / P next and previous file. Right click: the same
  options plus Copy, Select all and "Save as Markdown...".
  No other plugin or script is needed (no renderer, no PowerShell).

CONTENT (WDX)
  Title, Started, LastActive, Messages (prompts), Project, Model, Id for *.jsonl files in
  ordinary folders too. The prompt count needs the whole file and is calculated in the
  background.

INSTALL
  Open one of the ClaudeSessions-*.zip installers in Total Commander (Enter) and confirm.
  Or copy the files and add them by hand:
    Lister:       Configuration > Options > Plugins > Lister plugins (WLX) > Add
                  detect string:  EXT="JSONL"
    File system:  Configuration > Options > Plugins > File system plugins (WFX) > Add
    Content:      Configuration > Options > Plugins > Content plugins (WDX) > Add
  Open the file system from Network Neighborhood (the "Network" button of the drive bar)
  -> "Claude sessions". If another plugin also handles JSONL, move this one up.

SETTINGS  (ClaudeSessions.ini next to the DLL, see ClaudeSessions.ini.example)
  [view]  Language, Theme (auto = follow Total Commander), Results, Thinking, FontSize
  [fs]    Path         projects folder (default: found automatically)
          Enter        resume (default) or copy
          Terminal     wt (default) or cmd
          Claude       launcher to run (default: claude.cmd next to the "data" folder,
                       else "claude" from PATH)
          ResumeCommand  your own command line, placeholders {cwd} {id} {claude}
          ExportMd, MdResults  F5 copies sessions as .md; tool results in it (0/1/2)

NOTES
  - Only system DLLs are used. Sessions can contain private data (paths, command output,
    file contents): a Markdown export contains it too, so share exports with care.
  - Resuming only works if the project folder still exists (Claude Code finds a session by
    the folder it was started in).
  - The 32-bit build compiles from the same source but has had less testing than 64-bit.
  - Closed source, freeware. Downloads and issues: https://github.com/sergiokapone/tc-claudesessions
  - If you find this useful, see the Sponsor button on the GitHub page.
