# Long-form install prompt (fallback)

**Prefer URL install:** in the product repo, paste only:

https://github.com/asymetryk/agent-operating-charter

…or:

```text
Install the Agent Operating Charter from https://github.com/asymetryk/agent-operating-charter into this repo and run the intake wizard.
```

The agent should follow [`BOOTSTRAP.md`](BOOTSTRAP.md). Use this file only if the agent cannot fetch GitHub / the bootstrap doc.

---

Act as Principal System Architect. Bootstrap `.agent_charter/` in the **currently open product repository** using https://github.com/asymetryk/agent-operating-charter (`seed/.agent_charter/` + `BOOTSTRAP.md` + `SETUP.md`).

1. Clone or fetch the template; copy `seed/.agent_charter/` → `./.agent_charter/` (do not clobber a locked CONFIG unless re-setup was requested).
2. Run the intake wizard in `BOOTSTRAP.md` / `SETUP.md` (one question batch + mismatch audit).
3. After human confirm: write `CONFIG.md` with `setup_complete: true`, wire `AGENTS.md` snippet, summarize, stop.
4. Do not implement product features this turn.
