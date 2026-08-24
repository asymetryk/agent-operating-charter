# AGENT OPERATING CHARTER: ENGINEERING & VALIDATION

Requires `CONFIG.md` (`setup_complete: true`).

## 1. Execution & parallel sub-agent rules

* **Module fencing:** Workers own designated target files only. Do not edit shared utilities, global styles, or schema/migrations without parent approval.
* **Stub-driven progress:** If backend API or sibling UI is unfinished, code against a stub matching Design/API contracts and log the assumption (`CHARTER_CORE.md`).
* **Shared context:** Read the OpenProject WP, linked Wiki pages, and dedicated Buzz thread before editing. Keep discussion in that thread.
* **Graft:** When `graft_required: true`, discover edit points via graft before wide search.
* **Commit policy:** Follow `CONFIG.md` → `commit_policy`; the gate below still applies whenever a commit is authorized.

## 2. Pre-commit knowledge and discussion gate

Before every authorized commit:

1. Confirm the OpenProject WP reflects the current scope, status, acceptance criteria, and evidence.
2. Update the linked OpenProject Wiki pages when the work changes Bootstrap/setup, architecture, shared interfaces, dependencies, runbooks, handoffs, or assumptions.
3. Use the dedicated Buzz WP thread to resolve open questions and decisions; copy each durable outcome into the OpenProject WP or Wiki.
4. Post a concise commit-readiness summary in the Buzz thread: changed scope, validation evidence, open blockers, and the commit/branch identity when known.
5. Verify reciprocal links among the OpenProject WP, relevant Wiki pages, and Buzz thread.

A decision recorded only in Buzz, or shared context left only in a local checkout, blocks commit readiness.

## 3. Automated validation protocol

When status → **Validating**, run tiers in order. Skip tiers marked N/A on the WP.

### Tier 0 — Deterministic / static (cheap)

* Run `CONFIG.md` → `test_commands`.
* Fail → **Developing** with command output attached.

### Tier 1 — Functional browser tests

* Run project-standard Playwright (or equivalent) against the running build.
* Verify key interactions; no unhandled JS errors; no broken critical network calls.
* Browser = CONFIG `browser`.
* Fail → **Developing** + console/network dump.

### Tier 2 — Visual vs North Star (UI WPs only)

* Screenshot at `CONFIG.md` → `primary_viewport`.
* Compare to `NORTH_STAR_WP_[ID].png`.
* **Acceptance:** Structured compare notes (layout, tokens, type, placement) and/or persona gate — **not** an undefined pixel %. Prefer a short compare sheet in `evidence_log`.
* Fail → **Developing** + diff notes.

### Tier 3 — Shared UAT (when configured)

When `CONFIG.md` → `uat_host` is set:

* Deploy or refresh the WP build into the UAT runtime (`uat_runtime` / `uat_url_or_path`).
* **Instance pools:** If `uat_instances` lists multiple slots (e.g. A/B with LAN + Tailscale HTTPS), pick a **free** instance for the WP. Record which label (A/B/…) was used in the evidence pack.
* If `uat_if_busy: spin_new`: when no free instance is available, **provision a new one** (or bring up the idle compose service) — do not queue behind a busy slot unless the human overrides.
* Prefer configured UAT over laptop localhost when `localhost_default: false`. Prefer **Tailscale HTTPS** URLs for human/agent browser proof when both LAN and HTTPS are listed.
* Re-run Tier 1 (and Tier 2 for UI) **against the chosen UAT URL**, not only against localhost or preview.
* Attach UAT URL, instance label, runtime identity, and proof to the evidence pack.
* Fail → **Developing** (or halt per circuit breaker). Preview/staging is **not** a UAT substitute unless CONFIG waives it.
* `uat_url_or_path: PENDING` with no `uat_instances` → ask once, then record in CONFIG.

### Tier 4 — Repo DoD extras

If a build-loop / DoD doc exists and is in scope, its items apply. Charter tiers must not be weaker without a CONFIG waiver.

## 4. Evidence pack (before Human Review Queue)

1. Acceptance criteria checklist (pass/fail)
2. Tier 0 command + exit codes
3. Functional test summary (Tier 1)
4. Screenshots + compare notes vs North Star (Tier 2, if UI)
5. UAT proof (Tier 3, if configured)
6. Open assumptions list (empty or waived)
7. Branch / PR link
8. Primary viewport + browser used
9. OpenProject WP and relevant Wiki links
10. Dedicated Buzz WP thread with the commit-readiness summary

## 5. Merge & promote orchestration

When status → **Approved for Merge**, parent orchestrator:

1. Reconcile final Buzz decisions into the OpenProject WP and relevant Wiki pages; verify the Bootstrap/shared context is current.
2. Verify the Buzz thread contains the latest commit-readiness summary and reciprocal WP/wiki links.
3. Checkout feature branch; update from primary.
4. Integrate per `CONFIG.md` → `merge_style` (`ff-only-after-rebase` or `squash-via-pr`, etc.). Never force-push primary.
5. If conflict invalidates an Assumptions Log entry → **Developing** + notes in OpenProject and the Buzz thread.
6. Re-run Tier 0 (+ Tier 1 / Tier 3 as CONFIG requires).
7. Merge → status **Merged**; record the merge identity and outcome on the OpenProject WP and Buzz thread.

### Promote order (post-merge)

Follow `CONFIG.md` → `promote_order`. Typical pattern:

1. Shared UAT — must be green when configured  
2. Preview / staging (optional) — not a UAT substitute  
3. Production — only when `prod_gate` is satisfied  

Do **not** jump laptop → production when UAT is required.

## 6. Skills / tools

Invoke the repo’s configured validation and release skills (Playwright, frontend quality gate, PR workflow, deploy gate, etc.) as named in `CHARTER_ROUTING.md` / CONFIG.
