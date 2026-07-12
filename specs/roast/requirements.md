---
spec: roast.spec.md
---

## User Stories

- As a developer, I want an optional humorous critique of a selected commit through my configured AI provider.

## Acceptance Criteria

### REQ-roast-001

The plugin SHALL validate Git context and the selected commit before constructing or sending a prompt.

### REQ-roast-002

The prompt SHALL include commit identity and at most 800 diff lines.

### REQ-roast-003

Gentle, harsh, and brutal SHALL select their documented tone, while any other severity fails before AI invocation.

### REQ-roast-004

The plugin SHALL delegate through the configured Fledge Ask provider with spec indexing disabled.

### REQ-roast-005

Arguments after `--` SHALL pass through to Fledge Ask and the plugin SHALL not mutate repository state.

## Constraints

- Output is entertainment-oriented AI content and depends on the configured provider.

## Out of Scope

- Code-review approval, remediation advice, repository mutation, and provider configuration.
