# artifact_types — Shared Type Registry

Single source of truth for the artifact-type vocabulary used by both the
parallax daemon (tier classification) and the doc-provenance module
(authority validation).

## Purpose

Adding a type once in `artifact_types.json` registers it in both systems.
Before this registry, adding `proposal` required editing both the daemon's
`DEFAULTS` and the checker's `TYPE_TO_AUTHORITY` — and the two lists were
already drifting (`backlog` in one, `backlog` in another).

## Future

This directory is designed to be extracted into its own submodule.
Parallax and doc-provenance will both consume it. The directory structure
is self-contained — no dependencies on parallax or doc-provenance internals.

## Amendment Process

1. Proposal committed by one team
2. Independent review by the other
3. Bilateral agreement + version bump
4. Both systems pick up the change from the registry

## Schema

Each type: `{description, default_tier: 1-4, default_authority: derived|structured|speculative}`.
`default_tier`: the tier the parallax daemon assigns (1=must-read, 2=should-read, 3=optional, 4=never-read).
`default_authority`: the authority level for doc-provenance validation (derived/structured/speculative).
Both are defaults — each consuming system may override per its own policy.
