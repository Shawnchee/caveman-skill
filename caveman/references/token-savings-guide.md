# Token Savings Guide

## Why It Matters

Every token costs money, burns quota, and slows response time. Output tokens are the primary cost driver — models charge more for them than input, and they accumulate fast across a long session.

Caveman mode targets output token waste: the filler, narration, and ceremony that add length without adding value.

## The Math

A typical "normal mode" response to "find test files":

```
I'd be happy to help! Let me search for test files in your project.

I found the following test files:
- src/__tests__/auth.test.ts
- src/__tests__/api.test.ts

Would you like me to look at any of these in detail?
```

~55 tokens.

Caveman equivalent:

```
- src/__tests__/auth.test.ts
- src/__tests__/api.test.ts
```

~15 tokens. **~73% reduction on that response.**

Filler phrases ("I'd be happy to help!", "Let me...", "Would you like...") typically add 20–40 tokens per response. Over a 50-turn session, that's 1,000–2,000 wasted output tokens before any real work is counted.

### Output vs. Total Session

Output tokens are a fraction of total context, but they compound:

- Every output token you generate becomes an input token in the next turn (it's in the conversation history)
- Verbose responses bloat the rolling context window
- A 50-turn verbose session can carry 10,000+ tokens of accumulated filler that must be re-processed each turn

Cutting output waste shrinks the session context, reducing input costs too.

### Rough numbers (illustrative, not exact)

| Session type       | Output tokens saved | Context blowup avoided |
|--------------------|--------------------|-----------------------|
| 20-turn task       | ~600               | ~2,000 input tokens   |
| 50-turn deep work  | ~2,000             | ~8,000 input tokens   |
| 100-turn autopilot | ~4,500             | ~20,000 input tokens  |

Actual numbers depend on model, verbosity baseline, and task type.

## What Wastes the Most Tokens

Ranked by typical contribution:

1. **Acknowledgment openers** — "Sure!", "Great question!", "I'd be happy to help!" (~5–15 tokens each, every response)
2. **Narrating tool use** — "Let me read that file", "I'll search for..." (~10–20 tokens, often paired with actually doing the thing)
3. **Postamble** — "I've completed the task. Let me know if you need anything else!" (~15–25 tokens, every response)
4. **Restating the question** — Repeating back what the user said before answering (~20–50 tokens)
5. **Explaining the approach** before executing it (~30–80 tokens on complex tasks)
6. **Summarizing what was done** after doing it (~20–60 tokens)

## Tips for Maximizing Savings

**Cut ceremony, not content.** Never abbreviate code, errors, file paths, or factual output. Only cut prose wrapping.

**Front-load results.** Answer first, explain only if the result is non-obvious.

**Trust the user.** Skip "would you like me to..." — if they want something, they'll ask.

**Avoid redundant confirmation.** "Done." after completing a task is often fine. A paragraph recap is not.

**One-liners for simple results.** A file count, a path, a yes/no — one line, no elaboration.

**Let code be the answer.** A well-written function needs no prose introduction.

## What Caveman Mode Does NOT Save

Caveman mode is a prose discipline, not a content filter. It doesn't help with:

- Large file reads (input tokens — can't be avoided if you need the file)
- Long code generation (output tokens — necessary, not waste)
- Thinking/reasoning tokens (internal, not directly controllable)

The savings are real but bounded. Caveman mode eliminates waste; it doesn't compress necessary work.
