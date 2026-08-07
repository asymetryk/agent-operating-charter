# Install prompt — paste into a target repo agent chat

**How to use:** Open the **target** repository (the product repo, not this template). Paste **everything below the line** as the first message.

Optional first line:

```text
Template charter: https://github.com/asymetryk/agent-operating-charter
```

Or a local path to a clone’s `seed/.agent_charter` directory.

---

Act as Principal System Architect. Your only job this turn is to **bootstrap this repository’s AI Agent Governance Framework** under `.agent_charter/`.

Do **not** implement product features, deploy, or refactor app code unless required to create the charter files.

## A. Outcomes (all required)

1. `.agent_charter/` exists with the modular charter pack (§B).
2. You ran first-run **SETUP** (ask the human; do not invent blocking answers).
3. You ran the **mismatch audit** against this repo’s `AGENTS.md`, any global agent defaults file, and deploy/UAT docs.
4. `.agent_charter/CONFIG.md` is filled; set `setup_complete: true` **only after the human confirms**.
5. Repo `AGENTS.md` has a short **Agent Charter** pointer (no duplicated lifecycle board).
6. List created/updated paths + a 5-line CONFIG summary, then **stop**.

## B. Charter pack to install

Copy these files from the template’s `seed/.agent_charter/` (or clone of this repo):

| File | Role |
|------|------|
| `README.md` | Entry protocol + precedence |
| `SETUP.md` | First-run questions + mismatch audit |
| `CONFIG.example.md` | Blank template |
| `CHARTER_CORE.md` | Lifecycle, assumptions, circuit breaker |
| `CHARTER_DESIGN.md` | North Star / UI pipeline |
| `CHARTER_ENGINEERING.md` | Fencing, validation, merge, UAT |
| `CHARTER_ROUTING.md` | Model / skill / parent-worker routing |

Then create `CONFIG.md` from `CONFIG.example.md` using SETUP answers.

**Do not** copy a filled example `CONFIG` from another product repo. Start from `CONFIG.example.md`.

If cloning from GitHub:

```bash
git clone --depth 1 https://github.com/asymetryk/agent-operating-charter /tmp/agent-operating-charter
cp -R /tmp/agent-operating-charter/seed/.agent_charter/. ./.agent_charter/
```

Optional: copy useful seeds from the template’s `templates/` (assumptions log, compare sheet, AGENTS snippet) into `docs/` or the tracker — ask before inventing paths.

## C. Proposed defaults (human may override)

Present as **proposed** in one SETUP batch:

### Trackers
- Primary project WP tracker: as configured (commonly OpenProject, Linear, Jira, GitHub Issues, etc.)
- Optional secondary tracker for non-project adhoc/reminders (if the team uses one)

### Models / routing
- Fill from `CHARTER_ROUTING.md` examples + human preference
- Image/mockups: use the path named in CONFIG; do not silently use undeclared providers
- Parent agent keeps merge / DoD / integration judgment

### Viewport
- Project-specific; default when unspecified: **`1920x1080`**
- `primary_viewport` = screenshot resolution (not the UAT host machine)

### UAT / promote
- Prefer a shared UAT host/runtime over laptop localhost when the team has one
- If UAT slots can be busy: prefer **`spin_new`** (provision another runtime) over waiting
- Document promote order in CONFIG (e.g. UAT → preview → production)
- Preview/staging is not a substitute for UAT unless waived in CONFIG

### Other
- Browser: Chrome unless overridden
- If `graft/` exists → `graft_required: true`
- Self-improvement / learnings: **`on_commit`** (not every coding turn)
- Commit only when the human explicitly asks (unless CONFIG says otherwise)
- Non-UI WPs: skip Mocked Up
- Circuit breaker: 2 consecutive validation or human-review failures → halt

## D. Execution steps

1. Detect repo state (`AGENTS.md`, existing `.agent_charter/`, `graft/`, deploy docs).
2. Install/refresh charter files from template; do not overwrite `CONFIG.md` with `setup_complete: true` unless re-setup was requested.
3. Ask SETUP questions in one batch (prefill §C as proposed).
4. Run mismatch audit; show Pass/Fail table; resolve blockers with the human.
5. Write `CONFIG.md`; lock only after confirmation (`uat_url_or_path: PENDING` allowed if policy is otherwise set).
6. Wire a short Agent Charter section into `AGENTS.md` (see seed `README.md` / `templates/AGENTS.snippet.md`).
7. Confirm with `ls .agent_charter/`, summarize CONFIG, **stop**.

## E. Precedence

1. Human message  
2. Repo `AGENTS.md`  
3. `.agent_charter/CONFIG.md`  
4. `.agent_charter/CHARTER_*.md`  
5. Named skills  
6. Global agent defaults  

Conflicts → stop and ask.

## F. Out of scope

App feature coding, production deploys, unrelated refactors, deleting tools/skills, or changing other repositories.
