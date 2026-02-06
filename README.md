# agent-json (proposal)

agent-json is a minimal, domain-hosted facts format for AI agents.

It lets a domain owner publish a small, canonical JSON file that agents can prefer over scraped or inferred claims.

## The problem

Agents answer questions by stitching together:
- web pages
- docs
- third-party summaries
- cached snippets

This often produces confident, wrong, or outdated statements because the “ground truth” is scattered, ambiguous, or missing.

Domain owners don’t have a simple, standard place to publish the facts an agent should use.

## The proposal

A single machine-readable file hosted on the domain:

- `/.well-known/agent.json`

It contains a narrow set of domain-owner asserted facts plus links to supporting pages.

This repo provides:
- a v1 spec: [`SPEC.md`](./SPEC.md)
- examples: [`/examples`](./examples)
- optional validation tooling (future)

## Non-goals (v1)

agent-json does NOT try to:
- verify truth (it is domain-owner asserted)
- rank, compare, or recommend entities
- replace human-readable pages
- model every possible domain or industry
- require crypto signing or attestations in v1

## Who should care

- teams building browsing / procurement / support agents
- domain owners who want a canonical source for key facts
- tool builders who want a predictable “facts endpoint” to integrate

## Try it in 5 minutes

1) Open an example:
- [`examples/fictional/agent.json`](./examples/fictional/agent.json)

2) Publish on your domain:
- host at `/.well-known/agent.json`
- serve `Content-Type: application/json`

3) Verify it loads:
```bash
curl -s https://YOURDOMAIN.com/.well-known/agent.json | jq
