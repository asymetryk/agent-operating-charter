# AGENT OPERATING CHARTER: MODEL & WORKER ROUTING

Requires `CONFIG.md` (`setup_complete: true`). Values below are **examples**; **CONFIG wins** when filled.

## 1. Intent → lane (example table)

Replace model names and CLIs with your team’s stack during SETUP.

| Intent | Example lane | Notes |
|--------|--------------|-------|
| Plan / architecture | Strong reasoning model (HTTP or chat) | Parent keeps final call |
| Review (diff / design) | Strong reasoning model | |
| Explore / cheap skim | Faster / cheaper model | No secrets in prompts |
| Feature implement | Coding worker profile | Bounded prompt + acceptance + `DONE`/`FAIL` |
| Bulk scaffold / tests | High-throughput worker | Supervised; parent verifies |
| Mockup stills | Declared imagegen path in CONFIG | Never undeclared providers |
| Integration, merge, DoD | **Parent agent only** | Do not delegate authority |
| Image fallback | Ask human before alternate tools | Only if primary imagegen is unreachable |

Record exact commands and skill paths in CONFIG or a short team appendix — keep this file process-oriented.

## 2. Parent vs worker contract

**Parent:**

* Runs SETUP / mismatch audit
* Owns architecture, shared files, migrations, merge, OpenProject status/wiki integration, and Buzz decision reconciliation
* Verifies worker output before Human Review / merge
* Never marks UI DoD complete without live screenshots at primary viewport
* Never promotes to production without satisfying CONFIG `prod_gate`

**Worker brief must include:**

* Exact file fence
* Acceptance criteria
* Commands to run
* Assumption logging instructions
* OpenProject WP link, relevant Wiki links, and dedicated Buzz thread
* Terminal marker: `DONE` or `FAIL` with one-line reason

**Workers must not:**

* Expand scope, commit/push unless brief + policy say so
* Edit shared boundaries
* Send secrets in prompts
* Treat a Buzz-only decision as durable or merge-ready; the parent must reconcile it into OpenProject
* Claim merge/DoD authority

## 3. Skill routing (examples — enable what you have)

| Situation | Typical skill / tool |
|-----------|----------------------|
| Non-trivial feature/bug + PR | PR / feature workflow skill |
| User-visible UI | Frontend quality gate |
| Live hosted / infra change | Deploy / live-service gate |
| Outage / flaky service | Troubleshooting-first |
| New tool/architecture choice | Discovery-first |
| Durable learnings | Self-improvement **on commit** |

## 4. Forbidden defaults

* Undeclared image / model providers for charter lanes
* Edge as default browser
* Skipping North Star human lock when CONFIG requires it
* Delegating merge/DoD to bulk workers
* Silently weakening UAT / prod gates
