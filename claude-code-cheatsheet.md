# Claude Code — Quick Cheatsheet

> Commands ranked most → least useful. Run in the Claude Code terminal prompt.

---

## Built-in Slash Commands

### Tier 1 — Daily Drivers

| Command | What it does | Example |
|---|---|---|
| `/clear` | Wipe conversation context (fresh start, tokens reset) | `/clear` |
| `/compact` | Summarize + compress context, keeps token count low | `/compact focus on the auth module only` |
| `/cost` | Show tokens spent + estimated cost for this session | `/cost` |
| `/model` | Switch model mid-session | `/model claude-opus-4-8` |
| `/config` | Open interactive settings (model, theme, permissions) | `/config` |

### Tier 2 — Frequent

| Command | What it does | Example |
|---|---|---|
| `/memory` | View/edit your persistent memory files | `/memory` |
| `/help` | List all commands + keyboard shortcuts | `/help` |
| `/pr_comments` | Pull latest PR review comments into context | `/pr_comments` |
| `/terminal-setup` | Configure shell integration (shift+enter, etc.) | `/terminal-setup` |
| `/doctor` | Diagnose Claude Code installation issues | `/doctor` |

### Tier 3 — Occasional

| Command | What it does | Example |
|---|---|---|
| `/status` | Show account, subscription, and quota status | `/status` |
| `/login` | Re-authenticate (API key or browser) | `/login` |
| `/logout` | Sign out of current session | `/logout` |

---

## Skills (Slash Commands from Installed Agents)

### Tier 1 — Use on Every PR / Feature

```
/code-review              Review diff for bugs, simplification, efficiency
/code-review --fix        Review AND auto-apply fixes to working tree
/code-review --comment    Post findings as inline PR comments

/verify                   Run the app and confirm a change actually works
/security-review          Full security audit of pending branch changes
/simplify                 Cleanup pass: reuse, efficiency, dead code removal
```

**Examples:**
```
/code-review --fix
/code-review low          # quick pass — fewer, high-confidence findings only
/code-review high         # thorough pass — broader coverage
/security-review
/verify                   # launches app, exercises the change, reports result
```

### Tier 2 — Project Lifecycle

```
/init                     Generate CLAUDE.md for a new or undocumented project
/review                   Full pull request review (summary + findings + verdict)
/run                      Start the project's dev server and screenshot/validate
/deep-research <topic>    Multi-source, fact-checked research report
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
| `Ctrl+L` | Clear terminal (not context) |
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
| Quick edits, formatting, rename | Haiku 4.5 | `/model claude-haiku-4-5-20251001` |
| Feature implementation, review | Sonnet 4.6 (default) | `/model claude-sonnet-4-6` |
| Architecture, complex reasoning | Opus 4.8 | `/model claude-opus-4-8` |
| Long research + synthesis | Opus 4.8 | `/model claude-opus-4-8` |

Switch back after heavy tasks: `/model claude-sonnet-4-6`

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

---

## Quick Reference Card

```
DAILY                          WHEN STUCK
/cost        → check budget    /clear      → fresh start
/compact     → trim context    /help       → list commands
/model       → switch model    /doctor     → fix install

CODE QUALITY                   AUTOMATION
/code-review → find bugs       /loop       → repeat task
/simplify    → clean up code   /schedule   → cloud cron
/verify      → test the change /update-config → edit settings
/security-review → audit PR

SHELL ESCAPE                   CONTEXT TIPS
! git log    → git in session  Read specific line ranges
! npm test   → run tests       /compact before switching tasks
! cat file   → read into ctx   State file:line in prompts
```

---

*Last updated: 2026-06-30*
