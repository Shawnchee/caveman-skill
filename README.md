# caveman-skill

Make your AI coding assistant shut up and save tokens.

AI coding assistants waste up to 75% of output tokens on filler text — "I'd be happy to help!", "Let me search for that...", summaries of what they just did. **Caveman mode** makes them terse, saving real tokens and real money.

## Install

### Using [skills.sh](https://skills.sh) (recommended)

The easiest way — works with 45+ coding agents including Claude Code, Cursor, Windsurf, Codex, and more.

```bash
# Install to your project (team can use it too)
npx skills add Shawnchee/caveman-skill

# Install globally (available in all your projects)
npx skills add Shawnchee/caveman-skill -g

# Install to a specific agent only
npx skills add Shawnchee/caveman-skill -a claude-code
npx skills add Shawnchee/caveman-skill -a cursor
npx skills add Shawnchee/caveman-skill -a windsurf

# Preview what's available before installing
npx skills add Shawnchee/caveman-skill --list

# CI/CD-friendly (no prompts)
npx skills add Shawnchee/caveman-skill -g -a claude-code -y
```

### Manual install (any agent)

```bash
git clone https://github.com/Shawnchee/caveman-skill.git
```

Then copy the skill file to your agent's skills directory:

| Agent | Project-level | Global |
|-------|--------------|--------|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Cursor | `.cursor/skills/` | `~/.cursor/skills/` |
| Windsurf | `.windsurf/skills/` | `~/.windsurf/skills/` |
| Codex / OpenCode | `.codex/skills/` | `~/.codex/skills/` |
| Gemini CLI | `.gemini/skills/` | `~/.gemini/skills/` |
| Antigravity | Project config directory | — |

> **Note:** Skill directory paths may vary by agent version. Claude Code paths are verified; other agent paths follow the emerging SKILL.md standard and may need adjustment.

Example:

```bash
# Project-level (just this repo)
cp -r caveman-skill/caveman .claude/skills/

# Global (all your projects)
cp -r caveman-skill/caveman ~/.claude/skills/
```

The skill activates automatically once installed — your agent reads it on every interaction.

### Uninstall

```bash
# Via skills.sh
npx skills remove caveman

# Manual
rm -rf .claude/skills/caveman
```

## What It Does

Before (normal mode):
```
I'd be happy to help you with that! Let me search for the TypeScript test files
in your project. I found the following TypeScript test files:
- src/__tests__/auth.test.ts
- src/__tests__/api.test.ts
- src/__tests__/utils.test.ts

These are located in the __tests__ directory. Would you like me to look at any
of these files in more detail?
```

After (caveman mode):
```
Found 3 test files:
- src/__tests__/auth.test.ts
- src/__tests__/api.test.ts
- src/__tests__/utils.test.ts
```

Same information. 61% fewer output tokens.

## Benchmark Results

Token counts verified with tiktoken `cl100k_base`. Measured across 4 standard tasks:

| Task | Normal | Caveman | Reduction |
|------|--------|---------|-----------|
| Web Search | 82 | 26 | 68% |
| Code Edit | 192 | 96 | 50% |
| File Exploration | 148 | 71 | 52% |
| Q&A | 209 | 58 | 72% |
| **Average** | **158** | **63** | **61%** |

**Estimated total session savings**: 12-24% (input tokens don't change — this is the honest real-world number).

Full benchmark data with before/after examples: [`benchmarks/data.md`](benchmarks/data.md)

## The 10 Rules

1. No filler phrases ("I'd be happy to", "Sure!", "Let me")
2. Execute first, talk second
3. Be direct — short sentences, fragments where clear
4. No meta-commentary about what you're doing
5. No preamble or restating the question
6. No postamble or "anything else?"
7. No tool announcements — just use tools silently
8. Explain only when needed
9. Code speaks — show code, skip the wrapper
10. Error = fix, don't apologize

## Why This Works

LLMs default to being polite and verbose. A system-level instruction overriding this works because:

- **Filler comes first** — the model produces "I'd be happy to help" before the actual answer. Suppressing it saves tokens immediately.
- **Narration compounds** — announcing tool use, summarizing results, offering follow-ups each add zero-value tokens.
- **Useful content stays the same** — code, file paths, and explanations don't change. Only the wrapper shrinks.

## Supported IDEs

| IDE | Config Format | Config Location |
|-----|---------------|-----------------|
| Claude Code | SKILL.md with YAML frontmatter | `.claude/skills/caveman/SKILL.md` |
| Cursor | Plain markdown | `.cursorrules` (project root) |
| Windsurf | Plain markdown | `.windsurfrules` (project root) |
| GitHub Copilot | Plain markdown | `.github/copilot-instructions.md` |
| Antigravity | Plain markdown | Project config directory |

## License

MIT
