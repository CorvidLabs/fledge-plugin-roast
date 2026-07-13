---
module: roast
version: 1
status: active
files:
  - bin/roast

db_tables: []
depends_on: []
---

# Roast

## Purpose

Build an entertainment-focused prompt from a selected Git commit and delegate it to the developer's configured Fledge AI provider without changing the repository.

## Public API

| Surface | Behavior |
|---------|----------|
| commit argument | Select the Git commit-ish to include, defaulting to HEAD. |
| severity | Choose gentle, harsh, or brutal prompt tone. |
| show prompt | Print the generated prompt before delegation. |
| passthrough | Forward arguments after `--` to `fledge ask`. |

## Invariants

1. The selected commit-ish must resolve inside a Git worktree before AI invocation.
2. Severity accepts only gentle, harsh, or brutal.
3. The included diff is capped at 800 lines to bound model context.
4. The prompt includes author, short SHA, subject, and selected diff.
5. AI execution delegates to `fledge ask --no-spec-index` and inherits the configured provider.
6. Arguments after `--` are forwarded without being interpreted by the plugin.
7. The plugin performs no repository mutation.

## Behavioral Examples

```
Given a valid Git commit and configured Fledge AI provider
When the developer runs roast with a supported severity
Then the plugin builds the bounded commit prompt and delegates it to Fledge Ask
```

## Error Cases

| Error | When | Behavior |
|-------|------|----------|
| Not a Git worktree | Git context cannot be resolved | Report the repository requirement and exit 65. |
| Invalid commit-ish | The selected revision does not resolve | Report the invalid revision and exit 65. |
| Invalid severity | The severity is outside the supported set | Report valid choices and exit 64. |
| Unknown option | A plugin option is not recognized before `--` | Explain passthrough usage and exit 64. |
| AI provider failure | Fledge Ask cannot complete | Propagate the delegated command's failure. |

## Dependencies

- Bash
- Git
- Fledge Ask with a configured AI provider

## Change Log

| Version | Date | Changes |
|---------|------|---------|
| 1 | 2026-07-12 | Document existing bounded prompt and Fledge Ask delegation behavior for SpecSync 5 adoption. |
