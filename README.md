# Agent Operating Charter

A small, modular governance pack for coding agents. Drop it into any repo so agents share one lifecycle, validation ladder, and routing policy — without stuffing process into `AGENTS.md`.

## What’s in this repo

| Path | Purpose |
|------|---------|
| [`INSTALL_PROMPT.md`](INSTALL_PROMPT.md) | Paste into an agent chat in a **target** repo to install + configure the charter |
| [`seed/.agent_charter/`](seed/.agent_charter/) | Process files to copy into the target repo |
| [`templates/`](templates/) | Optional seed docs (AGENTS snippet, assumptions log, compare sheet, WP checklist) |
| [`examples/CONFIG.sample.md`](examples/CONFIG.sample.md) | Example filled config (fictional project) |

## Quick start

1. Open the target repository in your coding agent.
2. Paste the contents of [`INSTALL_PROMPT.md`](INSTALL_PROMPT.md) (everything below its horizontal rule).
3. Optionally prepend:

   ```text
   Template charter: https://github.com/asymetryk/agent-operating-charter
   ```

   or a local clone path to `seed/.agent_charter`.

4. Answer the SETUP questions; confirm; agent writes `.agent_charter/CONFIG.md` and a short pointer in `AGENTS.md`.

## Design principles

- **Modular:** Core / Design / Engineering / Routing are separate files.
- **Configured once:** Repo answers live in `CONFIG.md` (`setup_complete`).
- **Generic defaults:** Trackers, models, UAT hosts, and promote paths are CONFIG fields — not hard-coded vendors.
- **Optimistic concurrency** with an Assumptions Log and a circuit breaker.
- **North Star → code → validate** for UI; non-UI WPs can skip mockups.

## Precedence (in consuming repos)

1. Human message  
2. Repo `AGENTS.md`  
3. `.agent_charter/CONFIG.md`  
4. `.agent_charter/CHARTER_*.md`  
5. Named skills / tools  
6. Global agent defaults (e.g. `~/.codex/AGENTS.md` if present)

Conflicts → stop and ask.

## License

MIT — see [LICENSE](LICENSE).
