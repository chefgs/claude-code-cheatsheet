# Claude Code — Quick Cheatsheet

> Commands ranked most → least useful. Run in the Claude Code terminal prompt.

---

## Installation & Access Methods

Claude Code can be accessed in four ways. All methods share the same underlying model and slash-command surface.

---

### 1 — Terminal / CLI (primary method)

**Prerequisites:** Node.js 18+ and npm.

```bash
# Install globally
npm install -g @anthropic-ai/claude-code

# Authenticate (browser OAuth or API key)
claude login

# Start an interactive session in your project
cd my-project
claude
```

**Check & update:**
```bash
claude --version          # show installed version
claude update             # update to latest
claude doctor             # diagnose any install issues
```

**Uninstall:**
```bash
npm uninstall -g @anthropic-ai/claude-code
```

> **Tip:** Set `ANTHROPIC_API_KEY` in your shell profile (`~/.zshrc` / `~/.bashrc`) to avoid re-authenticating on every session:
> ```bash
> export ANTHROPIC_API_KEY="sk-ant-..."
> ```

---

### 2 — VS Code Extension

Install the **Claude Code** extension from the VS Code Marketplace to get an embedded panel inside your editor.

**Via the VS Code UI:**
1. Open VS Code → Extensions (`Ctrl+Shift+X` / `Cmd+Shift+X`)
2. Search `Claude Code`
3. Click **Install**

**Via the command line:**
```bash
code --install-extension anthropic.claude-code
```

**Via the VS Code Quick Open:**
```
Ctrl+P  →  ext install anthropic.claude-code
```

**Key VS Code features:**
| Feature | How to use |
|---|---|
| Open Claude panel | `Ctrl+Shift+P` → "Claude Code: Open" |
| Chat in sidebar | Click the Claude icon in the Activity Bar |
| Attach open file | Type `@` in the chat input and select the file |
| Accept / reject inline edits | Diff view appears in editor — click ✓ or ✗ |
| Run a slash command | Type `/` in the Claude chat panel |

> The VS Code extension shares the same CLI binary — install the npm package first and the extension will detect it automatically.

---

### 3 — Desktop Application (macOS / Windows / Linux)

Claude Code ships as a standalone desktop app, useful when you prefer a dedicated window outside your editor.

**Install:**

| Platform | Method |
|---|---|
| **macOS** | Download `.dmg` from [claude.ai/download](https://claude.ai/download), drag to Applications |
| **Windows** | Download `.exe` installer from [claude.ai/download](https://claude.ai/download), run setup |
| **Linux** | Download `.AppImage` or `.deb` from [claude.ai/download](https://claude.ai/download) |

**Or install via package managers:**
```bash
# macOS — Homebrew
brew install --cask claude-code

# Windows — winget
winget install Anthropic.ClaudeCode

# Linux — snap
sudo snap install claude-code
```

**First launch:**
1. Open the Claude Code app
2. Sign in with your Anthropic account or paste your API key
3. Use **File → Open Folder** (or drag a folder onto the window) to set your working directory
4. Start chatting — all slash commands and `!` shell escapes work the same as in the terminal

---

### 4 — Mobile App (iOS & Android)

The Claude mobile app includes a **Code** mode that lets you interact with Claude Code on the go — useful for reviewing, asking questions, or light edits when away from a desktop.

**Install:**

| Platform | Link |
|---|---|
| **iOS** | [App Store — Claude by Anthropic](https://apps.apple.com/app/claude-by-anthropic/id6473753684) |
| **Android** | [Google Play — Claude](https://play.google.com/store/apps/details?id=com.anthropic.claude) |

**Activate Code mode:**
1. Open the Claude app
2. Tap the **⊕** (compose) button to start a new conversation
3. Tap the **`</>` Code** toggle in the input bar to switch to Code mode
4. Paste code, describe your task, or share a file from your device

**Mobile capabilities:**
- Full slash-command support (`/code-review`, `/security-review`, etc.)
- Attach files from device storage or cloud drives
- Syntax-highlighted code responses
- Copy code blocks with one tap
- Continue sessions started on desktop (conversation sync)

> **Limitation:** The mobile app does not have direct terminal access or filesystem write access. Use it for review, planning, and code generation — apply changes on your desktop.

---

### Choosing the Right Method

| Scenario | Best method |
|---|---|
| Everyday development, terminal-first workflow | **Terminal / CLI** |
| Working inside VS Code | **VS Code Extension** |
| Prefer a dedicated app window, non-VS Code editors | **Desktop App** |
| On the go, reviewing code, quick questions | **Mobile App** |
| CI/CD pipelines, scripted automation | **Terminal / CLI** (`claude -p`) |

---

## Built-in Slash Commands

### Tier 1 — Daily Drivers

| Command | What it does | Example |
|---|---|---|
| `/clear` | Wipe conversation context (fresh start, tokens reset) | `/clear` |
| `/compact` | Summarize + compress context, keeps token count low | `/compact focus on the auth module only` |
| `/cost` | Show tokens spent + estimated cost for this session | `/cost` |
| `/model` | Switch model mid-session | `/model claude-opus-5` |
| `/config` | Open interactive settings (model, theme, permissions, workflow size) | `/config` |
| `/config key=value` | Set a setting inline without opening the full panel | `/config model=claude-opus-5` |
| `/context` | Show context window usage; warns when conversation exceeds limit | `/context` |
| `/plan` | Enter plan mode — Claude proposes a plan before executing | `/plan` |

### Tier 2 — Frequent

| Command | What it does | Example |
|---|---|---|
| `/memory` | View/edit your persistent memory files | `/memory` |
| `/help` | List all commands + keyboard shortcuts | `/help` |
| `/pr_comments` | Pull latest PR review comments into context | `/pr_comments` |
| `/terminal-setup` | Configure shell integration (shift+enter, etc.) | `/terminal-setup` |
| `/doctor` | Diagnose Claude Code installation issues | `/doctor` |
| `/mcp` | Manage MCP servers — list, connect, authenticate, view errors | `/mcp` |
| `/usage` | Show session token/spend usage bars | `/usage` |
| `/rewind` | Rewind conversation to an earlier state (Esc+Esc to pick) | `/rewind` |
| `/fork` | Copy current conversation into a new background session | `/fork` |
| `/subtask` | Launch an in-session subagent for a contained subtask | `/subtask refactor the auth module` |
| `/background` | Send current session to background (`←` also works) | `/background` |
| `/resume` | Resume a past or backgrounded session from a picker | `/resume` |
| `/add-dir` | Add a directory to the session's working scope | `/add-dir ../shared-lib` |
| `/btw` | Ask a side question without breaking the main task context | `/btw what does this function return?` |

### Tier 3 — Occasional

| Command | What it does | Example |
|---|---|---|
| `/status` | Show account, subscription, and quota status | `/status` |
| `/login` | Re-authenticate (API key or browser) | `/login` |
| `/logout` | Sign out of current session | `/logout` |
| `/install-github-app` | Install the Claude GitHub App for PR integration | `/install-github-app` |
| `/usage-credits` | Request usage credits from your org admin | `/usage-credits` |
| `/voice` | Toggle voice dictation (requires SoX on Linux) | `/voice` |
| `/remote-control` | Share session link so web/mobile viewers can watch or interact | `/remote-control` |
| `/teleport` | Jump into a remote cloud session | `/teleport` |

---

## Skills (Slash Commands from Installed Agents)

### Tier 1 — Use on Every PR / Feature

```
/code-review              Review diff for bugs, simplification, efficiency (runs as background subagent)
/code-review --fix        Review AND auto-apply fixes to working tree
/code-review --comment    Post findings as inline PR comments
/ultrareview              Deep cloud-based review of a PR or branch (billed separately)

/verify                   Run the app and confirm a change actually works
/security-review          Full security audit of pending branch changes
/simplify                 Cleanup pass: reuse, efficiency, dead code removal
```

**Examples:**
```
/code-review --fix
/code-review low          # quick pass — fewer, high-confidence findings only
/code-review high         # thorough pass — broader coverage
/code-review ultra        # cloud ultra-review of current branch
/ultrareview              # deep review of open PR
/ultrareview main         # compare against main branch
/security-review
/verify                   # launches app, exercises the change, reports result
```

### Tier 2 — Project Lifecycle

```
/init                     Generate CLAUDE.md for a new or undocumented project
/review                   Full pull request review (summary + findings + verdict)
/run                      Start the project's dev server and screenshot/validate
/deep-research <topic>    Multi-source, fact-checked research report (invoke manually)
```

**Examples:**
```
/init
/review                   # run inside a branch with open PR
/run
/deep-research best practices for JWT refresh token rotation 2025
```

### Tier 3 — Automation & Scheduling

```
/loop <interval> <cmd>    Run a command on a recurring interval
/schedule                 Create/manage cloud cron agents (runs without you)
/update-config            Edit settings.json, hooks, permissions via natural language
/fewer-permission-prompts Scan transcripts and add allowlist to reduce popups
```

**Examples:**
```
/loop 5m /code-review     # re-review every 5 minutes while you work
/loop                     # self-paced loop (model decides timing)
/schedule                 # opens scheduling dialog
/update-config allow npm commands
/update-config when claude stops, show a desktop notification
/fewer-permission-prompts
```

### Tier 4 — Specialist / On-Demand

```
/find-skills <query>      Discover installable skills for a task
/keybindings-help         Customize keyboard shortcuts
/update-config            Update settings, hooks, env vars
/claude-api               Reference for Anthropic SDK, models, pricing, tool use
```

---

## Keyboard Shortcuts (Terminal)

| Shortcut | Action |
|---|---|
| `Enter` | Submit message |
| `Shift+Enter` | Newline in message (requires /terminal-setup) |
| `Ctrl+C` | Cancel current agent action |
| `Ctrl+B` | Background current action (keep it running) |
| `Ctrl+L` | Clear terminal (not context) |
| `Ctrl+O` | Toggle transcript mode |
| `Ctrl+G` | Open current plan/file in external editor |
| `←` (left arrow) | Send session to background / open agents view |
| `Esc+Esc` | Open rewind picker (go back to an earlier state) |
| `↑ / ↓` | Navigate message history |
| `Esc` | Cancel tool permission prompt |

---

## ! Shell Escape

Prefix any command with `!` to run it as a shell command and pipe output directly into the conversation:

```bash
! git log --oneline -20         # show recent commits in context
! cat src/auth/jwt.ts           # read a file into context
! npm test 2>&1 | tail -40      # run tests, show last 40 lines
! gcloud auth login             # interactive auth (output stays in session)
! curl -s https://api.example.com/health | jq .
```

---

## CLI Commands (Run from Your Shell)

### Non-Interactive / Headless Mode

```bash
claude -p "Fix the bug in src/api.ts"           # print mode: run once, print response, exit
claude --print "Summarize this codebase" | tee out.txt
cat error.log | claude -p "What's wrong?"       # pipe input into Claude
claude -p --json "List all TODOs" > todos.json  # machine-readable JSON output
```

### Code Review via CLI

Run a code review from your shell — no interactive session needed:

```bash
# Quick review of current working-tree changes
claude -p "/code-review"

# Review and auto-apply fixes (no prompts — good for CI)
claude -p "/code-review --fix" --dangerously-skip-permissions

# Low / high detail passes
claude -p "/code-review low"   # faster, high-confidence findings only
claude -p "/code-review high"  # thorough, broader coverage

# Review a specific file
claude -p "Review src/auth/middleware.ts for bugs and suggest improvements"

# Pipe a diff and review it
git diff HEAD~1 | claude -p "Review this diff for logic errors and edge cases"

# Save review output to a file
claude -p "/code-review" > review-$(date +%Y%m%d).txt

# Review and post findings as PR comments (requires GitHub integration)
claude -p "/code-review --comment" --dangerously-skip-permissions
```

### Security Review via CLI

Audit your branch for vulnerabilities without opening an interactive session:

```bash
# Full security audit of pending branch changes
claude -p "/security-review"

# Security review with output saved to a report
claude -p "/security-review" > security-report-$(date +%Y%m%d).txt

# Pipe a specific file for a targeted audit
cat src/api/auth.py | claude -p "Perform a security review of this file. Check for injection, auth bypass, and insecure defaults."

# Review for a specific vulnerability class
claude -p "Check src/ for any SQL injection vulnerabilities. List file:line and the unsafe pattern."

# Review secrets / credential leaks before a commit
git diff --staged | claude -p "Check this diff for accidentally committed secrets, API keys, or credentials."

# Run security review as a background agent
claude --bg "/security-review" --dangerously-skip-permissions
claude agents    # check when it's done
```

### Deep / Ultra Review via CLI

```bash
# Cloud-based deep PR review (billed separately)
claude -p "/ultrareview"

# Compare against a specific branch
claude -p "/ultrareview main"

# Save the ultra-review report
claude -p "/ultrareview" > ultrareview-$(date +%Y%m%d).txt
```

### Session & Agent Management

```bash
claude agents                          # list all running/backgrounded sessions
claude agents --json                   # JSON output for scripting
claude attach <session-id>             # re-attach to a background session
claude rm <session-id>                 # delete a session
claude --continue                      # resume the most recent session
claude --resume <session-id>           # resume a specific past session
claude --bg "Run tests and fix failures"  # start a background agent session
```

### MCP Server Management

```bash
claude mcp list                        # list all configured MCP servers and their status
                                       # (shows HTTP error details for servers that failed to connect)
```

### Other CLI Commands

```bash
claude update                          # update Claude Code to the latest version
claude doctor                          # diagnose installation issues
claude auto-mode reset                 # restore default auto-mode config (prompts for confirm)
claude auto-mode reset --yes           # skip confirmation
claude daemon stop                     # stop the background daemon
claude daemon stop --any               # stop any daemon process (use with care)
```

### Useful CLI Flags

| Flag | What it does |
|---|---|
| `-p` / `--print` | Non-interactive: run once and exit |
| `--json` | Output as machine-readable JSON |
| `--bg` | Start as a background session |
| `--continue` | Resume the most recent session |
| `--resume <id>` | Resume a specific session |
| `--settings <file>` | Use a custom settings file |
| `--mcp-config <file>` | Load MCP server config from a file |
| `--max-budget-usd <n>` | Hard spend cap for the session |
| `--forward-subagent-text` | Include subagent text in stream-json output |
| `--ax-screen-reader` | Enable screen reader accessibility mode |
| `--dangerously-skip-permissions` | Skip all permission prompts (CI/automation only) |

### CI / Automation Recipes

Wire Claude Code into your pipeline for automated reviews on every PR:

```yaml
# GitHub Actions — code review on every pull request
- name: Claude Code Review
  run: claude -p "/code-review" --dangerously-skip-permissions
  env:
    ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
```

```yaml
# GitHub Actions — security audit on every push to main
- name: Claude Security Review
  run: claude -p "/security-review" --dangerously-skip-permissions > security-report.txt
  env:
    ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
- uses: actions/upload-artifact@v4
  with:
    name: security-report
    path: security-report.txt
```

```bash
# Pre-commit hook: block commits that introduce secrets
#!/usr/bin/env bash
git diff --staged | claude -p "Does this diff contain any secrets, API keys, or credentials? Reply YES or NO only." | grep -qi "^yes" && { echo "Secrets detected — commit blocked."; exit 1; }
```

---

## @ Mentions — Reference Files Without Pasting

Type `@` in the prompt to attach files, directories, or URLs directly into context:

```
@src/auth/middleware.ts    # attach a specific file
@src/auth/               # attach all files in a directory
@https://example.com/doc  # fetch a URL into context
```

---

## Emoji Shortcodes in the Prompt

Type `:name:` or partial `:na` to autocomplete emoji directly in the input:

```
:white_check_mark:    → ✅
:bug:                 → 🐛
:rocket:              → 🚀
```
Disable with `"emojiCompletionEnabled": false` in settings.

---

## Prompt Best Practices

### Be Explicit About Scope

```
# Vague — agent may over-reach or under-deliver
"fix the login bug"

# Precise — scope, file, constraint
"Fix the JWT expiry check in src/auth/middleware.ts:47 — tokens are being
 accepted after expiry. Do not touch the refresh token logic."
```

### State the Output Format You Want

```
"Give me a 3-bullet summary, not a full implementation."
"Write the code. No explanation unless something is non-obvious."
"Show the diff only — don't rewrite the whole file."
```

### Separate Research from Implementation

```
# Research first (read-only, cheap)
"Find all places in the codebase where we call getUserById — list file:line only."

# Then implement (destructive, expensive — confirm before running)
"Now update each of those callsites to use getUserByIdOrThrow instead."
```

### Anchor on the WHY

```
# Without context — agent may pick the wrong fix
"Remove the setTimeout in checkout.ts"

# With context — agent understands the constraint
"Remove the setTimeout in checkout.ts:88 — it was a workaround for a race
 condition that was fixed in PR #412. The delay now just slows down checkout."
```

### Use File:Line References

```
"The bug is in src/api/orders.ts:134 — the status field is not being validated
 against the OrderStatus enum before insert."
```

---

## Context & Token Usage

### Understanding the Budget

```
/usage (cost)                     # see current session usage
```

- **~200k token context** in most sessions — enough for ~150KB of code + conversation
- Each `/clear` resets to zero; use it when switching to an unrelated task
- `/compact` summarizes + compresses — keeps thread alive but cuts token count 50–70%
- The auto-compact fires automatically near limit; you can trigger it manually anytime

### What Costs the Most Tokens

| Action | Token cost | Mitigation |
|---|---|---|
| Reading entire large files | High | Read specific line ranges: `Read file:100-200` |
| Pasting full file contents | High | Reference by path, let agent read it |
| Long back-and-forth iterations | Medium | `/compact` mid-session |
| Running agents with broad scope | Medium-High | Narrow the prompt scope |
| Web searches with large pages | High | Ask for summary, not full page |

### Smart Context Loading

```
# Bad — loads everything into context
"Look at the entire backend and tell me what's wrong"

# Good — targeted
"Check src/api/auth.py and src/middleware/jwt.py for the token validation flow"
```

### Preserve Context Across Long Tasks

```
# Before hitting 80% token usage:
"Summarize where we are and what's left — I'm going to /compact"
/compact focus on: auth refactor, files changed so far, next step is the refresh endpoint

# After compact, re-anchor:
"Continuing the auth refactor. We've updated login and logout. Next: refresh endpoint in src/api/auth.py"
```

### Context Window Rules of Thumb

| Situation | Action |
|---|---|
| New unrelated task | `/clear` — full reset |
| Same task, getting long | `/compact <focus hint>` |
| Switching files/features | Mention what changed: "Now moving to the payment module" |
| Agent seems confused/looping | `/clear` and re-state cleanly |
| Research-heavy session | Spawn `Agent` tool to protect main context |

### Efficient Multi-File Work

```
# Tell the agent what NOT to read
"Only look at the files under src/auth/ — ignore everything in src/billing/"

# Give it a map instead of letting it explore
"The entry point is src/server.ts → routes in src/routes/ → handlers in src/handlers/auth.ts"

# Batch related questions
"In one pass: (1) find where sessions are stored, (2) check if they're encrypted,
 (3) confirm TTL is set. Report back before making any changes."
```

### Model Selection by Task

| Task | Best model | Command |
|---|---|---|
| Quick edits, formatting, rename | Haiku 4.5 | `/model claude-haiku-4-5` |
| Feature implementation, review | Sonnet 5 (default) | `/model claude-sonnet-5` |
| Architecture, complex reasoning | Opus 4.8 | `/model claude-opus-4-8` |
| Long research + synthesis, 1M ctx | Opus 5 (latest) | `/model claude-opus-5` |

Switch back after heavy tasks: `/model claude-sonnet-5`

---

## Effective Prompting Patterns

### The 3-Part Task Structure

```
GOAL:    What outcome do you need?
CONTEXT: What files/systems/constraints are relevant?
OUTPUT:  What format should the answer take?

Example:
"GOAL: Add rate limiting to the login endpoint.
 CONTEXT: FastAPI backend in src/api/auth.py, we use Redis (already configured in src/cache.py).
 OUTPUT: Show only the changed functions, no full file rewrite."
```

### Iterative Refinement (don't start over)

```
Turn 1: "Implement the password reset flow"
Turn 2: "Good. Now add the email sending step — use the existing mailer in src/mail.py"
Turn 3: "The token should expire in 1 hour, not 24 — update just that constant"
```

### Defensive Prompts (prevent over-reach)

```
"Do NOT modify any test files."
"Read only — do not make changes yet, just report what you find."
"Only change the function signature, not the implementation."
"Stop after writing the migration — do not run it."
```

### Parallel Research (saves time)

```
"In parallel, find: (1) where we define database models, (2) where we handle errors,
 (3) where the API routes are registered. List file paths only."
```

### Extended Thinking Keywords

Trigger deeper reasoning by adding these words to your prompt:

| Keyword | Thinking depth |
|---|---|
| `think` | Normal extended thinking |
| `think harder` / `think more` | Deeper thinking |
| `ultrathink` | Maximum thinking budget |

```
"ultrathink — design a zero-downtime migration strategy for this schema change"
"think harder about edge cases in the rate limiter"
```

### Stacked Slash Skills

Chain multiple skills in a single invocation — they run sequentially, each using the prior skill's result as its target:

```
/code-review /simplify /verify    # review, then simplify, then verify in sequence
```

---

## Background Agents & Multi-Agent Workflows

### Managing Sessions in the Background

```bash
claude --bg "Run all tests and fix any failures"   # launch a background agent
claude agents                                       # see all running/stopped sessions
claude attach <id>                                  # re-attach to a running session
←  (left arrow in terminal)                        # send current session to background
/fork                                               # copy conversation to a new bg session
/subtask refactor the payment module               # run a contained task as a subagent
/resume                                             # pick and resume a past session
/background                                         # park this session (same as ←)
```

### Agent View Workflow

```
1. Start a long task:  claude --bg "Migrate all API endpoints to v2"
2. Check progress:     claude agents (shows Running / Needs input / Done)
3. Respond to prompts: claude attach <id>  or  ← in any session
4. Run another task:   /fork  →  sends copy to bg, you keep working
5. Clean up:           claude rm <id>
```

### Controlling Concurrency

```bash
CLAUDE_CODE_MAX_CONCURRENT_SUBAGENTS=10   # cap parallel subagents (default: 20)
CLAUDE_CODE_MAX_SUBAGENTS_PER_SESSION=50  # cap total spawns per session (default: 200)
CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH=2    # allow nested subagents (default: 3)
CLAUDE_CODE_MAX_WEB_SEARCHES_PER_SESSION=100  # prevent search loops (default: 200)
CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1    # enable experimental agent teams feature
```

---

## MCP (Model Context Protocol)

### Using MCP in Claude Code

```bash
# Load an MCP config file at startup
claude --mcp-config ./mcp-servers.json

# View status of all MCP servers
/mcp

# List servers + connection errors from the CLI
claude mcp list
```

### Example `mcp-servers.json`

```json
{
  "servers": {
    "github": { "command": "mcp-server-github", "args": ["--token", "${GITHUB_TOKEN}"] },
    "postgres": { "command": "mcp-server-postgres", "args": ["--url", "${DATABASE_URL}"] }
  }
}
```

MCP tool calls running longer than 2 minutes move to the background automatically.  
Override the threshold: `CLAUDE_CODE_MCP_AUTO_BACKGROUND_MS=120000`

---

## Hooks System

Hooks let you intercept Claude's tool calls with custom scripts, with exit code control:

| Exit code | Meaning |
|---|---|
| `0` | Proceed normally |
| `1` | Show stderr to user (warning), but allow tool to continue |
| `2` | Block the tool call — show stderr to Claude so it can correct |

### Common Hook Events

| Event | When it fires |
|---|---|
| `PreToolUse` | Before every tool call |
| `PostToolUse` | After every tool call completes |
| `SessionStart` | When a session starts (source: `resume` or `fork`) |
| `DirectoryAdded` | After `/add-dir` registers a new working directory |

### Example: Block dangerous `rm -rf` commands

Add to your `settings.json`:
```json
{
  "hooks": {
    "PreToolUse": [{
      "matcher": "Bash",
      "hooks": [{ "type": "command", "command": "/usr/local/bin/check-dangerous-command.sh" }]
    }]
  }
}
```

Configure via natural language: `/update-config block all git push --force commands`

---

## CLAUDE.md — Project Memory

`CLAUDE.md` is loaded automatically into every session's context for a project.

### Recommended Structure

```markdown
# Project: <name>

## Architecture
- Entry point: src/server.ts → routes in src/routes/ → handlers in src/handlers/
- Database: PostgreSQL via Prisma ORM (src/db/)

## Key Conventions
- All API errors must use the AppError class in src/errors.ts
- Never commit secrets — use .env.local for local overrides
- Tests live in __tests__/ mirroring src/ structure

## Common Commands
- Dev server: npm run dev
- Tests: npm test
- Lint: npm run lint

## Off-Limits
- Do NOT modify src/legacy/ — read-only unless explicitly asked
- Do NOT run database migrations without confirming with the user
```

Generate one for any project with: `/init`

### Memory Scopes

| Scope | Location | Loaded when |
|---|---|---|
| User (global) | `~/.claude/CLAUDE.md` | All sessions |
| Project | `<repo>/CLAUDE.md` | In-project sessions |
| Rules | `<repo>/.claude/rules/*.md` | Conditionally per path |
| Team | `CLAUDE_MEMORY_STORES` env path | Shared team sessions |

```bash
# Share memory stores across a team:
export CLAUDE_MEMORY_STORES=/shared/team-memory/CLAUDE.md
```

### CLAUDE.md Imports

```markdown
# Pull in additional shared files:
@.claude/team-standards.md
@docs/api-conventions.md
```

---

## Quick Reference Card

```
DAILY                          WHEN STUCK
/cost        → check budget    /clear      → fresh start
/compact     → trim context    /help       → list commands
/model       → switch model    /doctor     → fix install
/context     → check ctx used  /rewind     → undo to earlier state

CODE QUALITY                   AUTOMATION
/code-review → find bugs       /loop       → repeat task
/ultrareview → deep PR review  /schedule   → cloud cron
/simplify    → clean up code   /update-config → edit settings
/verify      → test the change /background → park session
/security-review → audit PR    claude agents → manage bg sessions

SHELL ESCAPE                   CONTEXT TIPS
! git log    → git in session  Read specific line ranges
! npm test   → run tests       /compact before switching tasks
! cat file   → read into ctx   State file:line in prompts
@file.ts     → attach to ctx   /fork to protect main context
```

---

*Last updated: 2026-08-03*
