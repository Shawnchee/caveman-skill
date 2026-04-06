# caveman-skill

Make your AI coding assistant shut up and save tokens.

AI coding assistants waste up to 75% of output tokens on filler text — "I'd be happy to help!", "Let me search for that...", summaries of what they just did. **Caveman mode** makes them terse, saving real tokens and real money.

## Quick Start

### Claude Code

```bash
# From your project root:
mkdir -p .claude/skills
cp claude-code/caveman.md .claude/skills/caveman.md
```

Then say **"caveman mode"** in chat to activate.

The skill file uses Claude Code's [SKILL.md format](https://docs.anthropic.com/en/docs/claude-code/skills) with a `trigger` field — Claude reads it automatically when you say the trigger phrase.

### Cursor

```bash
# From your project root:
cp cursor/.cursorrules-caveman .cursorrules
```

Cursor reads `.cursorrules` from the project root on every interaction. No activation step needed.

### Windsurf

```bash
# From your project root:
cp windsurf/.windsurfrules-caveman .windsurfrules
```

Windsurf reads `.windsurfrules` from the project root on every interaction. No activation step needed.

### GitHub Copilot

```bash
# From your project root:
mkdir -p .github
cp copilot/caveman-instructions.md .github/copilot-instructions.md
```

Copilot reads `.github/copilot-instructions.md` as custom instructions for your repository. Works in VS Code, JetBrains, and GitHub.com.

### Antigravity

```bash
# Copy to your project's config directory:
cp antigravity/caveman-instructions.md <your-project-config-dir>/caveman-instructions.md
```

Refer to Antigravity's documentation for the exact config path in your project.

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
| Claude Code | SKILL.md with YAML frontmatter | `.claude/skills/caveman.md` |
| Cursor | Plain markdown | `.cursorrules` (project root) |
| Windsurf | Plain markdown | `.windsurfrules` (project root) |
| GitHub Copilot | Plain markdown | `.github/copilot-instructions.md` |
| Antigravity | Plain markdown | Project config directory |

## License

MIT
