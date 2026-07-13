---
spec: roast.spec.md
---

## Context

This small Bash plugin composes Git metadata with the existing Fledge AI surface rather than implementing a provider client.

## Related Modules

- Fledge Ask and AI provider configuration.
- Git commit inspection.

## Design Decisions

- Cap diff input to bound cost and context.
- Use explicit severity templates while leaving provider/model choice to Fledge.
