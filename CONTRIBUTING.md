# Contributing

Thanks for your interest in improving caveman-skill.

## Adding a New IDE

1. Create a directory named after the IDE (e.g., `zed/`)
2. Add a caveman instructions file using that IDE's config format
3. Keep the 10 rules identical to the existing files — only the format/frontmatter should differ
4. Add the IDE to the "Supported IDEs" table in README.md and a Quick Start section
5. Open a PR

## Updating the Rules

The rules should stay consistent across all IDE files. If you change a rule:

1. Update `caveman/SKILL.md` first (this is the canonical source)
2. Apply the same change to all other IDE files
3. If the change affects response style, re-run the benchmarks

## Benchmarks

Token counts in `benchmarks/data.md` are verified with tiktoken `cl100k_base`. To re-run:

```bash
pip install tiktoken
python count_tokens.py  # or write your own script against the response text
```

If you add new benchmark tasks:
- Include the exact prompt
- Show normal and caveman responses
- Count tokens with `cl100k_base`, not estimates
- Update the summary table and README

## Style

- Keep files simple — these are markdown configs, not application code
- No build steps, no dependencies, no tooling
- PRs should be small and focused
