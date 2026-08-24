# AGENT OPERATING CHARTER: CORE & LIFECYCLE

Requires `.agent_charter/CONFIG.md` with `setup_complete: true`. If not, run `SETUP.md` first.

## 1. Global operating philosophy

* **Optimistic concurrency:** Execute independent work in parallel. When blocked on an unbuilt module or external interface, **make an explicit assumption**, generate a stub/contract, log it in the OpenProject Wiki Assumptions Log (`CONFIG.md`), comment on the OpenProject Work Package, and proceed.
* **Strict scope isolation:** Modify ONLY assigned files/modules. Never touch code outside explicit scope. Request shared-boundary changes from the **parent orchestrator** (see `CHARTER_ROUTING.md`).
* **Non-blocking execution:** Do not halt on missing sibling dependencies. Log assumptions and push to reconciliation before merge.
* **Durable shared context:** OpenProject Wikis hold the Bootstrap, architecture, dependencies, runbooks, handoffs, assumptions, and other information agents must share across sessions.
* **Discussion before mutation:** WP discussion and decision-making happen in Buzz before commit or merge, in the configured project channel and the WP's dedicated thread.
* **Context first:** If `CONFIG.md` has `graft_required: true`, run `graft ask "<task>" --source` (or `graft map` when new to the repo) before broad grep/file reads. After large code changes, `graft build`.

## 2. Precedence

Human turn → repo `AGENTS.md` → `CONFIG.md` → this charter set → named skills → global agent defaults (if any).  
Conflicts → stop and ask (see `SETUP.md` mismatch audit).

## 3. Work package lifecycle

All Features / Bugs / Tasks are **Work Packages in OpenProject**, under `CONFIG.md` → `openproject_project`. Agents update **Status** as work progresses:

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

1. **Submitted** — OpenProject WP created; dedicated Buzz thread created in the project channel; reciprocal links recorded.
2. **Approved for Dev** — Human/lead verifies scope in the Buzz WP thread and records the outcome on the OpenProject WP. Required on the WP before coding:
   * Acceptance criteria (testable)
   * In-scope / out-of-scope file list
   * Primary viewport (from CONFIG, or WP override)
   * UAT target (from CONFIG `uat_host`, if any)
   * UI? yes/no (determines Mocked Up)
   * Relevant OpenProject Wiki page(s), including the Bootstrap page when setup or shared context is affected
   * Dedicated Buzz thread in the configured project channel
3. **Mocked Up** — North Star + contracts attached (`CHARTER_DESIGN.md`). Stays here until the human approves in the Buzz WP thread and the approval is recorded on the OpenProject WP when `human_north_star_approval_required: true`.
4. **Developing** — Implementation by fenced workers (`CHARTER_ENGINEERING.md`).
5. **Validating** — Automated tiers (`CHARTER_ENGINEERING.md`).
   * Fail → **Developing** + failure logs on the OpenProject WP and summary in the Buzz thread.
   * Pass → **Human Review Queue** + evidence pack linked from OpenProject and Buzz.
6. **Human Review Queue** — Automated checks passed; awaiting human sign-off in the Buzz WP thread.
   * Reject → **Developing** + feedback in Buzz and outcome recorded on OpenProject.
   * Approve → record approval on OpenProject → **Approved for Merge**.
7. **Approved for Merge** — Orchestrator integrates per CONFIG `merge_style`, runs final validation, merges.
8. **Merged** — On primary branch.
9. **Closed** — Deployed/archived per repo release rules; update the OpenProject WP and close out its Buzz thread.

## 4. OpenProject wiki and Buzz collaboration

OpenProject is the durable system of record; Buzz is the discussion surface:

1. Maintain one Buzz channel for the project (`CONFIG.md` → `buzz_channel`).
2. Create one thread per OpenProject WP, named `WP <id> — <title>`, and cross-link the WP and thread.
3. Use that thread for proposals, questions, blockers, handoffs, approvals, waivers, and decisions about the WP.
4. Record durable outcomes in the OpenProject WP or a relevant OpenProject Wiki page. A Buzz-only decision is not merge-ready.
5. Keep the OpenProject Wiki Bootstrap page and relevant architecture, dependency, interface, runbook, handoff, and assumption pages current before committing or merging work that changes them.
   * Minimum Bootstrap content: repo purpose; canonical repository and primary branch; setup/build/test/run commands; secret references without secret values; architecture, shared interfaces, and dependencies; environments, UAT, promote, and rollback path; current handoff/integration state; and links to the OpenProject project/Wiki/evidence/assumptions locations plus the Buzz channel.
6. Before commit or merge, post a concise readiness summary in the Buzz WP thread and verify the WP, wiki page(s), and thread cross-link each other. Record outcomes and owners; do not paste raw chat transcripts.

## 5. Centralized assumption protocol

When executing on an unverified dependency, update the OpenProject Wiki page at `CONFIG.md` → `assumptions_log`, comment on the OpenProject WP, and post the assumption in the WP's Buzz thread:

```markdown
### [WP-#ID] Target: <Module/File>
- **Dependent On:** <missing interface / package / WP>
- **Assumption Made:** <signature, stub type, payload, behavior>
- **Reconciliation Action:** <what must be proven at integration>
```

**Merge gate:** No WP may enter **Merged** with unresolved assumptions unless a human waiver is approved in the Buzz WP thread and recorded in `CONFIG.md` → Waivers or on the OpenProject WP.

## 6. Circuit breaker

If a WP fails **Validating** or **Human Review** `circuit_breaker_strikes` times **consecutively** (default 2):

1. **Validation failures:** leave status at **Validating**; halt retries.
2. **Human review failures:** leave status at **Human Review Queue**; halt retries.
3. Post the failure summary in the Buzz WP thread and record it on the OpenProject WP: (a) target files, (b) failing log or rejected criteria, (c) root-cause hypothesis.
4. Wait for explicit human intervention before further attempts.

## 7. Parent orchestrator vs workers

| Role | Owns |
|------|------|
| **Parent** | Requirements, architecture, shared types/utilities/global styles, migrations, merge, DoD judgment, OpenProject status/wiki finalization, and Buzz decision reconciliation |
| **Worker** | Fenced files only; stubs at boundaries; `DONE`/`FAIL` + evidence |

Workers never edit shared boundaries without parent approval. See `CHARTER_ROUTING.md`.
