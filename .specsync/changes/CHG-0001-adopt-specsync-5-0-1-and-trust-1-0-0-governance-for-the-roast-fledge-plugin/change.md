---
id: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-roast-fledge-plugin
state: draft
type: migration
base_commit: c460c7a07018000b4896f8ef923c93c59c27712b
---

# Adopt SpecSync 5.0.1 and Trust 1.0.0 governance for the Roast Fledge plugin

## Intent

Adopt SpecSync 5.0.1 and Trust 1.0.0 governance for the Roast Fledge plugin

## Affected Canonical Specs

- `roast`

## Acceptance Criteria

- SpecSync strict checks pass at explicit advisory threshold 0 for the extensionless Bash executable; all four integrations are installed; Trust doctor and verification pass; ShellCheck
- syntax
- help
- invalid-severity
- invalid-commit
- and manifest checks remain green.

## No-spec Rationale

Not applicable
