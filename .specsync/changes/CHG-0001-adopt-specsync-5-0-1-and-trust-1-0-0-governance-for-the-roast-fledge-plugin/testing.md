---
change: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-roast-fledge-plugin
artifact: testing
---

# Testing

Local acceptance requires the six-step Fledge lane, strict SpecSync checks at threshold 0, all four integrations, healthy Trust doctor, and a clean diff.

Hosted acceptance requires the new `trust` job plus existing ShellCheck and help smoke to pass. Live provider output is intentionally not a deterministic CI requirement.
