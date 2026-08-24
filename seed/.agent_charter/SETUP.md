# First-run setup & mismatch audit

Run once per repo, whenever `CONFIG.md` has `setup_complete: false`, or whenever `charter_version` is missing or below `2`. Ask the human; do not invent blocking answers. Provision and verify required collaboration surfaces before marking setup complete, then wire repo `AGENTS.md` (see §Wire).

---

## §0 Upgrade contract

Current config contract: `charter_version: 2`.

For an existing CONFIG with no version or a lower version:

1. Preserve confirmed repo-specific values and waivers.
2. If legacy `wp_status_authority` was OpenProject, map `wp_status_location` to `openproject_project`. Otherwise leave `openproject_project` unset, ask for the required OpenProject project, and preserve the old tracker only when the human designates it as `non_project_tracker`.
3. Validate every existing collaboration value against the v2 contract. `evidence_log` must be an OpenProject WP attachment/comment location or a page in the configured OpenProject Wiki; `assumptions_log` must be a page/section in that Wiki. Treat local repo paths, non-OpenProject URLs, and ambiguous legacy labels as missing, then collect replacements plus any missing `openproject_wiki`, `bootstrap_wiki_page`, or `buzz_channel` through §1.
4. Keep `setup_complete: false` until the §2 audit passes, the OpenProject project/wiki/Bootstrap page plus Buzz channel are verified reachable, and the Bootstrap page contains the current shared context required by `CHARTER_CORE.md` §4.

An old `setup_complete: true` does not bypass this migration.

## §1 Primary setup questions

Ask in one batch. Label suggested defaults as **proposed**.

### A. OpenProject and Buzz

1. **OpenProject project URL / id?** OpenProject is the authoritative project WP tracker.
2. **OpenProject Wiki URL / id, Bootstrap page, and pages/sections for evidence and assumptions?**
3. **Buzz project channel URL / name?** Select one existing project channel or create one after the human confirms setup.
4. Optional **non-project** tracker for adhoc/reminders?

### B. Viewport & browser

5. **Primary viewport?** Default proposed: `1920x1080` (project-specific overrides later).
6. Secondary viewports in MVP? (`none` recommended)
7. **Browser?** Proposed: `Chrome`

### C. UAT & promote path

8. **Primary UAT host / runtime?** (machine, cluster, PaaS, or `none` for localhost-only teams)
9. How agents reach it (URL / path). `PENDING` allowed if policy is otherwise clear.
10. If UAT is busy? Proposed: `spin_new` | `wait` | `fail`
11. Localhost as default run target? Proposed: `no` when a shared UAT exists
12. Preview / production environment names (if any)
13. **Promote order?** Example: `UAT → preview → production`
14. **Prod gate?** Example: Human Review + green UAT before production

### D. Model routing

15. Plan / review lane
16. Implement lane
17. Bulk / scaffold lane
18. Image / mockup generation path (declare explicitly; forbid undeclared providers)
19. What stays **parent-only**? (proposed: merge, DoD, integration judgment)

### E. Design gate

20. Human must approve North Star before Developing? (proposed: `yes`)
21. Personas path / names
22. Persona pass threshold (e.g. `≥3/4 pass, zero P0`)

### F. Engineering

23. Default test commands
24. Graft required? (`yes` if `graft/` exists)
25. Branch naming pattern
26. Merge style
27. Secrets location
28. Self-improvement cadence (proposed: `on_commit`)
29. Non-UI WPs skip Mocked Up? (proposed: `yes`)
30. Circuit breaker strikes (proposed: `2`)

---

## §2 Mismatch audit (blocking)

Compare before locking:

| Source | Path |
|--------|------|
| Repo AGENTS | `./AGENTS.md` |
| Global defaults | e.g. `~/.codex/AGENTS.md` if present |
| Cursor / IDE rules | project or user rules if accessible |
| Deploy / UAT docs | e.g. `docs/**` |

### Checks

1. `AGENTS.md` exists (create minimal stub + charter pointer if missing).
2. OpenProject is the project WP authority across AGENTS / global / CONFIG.
3. OpenProject project, Wiki, and Bootstrap page are recorded and reachable; `evidence_log` resolves to that OpenProject project/Wiki; `assumptions_log` resolves inside that Wiki. Local repo paths and non-OpenProject destinations fail.
4. Buzz is the discussion authority; one project channel is recorded and the one-thread-per-WP policy is not contradicted.
5. Browser: no Edge-by-default conflict.
6. Imagegen: no undeclared provider as default.
7. Viewport: docs vs CONFIG `primary_viewport`.
8. UAT vs production: docs must not skip UAT if CONFIG requires it.
9. Preview ≠ UAT unless waived.
10. Graft: if `graft/` present, AGENTS or CONFIG should acknowledge it.
11. DoD: test commands / tiers not weaker than existing build contracts without waiver.
12. Duplicate process bloat: prefer “see `.agent_charter/`” over copying the full board into AGENTS.
13. Commit policy recorded and compatible with the pre-commit OpenProject/Buzz gate.

### Report format

```markdown
## Mismatch audit — <repo> — <date>
| Check | Result | Evidence | Resolution |
|-------|--------|----------|------------|
| … | Pass/Fail | … | … |
```

Blocking Failures → leave `setup_complete: false`.

---

## §3 Wire AGENTS.md

Add (or equivalent):

```markdown
## Agent Charter

- Follow `.agent_charter/` for the OpenProject work-package lifecycle and Wiki knowledge, Buzz discussion threads, North Stars, validation, and routing.
- Repo-specific OpenProject and Buzz locations and other answers: `.agent_charter/CONFIG.md`.
- If `CONFIG.md` is missing or `setup_complete: false`, run `.agent_charter/SETUP.md` before feature work.
```

Do not duplicate the full status machine into AGENTS.

---

## §4 Completion

1. Verify that the OpenProject project, Wiki, Bootstrap page, and Buzz project channel exist and are reachable. Obtain action-time human confirmation before creating or changing an external surface. Missing required surfaces block completion.
2. Populate or reconcile the Bootstrap page with the minimum shared context in `CHARTER_CORE.md` §4. An empty or stale page blocks completion.
3. Write `CONFIG.md`.
4. Set `charter_version: 2`, `setup_complete: true`, and `setup_completed_at` only after the verification, Bootstrap reconciliation, and human answers are complete.
5. Show a concise CONFIG summary covering OpenProject project/wiki, Buzz channel, viewport, UAT, routing, and tests.
6. Only then allow normal WP work under the charter.
