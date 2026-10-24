<p align="center">
  <img src="https://img.freepik.com/premium-photo/caveman-sitting-by-fire-inside-cave-sunset-high-resolution-high-quality_188161-10065.jpg?w=360" width="200" />
</p>

<h1 align="center">caveman-skill</h1>

<p align="center">
  <strong>shut up and code</strong>
</p>

<p align="center">
  <a href="https://github.com/Shawnchee/caveman-skill/stargazers"><img src="https://img.shields.io/github/stars/Shawnchee/caveman-skill?style=flat&color=yellow" alt="Stars"></a>
  <a href="https://github.com/Shawnchee/caveman-skill/commits/main"><img src="https://img.shields.io/github/last-commit/Shawnchee/caveman-skill?style=flat" alt="Last Commit"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/Shawnchee/caveman-skill?style=flat" alt="License"></a>
</p>

<p align="center">
  <a href="#install">Install</a> •
  <a href="#before--after">Before / After</a> •
  <a href="#benchmarks">Benchmarks</a> •
  <a href="#the-10-rules">Rules</a> •
  <a href="#why-this-works">Why</a>
</p>

---

A skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code), Cursor, Windsurf, Copilot, Codex, and 40+ other agents. Makes your AI stop narrating its life story and just give you the answer.

Your coding assistant wastes up to **61% of output tokens** on filler — greetings, play-by-play, summaries of what it just did, offers to do more. Caveman kills all of it. One install. Every session after.

## Before / After

<table>
<tr>
<td width="50%">

### Normal (85 tokens)

> "I'll search for all TypeScript test files in your project. Let me look through the codebase for files matching common test patterns.
>
> I found the following TypeScript test files:
> - src/\_\_tests\_\_/auth.test.ts
> - src/\_\_tests\_\_/api.test.ts
> - src/\_\_tests\_\_/utils.test.ts
>
> That's 3 test files total in src/\_\_tests\_\_/. Would you like me to look at any of these?"

</td>
<td width="50%">

### Caveman (26 tokens)

> ```
> - src/__tests__/auth.test.ts
> - src/__tests__/api.test.ts
> - src/__tests__/utils.test.ts
> ```

</td>
</tr>
<tr>
<td>

### Normal

> "I can see the error you're encountering. This is a TypeScript type error — the function expects a string but you're passing a number. Let me fix that for you.
>
> I've updated the code to cast the value to a string using `.toString()`. The error should be resolved now. Would you like me to run the tests to confirm?"

</td>
<td>

### Caveman

> "`userId` was number, param expects string. Cast added. Tests pass."

</td>
</tr>
<tr>
<td>

### Normal

> "Great question! I'll go ahead and update the timeout value for you. Let me open the config file and make that change.
>
> I've updated the timeout from 5000 to 10000 milliseconds in src/config.ts. This should resolve your issue. Let me know if you need anything else!"

</td>
<td>

### Caveman

> "`src/config.ts:14` — timeout: 5000 → 10000"

</td>
</tr>
</table>

**Same answer. Way less theatre.**

## Install

### Using [skills.sh](https://skills.sh) (recommended)

Works with 45+ agents. One command.

```bash
npx skills add Shawnchee/caveman-skill
```

```bash
# Global (all projects)
npx skills add Shawnchee/caveman-skill -g

# Specific agent
npx skills add Shawnchee/caveman-skill -a claude-code
npx skills add Shawnchee/caveman-skill -a cursor
npx skills add Shawnchee/caveman-skill -a windsurf

# CI-friendly (no prompts)
npx skills add Shawnchee/caveman-skill -g -a claude-code -y
```

### Manual

```bash
git clone https://github.com/Shawnchee/caveman-skill.git
```

Copy the skill file for your agent:

| Agent | Project | Global |
|-------|---------|--------|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Cursor | `.cursor/skills/` | `~/.cursor/skills/` |
| Windsurf | `.windsurf/skills/` | `~/.windsurf/skills/` |
| Codex / OpenCode | `.codex/skills/` | `~/.codex/skills/` |
| Gemini CLI | `.gemini/skills/` | `~/.gemini/skills/` |
| Copilot | `.github/copilot-instructions.md` | — |
| Antigravity | Project config directory | — |

```bash
# Example: Claude Code, project-level
cp -r caveman-skill/caveman .claude/skills/

# Example: Claude Code, global
cp -r caveman-skill/caveman ~/.claude/skills/
```

### Uninstall

```bash
npx skills remove caveman
# or: rm -rf .claude/skills/caveman
```

## Benchmarks

Token counts verified with tiktoken `cl100k_base`. Four standard tasks, measured honestly:

| Task | Normal | Caveman | Reduction |
|------|-------:|--------:|----------:|
| Web Search | 82 | 26 | **68%** |
| Code Edit | 192 | 96 | **50%** |
| File Exploration | 148 | 71 | **52%** |
| Q&A Explanation | 209 | 58 | **72%** |
| **Average** | **158** | **63** | **61%** |

**Estimated real-world session savings: 12–24%.** Input tokens don't change — this is the honest number, not a marketing number.

> [!NOTE]
> Caveman only targets output tokens — reasoning/thinking tokens are untouched. Brain same size. Mouth smaller.

Full benchmark data with before/after transcripts: [`benchmarks/data.md`](benchmarks/data.md)

## The 10 Rules

| # | Rule | What dies |
|---|------|-----------|
| 1 | No filler phrases | "I'd be happy to", "Sure!", "Great question" |
| 2 | Execute first, talk second | Pre-task narration |
| 3 | Be direct — fragments where clear | Unnecessary articles, pronouns |
| 4 | No meta-commentary | "I'm going to search for..." |
| 5 | No preamble | Restating the question |
| 6 | No postamble | "Let me know if you need anything else!" |
| 7 | No tool announcements | "Let me read that file" |
| 8 | Explain only when needed | Unsolicited tutorials |
| 9 | Code speaks | English wrappers around code blocks |
| 10 | Error = fix | Apologies, error narration |

### What Stays

Caveman cuts words, never facts.

| Content | Caveman touch? |
|---------|---------------|
| Code blocks | Never — full snippet, not summary |
| Error messages | Never — exact text |
| File paths | Never — exact path |
| Technical terms | Never — polymorphism stays polymorphism |
| Numbers, versions | Never — exact values |

### When Rules Bend

Caveman isn't stupid. Rules bend when clarity demands it:

- **Surprising result** → brief explanation ("Fixed — but note: this disables auth caching")
- **User asks why** → answer the question
- **Destructive action** → warn first ("Deletes all rows in `sessions`. No rollback. Proceed?")
- **Ambiguous plan** → clarify before executing

The test: would a senior engineer reading this miss something important? If yes, add words. If no, cut them.

## Why This Works

```
┌──────────────────────────────────────┐
│  OUTPUT TOKENS SAVED    ████████ 61% │
│  TECHNICAL ACCURACY     ████████ 100%│
│  FILLER ELIMINATED      ████████ YES │
│  BRAIN DAMAGE           ░░░░░░░░ 0%  │
└──────────────────────────────────────┘
```

LLMs default to polite and verbose. Every response starts with ceremony and ends with an encore. Caveman overrides that at the system level:

- **Filler tokens come first** — "I'd be happy to help" generates before the actual answer. Killing it saves tokens immediately.
- **Narration compounds** — announcing tools, summarizing results, and offering follow-ups each add zero-value tokens. Over 50 turns, that's 1,000–2,000 wasted tokens.
- **Context bloat** — every verbose output becomes input on the next turn. Terse responses keep the context window lean across the whole session.
- **Useful content is untouched** — code, paths, errors, explanations stay exactly the same. Only the wrapper shrinks.

## Supported Agents

| Agent | Config | Location |
|-------|--------|----------|
| Claude Code | SKILL.md (YAML frontmatter) | `.claude/skills/caveman/SKILL.md` |
| Cursor | Plain markdown | `.cursorrules` |
| Windsurf | Plain markdown | `.windsurfrules` |
| GitHub Copilot | Plain markdown | `.github/copilot-instructions.md` |
| Antigravity | Plain markdown | Project config directory |

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md). Keep it simple — these are markdown configs, not application code.

## License

MIT — free like open plain.
