# Intake wizard — Agent Operating Charter

> **Trigger:** The human gave you this repository’s URL (or said to install/bootstrap the Agent Operating Charter from it).  
> **Workspace:** Install into the **currently open product repository**, not into this template repo (unless the open workspace *is* this template and they asked to work on the template itself).

Do **not** wait for a long pasted prompt. Fetch this file + `seed/.agent_charter/` and run the wizard now.

---

## Immediate actions

1. Confirm the open workspace root (product repo). If unclear, ask once: “Install charter into which repo path?”
2. Materialize the current seed process files **before** evaluating config or running migrations:

```bash
TMP=$(mktemp -d)
git clone --depth 1 https://github.com/asymetryk/agent-operating-charter "$TMP/aoc"
mkdir -p .agent_charter
# Refresh process files; CONFIG.md is not part of the seed and must be preserved
cp -R "$TMP/aoc/seed/.agent_charter/." .agent_charter/
rm -rf "$TMP"
```

   Prefer copying from a local clone of this repo if the human provided a path.

3. Inspect `.agent_charter/CONFIG.md` using the newly installed `SETUP.md`:
   * If `setup_complete: true` **and** `charter_version: 2` (or newer), and re-setup was not requested → the process-file refresh is complete; show the current CONFIG summary and stop.
   * If `charter_version` is missing or below `2`, run the v2 migration. Preserve confirmed values. Map legacy `wp_status_location` only when legacy `wp_status_authority` was OpenProject; otherwise ask for the required OpenProject project and preserve the old tracker only if the human designates it for non-project use.
4. Read `.agent_charter/SETUP.md` and ask **all §1 questions in one batch**, including the OpenProject project/wiki and Buzz channel locations, labeling defaults as **proposed**. During migration, preserve confirmed values and ask only for missing or contradictory answers.
5. Run **SETUP §2 mismatch audit** against this repo’s `AGENTS.md`, global agent defaults (if any), and deploy/UAT docs. Show a Pass/Fail table.
6. Verify that the configured OpenProject project, Wiki, Bootstrap page, and Buzz project channel exist and are reachable. After obtaining action-time human confirmation for external mutations, create missing surfaces and populate or reconcile the Bootstrap page with the minimum shared context in `CHARTER_CORE.md` §4. A missing, empty, or stale required surface leaves setup incomplete.
7. Write `.agent_charter/CONFIG.md` with `charter_version: 2` and `setup_complete: true` only after step 6 passes; wire the short Agent Charter pointer into `AGENTS.md` (see `templates/AGENTS.snippet.md`).
8. Offer `templates/*` as additional OpenProject Wiki content seeds (assumptions log and WP checklist) and copy visual comparison assets into `docs/` when appropriate; do not invent paths.
9. List `.agent_charter/`, print a concise CONFIG summary including OpenProject and Buzz locations, **stop**. Do not start feature work unless asked.

---

## Proposed defaults (override per repo)

| Topic | Proposed |
|-------|----------|
| Work packages | OpenProject |
| Shared agent knowledge | OpenProject Wiki, including a Bootstrap page |
| Discussion | One Buzz project channel; one thread per OpenProject WP |
| Viewport | `1920x1080` (project-specific later) |
| Browser | Chrome |
| UAT busy policy | `spin_new` when a shared UAT exists |
| Localhost default | `false` when shared UAT exists |
| Self-improvement | `on_commit` |
| Non-UI Mocked Up | skip |
| Circuit breaker | 2 strikes |
| Imagegen | only the path declared in CONFIG |

OpenProject project/wiki locations, Bootstrap page, Buzz channel, models, UAT host URL, promote order, and test commands are **required human answers** (or explicit acceptance of a proposed value).

---

## Out of scope

Product feature coding, production deploys, rewriting unrelated docs, or modifying other repos.
