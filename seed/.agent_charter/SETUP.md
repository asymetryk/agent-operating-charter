# First-run setup & mismatch audit

Run **once per repo** (or whenever `CONFIG.md` has `setup_complete: false`). Ask the human; do not invent blocking answers. After answers, write `CONFIG.md` from `CONFIG.example.md`, set `setup_complete: true`, and wire repo `AGENTS.md` (see §Wire).

---

## §1 Primary setup questions

Ask in one batch. Label suggested defaults as **proposed**.

### A. Tracker

1. **Authoritative tracker for project WP status?** (OpenProject, Linear, Jira, GitHub Issues, other)
2. Project URL / id for that tracker.
3. Optional **non-project** tracker for adhoc/reminders?
4. Where do agents attach evidence (logs, screenshots) and assumptions?

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
2. Tracker authority agrees across AGENTS / global / CONFIG (or CONFIG explicitly overrides with human sign-off).
3. Browser: no Edge-by-default conflict.
4. Imagegen: no undeclared provider as default.
5. Viewport: docs vs CONFIG `primary_viewport`.
6. UAT vs production: docs must not skip UAT if CONFIG requires it.
7. Preview ≠ UAT unless waived.
8. Graft: if `graft/` present, AGENTS or CONFIG should acknowledge it.
9. DoD: test commands / tiers not weaker than existing build contracts without waiver.
10. Duplicate process bloat: prefer “see `.agent_charter/`” over copying the full board into AGENTS.
11. Commit policy recorded.

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

- Follow `.agent_charter/` for work-package lifecycle, North Stars, validation, and routing.
- Repo-specific answers: `.agent_charter/CONFIG.md`.
- If `CONFIG.md` is missing or `setup_complete: false`, run `.agent_charter/SETUP.md` before feature work.
```

Do not duplicate the full status machine into AGENTS.

---

## §4 Completion

1. Write `CONFIG.md`.
2. Set `setup_complete: true` and `setup_completed_at` after human confirms.
3. Show a 5-line CONFIG summary.
4. Only then allow normal WP work under the charter.
