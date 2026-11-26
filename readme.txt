ClaudeSessions 1.2 - Total Commander plugins for Claude Code sessions (32 and 64 bit)
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
  - Two folders: "All sessions" (the sessions of every project in one list) and
    "Projects" with one subfolder per project (named after the project path), inside it the sessions
    as "Title [id].jsonl" (sort by date for the latest first); own icons for the folders and sessions.
  - Columns: prompts, model, date, size; also Title, Started, LastActive, Project, Id and
    Tokens, OutputTokens, CacheReadTokens.
  - F3 = view the conversation, F5 = copy the .jsonl (or a Markdown version, see ExportMd).
  - Alt+Enter = small menu: go to the real project folder, resume the session, properties.
  - Enter on a session = resume it: opens a terminal in the project folder and runs
        claude --resume <session id>
    (Windows Terminal if available, else cmd; configurable, see below).
  - F8 moves a session (after Total Commander's confirmation) to <claude data>\sessions-trash\
    <project>\, from where it can be moved back; nothing is deleted for good. Sessions are
    never renamed or moved otherwise.
  - Under the two folders: the 5-hour and weekly limits of the Claude subscription, e.g.
    "5-hour limit - 26%" (reset time in the date column; Enter/F3 = details). The same data as
    /usage in Claude Code: the plugin reads the Claude Code login token (.credentials.json in
    the data folder) and asks api.anthropic.com, at most once a minute. The token is only read,
    never refreshed, stored or sent anywhere else. No subscription login, an expired token or
    no network: the entries are not shown (or keep the last values).

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
  Title, Started, LastActive, Messages (prompts), Project, Model, Id, Tokens, OutputTokens,
  CacheReadTokens for *.jsonl files in ordinary folders too. Tokens = new input + cache
  writes + output (cache reads are counted separately). The prompt and token counts need
  the whole file and are calculated in the background.
  The field names follow the language of Total Commander (in a Ukrainian TC: Назва, Початок,
  Остання активність, Повідомлень, Проєкт, Модель, Id, Токени, Токени виводу, Токени з кешу;
  in a Russian one: Название, Начало, ...). Changing the language of TC changes the names, so
  column sets made before have to be set up again (or fix the names with [view] Language=).

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
                       else claude.exe / claude.cmd from PATH, else the usual install
                       places %USERPROFILE%\.local\bin\claude.exe and %APPDATA%\npm\claude.cmd,
                       so a fresh install works without restarting TC)
          ResumeCommand  your own command line, placeholders {cwd} {id} {claude}
          ExportMd, MdResults  F5 copies sessions as .md; tool results in it (0/1/2)
          Trash        where F8 moves sessions (default: sessions-trash next to "projects")
          Limits       0 = do not show the 5-hour and weekly limits in the root

NOTES
  - Only system DLLs are used. Sessions can contain private data (paths, command output,
    file contents): a Markdown export contains it too, so share exports with care.
  - Resuming only works if the project folder still exists (Claude Code finds a session by
    the folder it was started in).
  - The 32-bit build compiles from the same source but has had less testing than 64-bit.
  - Closed source, freeware. Downloads and issues: https://github.com/sergiokapone/tc-claudesessions
  - If you find this useful, see the Sponsor button on the GitHub page.
