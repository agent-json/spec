# Contributing

Thanks for helping improve `agent-json`.

This repo is intentionally narrow in v1. The goal is a small, stable spec that’s easy for domain owners to publish and easy for agents to consume.

## What we’re looking for

The most valuable contributions are:
- **realistic examples** (`examples/.../agent.json`) with clear facts + evidence links
- **clarifications** to `SPEC.md` that reduce ambiguity
- **small schema improvements** that keep v1 simple and backward-compatible

## What we’re not looking for (yet)

Please avoid (for v1):
- broad “universal” schema expansion
- crypto signing / attestations / identity systems
- agent ranking, evaluation, or policy layers
- large field sets that are hard to implement

These may be discussed later, but v1 prioritizes adoption and simplicity.

## How to propose changes

1) **Open an issue first** (preferred), especially for new fields.
   - Explain the use-case in 2–3 sentences.
   - Include an example `agent.json` showing the change.
   - Include why existing fields are insufficient.

2) **PRs are welcome** once there’s alignment in the issue.

## PR guidelines

- Keep changes small and focused.
- Update `SPEC.md` and (if relevant) the JSON Schema in `schema/`.
- Add or update an example in `examples/` for any behavioral/spec change.
- Preserve backward compatibility whenever possible.

## Questions / discussion

If you’re unsure whether something fits v1, open an issue with a minimal example and we’ll discuss it there.
