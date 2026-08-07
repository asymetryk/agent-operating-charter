# Intake wizard — Agent Operating Charter

> **Trigger:** The human gave you this repository’s URL (or said to install/bootstrap the Agent Operating Charter from it).  
> **Workspace:** Install into the **currently open product repository**, not into this template repo (unless the open workspace *is* this template and they asked to work on the template itself).

Do **not** wait for a long pasted prompt. Fetch this file + `seed/.agent_charter/` and run the wizard now.

---

## Immediate actions

1. Confirm the open workspace root (product repo). If unclear, ask once: “Install charter into which repo path?”
2. If `.agent_charter/CONFIG.md` exists with `setup_complete: true` and they did not ask to re-run setup → show current CONFIG summary and stop (or ask whether to re-run).
3. Materialize seed files:

```bash
TMP=$(mktemp -d)
git clone --depth 1 https://github.com/asymetryk/agent-operating-charter "$TMP/aoc"
mkdir -p .agent_charter
# Refresh process files; do not clobber a locked CONFIG unless re-setup was requested
cp -R "$TMP/aoc/seed/.agent_charter/." .agent_charter/
rm -rf "$TMP"
# If CONFIG.md was overwritten from example, keep setup_complete: false until wizard finishes
```

   Prefer copying from a local clone of this repo if the human provided a path.

4. Read `.agent_charter/SETUP.md` and ask **all §1 questions in one batch**, labeling defaults as **proposed** (see SETUP + README defaults).
5. Run **SETUP §2 mismatch audit** against this repo’s `AGENTS.md`, global agent defaults (if any), and deploy/UAT docs. Show a Pass/Fail table.
6. After the human confirms answers, write `.agent_charter/CONFIG.md`, set `setup_complete: true`, wire the short Agent Charter pointer into `AGENTS.md` (see `templates/AGENTS.snippet.md` in this repo).
7. Optionally offer to copy `templates/*` into `docs/` (assumptions log, compare sheet, WP checklist) — ask before inventing paths.
8. List `.agent_charter/`, print a 5-line CONFIG summary, **stop**. Do not start feature work unless asked.

---

## Proposed defaults (override per repo)

| Topic | Proposed |
|-------|----------|
| Viewport | `1920x1080` (project-specific later) |
| Browser | Chrome |
| UAT busy policy | `spin_new` when a shared UAT exists |
| Localhost default | `false` when shared UAT exists |
| Self-improvement | `on_commit` |
| Non-UI Mocked Up | skip |
| Circuit breaker | 2 strikes |
| Imagegen | only the path declared in CONFIG |

Trackers, models, UAT host URL, promote order, and test commands are **required human answers** (or explicit “use proposed X”).

---

## Out of scope

Product feature coding, production deploys, rewriting unrelated docs, or modifying other repos.
