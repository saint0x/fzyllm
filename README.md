# fzyllm

`fzyllm` is a small agentic runtime written in fzy (fozzylang) as a public exhibition project.

The point is not the app itself. The point is showing what fzy (fozzylang) feels like in a real, running system.

## Why this project exists

This repo demonstrates that fzy (fozzylang) can handle production-shaped service code with clean structure, deterministic tooling, and practical networking/runtime behavior.

## Language features demonstrated

- Module-oriented architecture across runtime, services, model, api, and cli layers
- Type-safe function boundaries and explicit contracts between components
- Concurrency and scheduling primitives in a runtime context
- Native `async`/`await` protocol paths for provider I/O orchestration
- Explicit `match`-based state/failure mapping in runtime domain models
- Deadline and cancellation markers (`timeout`, `deadline`, `cancel`) in request paths
- Native HTTP/server flows and provider integration in language-level code
- Structured logging and operational visibility from fzy (fozzylang) code paths

## How the language maps to the runtime

- `src/main.fzy` wires a full boot path (config -> services -> runtime -> serve)
- `src/services/*` shows request handling, provider calls, and tool/session plumbing
- `src/runtime/*` demonstrates supervision, limits, failure handling, and worker orchestration
- `src/model/*` keeps app state/contracts explicit and inspectable

## Local run

```bash
cp .env.example .env
# set ANTHROPIC_API_KEY in .env

fz check
fz build
fz test
fz run
```

Default listen address is `127.0.0.1:8787`.

## Notes

- Secrets are env-driven (`ANTHROPIC_API_KEY`) and `.env` is gitignored.
- This repo is intentionally small and focused: it is an exhibition of fzy (fozzylang) in action.
