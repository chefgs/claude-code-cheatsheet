# Claude Code Cheatsheet 🚀

A comprehensive quick-reference guide for [Claude Code](https://claude.ai/code) — Anthropic's AI-powered coding assistant. All commands, shortcuts, flags, prompting patterns, and workflows in one place.

---

## What's Inside

| Section | Description |
|---|---|
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
| **Quick Reference Card** | One-screen cheat card for daily use |

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

# Headless / CI
claude -p "/code-review" --dangerously-skip-permissions
```

### Security Audit in One Line

```bash
claude -p "/security-review" --dangerously-skip-permissions
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
