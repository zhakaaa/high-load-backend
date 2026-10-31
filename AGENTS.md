# Repository Guidelines

## Project Structure & Module Organization

`SIS2_Pastebin_Step3.ipynb` contains the entire Python Pastebin prototype: configuration, Protocol Buffers contract, SQLite persistence, shared business logic, FastAPI REST endpoints, gRPC server, client examples, and functional checks. Keep cells in execution order and update adjacent Markdown explanations when behavior changes. There are no separate source, test, or asset directories.

Running the notebook creates `sis2_pastebin_runtime/` with `pastebin.proto`, generated Python stubs, and `pastebin.sqlite3`. Treat these as runtime artifacts; edit the notebook’s `PROTO` string rather than generated stubs.

## Build, Test, and Development Commands

Use Python 3.11+ and a local Jupyter kernel.

- `python3 -m pip install jupyterlab` installs the notebook interface if needed.
- `python3 -m jupyterlab SIS2_Pastebin_Step3.ipynb` opens the implementation.
- Run the dependency cell (`%pip install ...`) to install gRPC, Protocol Buffers tooling, FastAPI, Uvicorn, HTTPX, and Pydantic.
- Execute cells top to bottom to generate stubs, initialize storage, start both servers, and run checks. No separate build command exists.
- Run the final shutdown cell when finished; restart the kernel before a full rerun.

REST listens at `127.0.0.1:18080` with API documentation at `/docs`; gRPC uses `127.0.0.1:50071`.

## Coding Style & Naming Conventions

Use four-space indentation, `snake_case` for Python functions and variables, `PascalCase` for classes, and uppercase constants. Preserve Protocol Buffers RPC names such as `CreateSnippet` and `GetSnippet`. Keep validation and storage behavior in `PastebinService` so both transports share semantics. No formatter or linter configuration is present.

## Testing Guidelines

Notebook sections 6–7 use Python assertions, HTTPX, and FastAPI `TestClient`. Run both sections after implementation changes. Preserve checks for create/read, public URLs, idempotent retries, missing IDs, empty content, oversized payloads, and conflicting keys. Add assertions beside the relevant checks. No standalone test framework or coverage threshold is configured; timeout/retry tests and benchmarks remain planned work.

## Commit & Pull Request Guidelines

No Git metadata is available here to establish commit conventions. Use concise imperative messages, such as `Add TTL boundary checks`. PR descriptions should explain behavior changes, identify affected notebook sections, and report checks actually run. Exclude generated stubs, databases, and sensitive notebook outputs.

## Assignment Constraints

The assignment specifies Java, while this prototype uses Python. Document that deviation and the rationale for comparing gRPC with REST. Preserve immutable snippets, the 1 MiB limit, and TTL bounds of 60 seconds–30 days. Local SQLite results do not establish production throughput or latency guarantees.
