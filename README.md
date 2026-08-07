# Agent Operating Charter

Modular governance for coding agents: one lifecycle, North Star design gate, validation ladder, and routing policy — configured once per repo.

---

## Install (this is the whole UX)

1. Open your **product** repository in your coding agent.
2. Paste **only** this link (or the one-liner under it):

**https://github.com/asymetryk/agent-operating-charter**

```text
Install the Agent Operating Charter from https://github.com/asymetryk/agent-operating-charter into this repo and run the intake wizard.
```

3. Answer the intake questions; confirm; done.

The agent should fetch [`BOOTSTRAP.md`](BOOTSTRAP.md) and run the wizard — **no long prompt paste required**.

---

## What gets installed

| Path | Purpose |
|------|---------|
| [`BOOTSTRAP.md`](BOOTSTRAP.md) | Intake wizard (URL / one-liner entrypoint) |
| [`seed/.agent_charter/`](seed/.agent_charter/) | Files copied into the product repo as `.agent_charter/` |
| [`templates/`](templates/) | Optional seeds (AGENTS snippet, assumptions log, compare sheet, WP checklist) |
| [`examples/CONFIG.sample.md`](examples/CONFIG.sample.md) | Fictional filled config |
| [`INSTALL_PROMPT.md`](INSTALL_PROMPT.md) | Optional long-form fallback if the agent cannot fetch the web |

## Design principles

- **URL-first install** — link kicks off intake; CONFIG is filled by wizard.
- **Modular** — Core / Design / Engineering / Routing.
- **Generic** — trackers, models, UAT, promote paths are CONFIG fields.
- **Optimistic concurrency** with Assumptions Log + circuit breaker.
- **North Star → code → validate** for UI; non-UI WPs can skip mockups.

## Precedence (in consuming repos)

1. Human message  
2. Repo `AGENTS.md`  
3. `.agent_charter/CONFIG.md`  
4. `.agent_charter/CHARTER_*.md`  
5. Named skills / tools  
6. Global agent defaults (if any)

Conflicts → stop and ask.

## License

MIT — see [LICENSE](LICENSE).
