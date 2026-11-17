# Claude Code Cheatsheet 🚀

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/chefgs/claude-code-cheatsheet?style=social)](https://github.com/chefgs/claude-code-cheatsheet/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/chefgs/claude-code-cheatsheet?style=social)](https://github.com/chefgs/claude-code-cheatsheet/network/members)
[![GitHub issues](https://img.shields.io/github/issues/chefgs/claude-code-cheatsheet)](https://github.com/chefgs/claude-code-cheatsheet/issues)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/chefgs/claude-code-cheatsheet/pulls)
[![Last Commit](https://img.shields.io/github/last-commit/chefgs/claude-code-cheatsheet)](https://github.com/chefgs/claude-code-cheatsheet/commits/main)
[![Node.js >= 18](https://img.shields.io/badge/node-%3E%3D18-brightgreen.svg)](https://nodejs.org/)

A comprehensive quick-reference guide for [Claude Code](https://claude.ai/code) — Anthropic's AI-powered coding assistant. All commands, shortcuts, flags, prompting patterns, and workflows in one place.

---

## Table of Contents

- [What's Inside](#whats-inside)
- [Quick Install](#quick-install)
- [How to Use](#how-to-use)
- [Highlights](#highlights)
  - [Code Review — One Command](#code-review--one-command)
  - [Security Audit in One Line](#security-audit-in-one-line)
  - [Background Agent — Fire and Forget](#background-agent--fire-and-forget)
  - [Pipe Logs Into Claude](#pipe-logs-into-claude)
- [Working Practices for Long Sessions](#working-practices-for-long-sessions)
- [Contributing](#contributing)
- [License](#license)

---

## What's Inside

| Section | Description |
|---|---|
| **Installation & Access Methods** | Terminal/CLI, VS Code extension, desktop app, and mobile app — with install steps and a comparison table |
| **Built-in Slash Commands** | `/clear`, `/compact`, `/model`, `/plan`, and every other built-in command, tiered by frequency |
| **Skills (Agent Commands)** | `/code-review`, `/security-review`, `/ultrareview`, `/verify`, `/simplify`, and more |
| **Keyboard Shortcuts** | Terminal key bindings for faster navigation and control |
| **`!` Shell Escape** | Run shell commands and pipe output directly into your session |
| **CLI Commands** | Headless mode, session management, code/security review automation, and useful flags |
| **`@` Mentions** | Attach files, directories, or URLs to context without pasting |
| **Prompt Best Practices** | Scope, output format, file:line references, iterative refinement |
| **Context & Token Usage** | Budget tips, model selection, smart context loading |
| **Effective Prompting Patterns** | 3-part task structure, defensive prompts, parallel research, extended thinking |
| **Background Agents & Multi-Agent** | Concurrent workflows, session management, concurrency controls |
| **MCP (Model Context Protocol)** | Configuring and using MCP servers |
| **Hooks System** | Intercept tool calls with custom scripts |
| **CLAUDE.md — Project Memory** | Auto-loaded project context, memory scopes, imports |
| **Working Practices for Long Sessions** | Why `CLAUDE.md` rules decay as a session grows and which mechanisms are actually enforced, consent semantics, when to `/clear` vs `/compact`, and verification habits |
| **Quick Reference Card** | One-screen cheat card for daily use |

---

## Quick Install

```bash
# 1. Install the CLI (Node.js 18+ required)
npm install -g @anthropic-ai/claude-code

# 2. Authenticate
claude login

# 3. Start in your project
cd my-project && claude
```

For VS Code, desktop app, and mobile installation see the **[Installation & Access Methods](./claude-code-cheatsheet.md#installation--access-methods)** section of the cheatsheet.

---

## How to Use

Open [`claude-code-cheatsheet.md`](./claude-code-cheatsheet.md) in any Markdown viewer, or clone and view locally:

```bash
git clone https://github.com/chefgs/claude-code-cheatsheet.git
cd claude-code-cheatsheet
# Open in VS Code
code claude-code-cheatsheet.md
```

You can also paste the cheatsheet directly into a Claude Code session to give Claude full awareness of available commands:

```
@claude-code-cheatsheet.md
"Use the relevant commands from the cheatsheet to review and improve this PR."
```

---

## Highlights

### Code Review — One Command

```bash
# Interactive (inside Claude Code session)
/code-review --fix       # review AND auto-fix

# Headless / one-shot
claude -p "/code-review"
```

### Security Audit in One Line

```bash
claude -p "/security-review"
```

### Background Agent — Fire and Forget

```bash
claude --bg "Run the full test suite and fix any failing tests"
claude agents           # check status
claude attach <id>      # re-attach when done
```

### Pipe Logs Into Claude

```bash
cat error.log | claude -p "Diagnose this error and suggest a fix"
```

---

## Contributing

Contributions are welcome! If you know a command, flag, or pattern that's missing:

1. Fork the repository
2. Edit `claude-code-cheatsheet.md`
3. Open a pull request with a clear description of what you added or changed

Please keep additions concise and use the existing table/code-block style.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

*Last updated: 2026-08-03*
