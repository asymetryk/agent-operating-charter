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

1. Clone or fetch the current template; copy `seed/.agent_charter/` → `./.agent_charter/`. Preserve the existing `CONFIG.md`.
2. Inspect `charter_version`. For an explicit re-setup request, ask the full SETUP §1 question batch so existing choices can be replaced. Otherwise run the v2 migration when required and ask only for missing or contradictory values. Always run the blocking mismatch audit.
3. After action-time human confirmation for external mutations, verify or provision the OpenProject project/Wiki/Bootstrap page and Buzz project channel. Populate or reconcile the Bootstrap page with `CHARTER_CORE.md` §4 minimum shared context; missing, unreachable, empty, or stale surfaces block completion.
4. Only after those gates pass, write `CONFIG.md` with `charter_version: 2` and `setup_complete: true`, wire the `AGENTS.md` snippet, summarize the OpenProject/Buzz locations, and stop.
5. Do not implement product features this turn.
