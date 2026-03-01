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
- Trait + generic polymorphism with explicit specialization and concrete impl dispatch
- Explicit `match`-based state/failure mapping in runtime domain models
- Closure/lambda values with lexical capture in deterministic language-surface tests
- Native array/index expression paths exercised in deterministic language-surface tests
- Import metadata surface demonstrated with `use ... as alias` and `pub use ...`
- Production loop/control primitives (`loop`, `for-in` ranges, `break`, `continue`) in runtime/test paths
- Full statement-as-expression surface (`if`, `match`, `loop`, `break <expr>`, `discard`) in deterministic language tests
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

fz check . --json
fz build . --backend cranelift --json
fz build . --release --backend llvm --json
fz audit unsafe . --workspace --json
fozzy doctor --deep --scenario .fz/det/main.det.fozzy.json --runs 5 --seed 4242 --json
fozzy test --det --strict .fz/det/main.det.fozzy.json --json
fz test . --det --strict-verify --seed 4242 --record artifacts/anthropic_smoke.det.trace.fozzy --json
fz run . --backend cranelift --json
fozzy trace verify artifacts/anthropic_smoke.det.trace.fozzy --strict --json
fozzy replay artifacts/anthropic_smoke.det.trace.fozzy --json
fozzy ci artifacts/anthropic_smoke.det.trace.fozzy --json
```

Default listen address is `127.0.0.1:8787`.

## Notes

- Secrets are env-driven (`ANTHROPIC_API_KEY`) and `.env` is gitignored.
- Unsafe audit now emits unsafe inventory/docs artifacts under `.fz/` (JSON + Markdown + HTML).
- Strict unsafe policy for CI is opt-in with `FZ_UNSAFE_STRICT=1`.
- `src/tests/smoke.fzy` exercises first-class unsafe semantics in `det_language_surface` (`unsafe fn` + `unsafe { ... }`).
- `src/tests/smoke.fzy` also exercises production trait/generic semantics (`trait`, concrete `impl`, `fn<T: ...>`, explicit specialization, and `Type.method(...)` dispatch).
- Macro/attribute baseline used in this repo is constrained to supported attributes (`#[repr(...)]`, `#[ffi_panic(...)]` where applicable).
- This repo is intentionally small and focused: it is an exhibition of fzy (fozzylang) in action.
