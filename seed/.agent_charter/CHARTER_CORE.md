# AGENT OPERATING CHARTER: CORE & LIFECYCLE

Requires `.agent_charter/CONFIG.md` with `setup_complete: true`. If not, run `SETUP.md` first.

## 1. Global operating philosophy

* **Optimistic concurrency:** Execute independent work in parallel. When blocked on an unbuilt module or external interface, **make an explicit assumption**, generate a stub/contract, log it in the configured Assumptions Log (`CONFIG.md`), comment on the Work Package, and proceed.
* **Strict scope isolation:** Modify ONLY assigned files/modules. Never touch code outside explicit scope. Request shared-boundary changes from the **parent orchestrator** (see `CHARTER_ROUTING.md`).
* **Non-blocking execution:** Do not halt on missing sibling dependencies. Log assumptions and push to reconciliation before merge.
* **Context first:** If `CONFIG.md` has `graft_required: true`, run `graft ask "<task>" --source` (or `graft map` when new to the repo) before broad grep/file reads. After large code changes, `graft build`.

## 2. Precedence

Human turn → repo `AGENTS.md` → `CONFIG.md` → this charter set → named skills → global agent defaults (if any).  
Conflicts → stop and ask (see `SETUP.md` mismatch audit).

## 3. Work package lifecycle

All Features / Bugs / Tasks are **Work Packages** in the tracker named by `CONFIG.md` → `wp_status_authority`. Agents update **Status** as work progresses:

```
[Submitted] → [Approved for Dev] → [Mocked Up]* → [Developing] → [Validating]
                                      │                ↑              │
                                      │                │         (fail)┘
                                      │                │
                                      │                └── [Human Review Queue]
                                      │                         │
                                      │              (reject) ──┘  (approve)
                                      │                              ↓
                                      │                    [Approved for Merge]
                                      │                              ↓
                                      │                         [Merged] → [Closed]

* Skip [Mocked Up] when CONFIG skip_mocked_up_for_non_ui is true AND the WP has no user-visible UI.
```

### Status definitions & rules

1. **Submitted** — Ticket created.
2. **Approved for Dev** — Human/lead verified scope. Required on the WP before coding:
   * Acceptance criteria (testable)
   * In-scope / out-of-scope file list
   * Primary viewport (from CONFIG, or WP override)
   * UAT target (from CONFIG `uat_host`, if any)
   * UI? yes/no (determines Mocked Up)
3. **Mocked Up** — North Star + contracts attached (`CHARTER_DESIGN.md`). Stays here until **human approves** the North Star when `human_north_star_approval_required: true`.
4. **Developing** — Implementation by fenced workers (`CHARTER_ENGINEERING.md`).
5. **Validating** — Automated tiers (`CHARTER_ENGINEERING.md`).
   * Fail → **Developing** + failure logs on WP.
   * Pass → **Human Review Queue** + evidence pack.
6. **Human Review Queue** — Automated checks passed; awaiting human sign-off.
   * Reject → **Developing** + feedback notes.
   * Approve → **Approved for Merge**.
7. **Approved for Merge** — Orchestrator integrates per CONFIG `merge_style`, runs final validation, merges.
8. **Merged** — On primary branch.
9. **Closed** — Deployed/archived per repo release rules; update tracker.

## 4. Centralized assumption protocol

When executing on an unverified dependency, log to `CONFIG.md` → `assumptions_log` **and** comment on the WP:

```markdown
### [WP-#ID] Target: <Module/File>
- **Dependent On:** <missing interface / package / WP>
- **Assumption Made:** <signature, stub type, payload, behavior>
- **Reconciliation Action:** <what must be proven at integration>
```

**Merge gate:** No WP may enter **Merged** with unresolved assumptions unless a human waiver is recorded in `CONFIG.md` → Waivers (or on the WP).

## 5. Circuit breaker

If a WP fails **Validating** or **Human Review** `circuit_breaker_strikes` times **consecutively** (default 2):

1. **Validation failures:** leave status at **Validating**; halt retries.
2. **Human review failures:** leave status at **Human Review Queue**; halt retries.
3. Post a WP comment: (a) target files, (b) failing log or rejected criteria, (c) root-cause hypothesis.
4. Wait for explicit human intervention before further attempts.

## 6. Parent orchestrator vs workers

| Role | Owns |
|------|------|
| **Parent** | Requirements, architecture, shared types/utilities/global styles, migrations, merge, DoD judgment, tracker status for integration |
| **Worker** | Fenced files only; stubs at boundaries; `DONE`/`FAIL` + evidence |

Workers never edit shared boundaries without parent approval. See `CHARTER_ROUTING.md`.
