# Agent Operating Charter

Modular governance for coding agents: one lifecycle, North Star design gate, validation ladder, and routing policy — configured once per repo.

---

## What it is

A **small markdown pack** (`.agent_charter/`) you install into a product repo so coding agents share the same operating rules:

| Module | Covers |
|--------|--------|
| **CORE** | Work-package lifecycle, assumptions log, circuit breaker, parent vs worker |
| **DESIGN** | North Star mockups → persona scoring → human lock before UI code |
| **ENGINEERING** | File fencing, validation tiers (tests → browser → visual → UAT), merge/promote |
| **ROUTING** | Which model/skill lane for plan / implement / bulk / imagegen; parent-only judgment |
| **SETUP + CONFIG** | One-time intake wizard; repo-specific answers live in `CONFIG.md` |

It is **process + config**, not a runtime, SaaS, or agent framework. Agents read the files; your existing IDE/agent (Cursor, Codex, etc.) executes the work.

---

## Why use it

- **Less prompt thrash** — paste a URL once; stop re-explaining boards, UAT, and mockup rules every chat.
- **Parallel agents without collisions** — strict file fences + stub/assumption protocol.
- **UI quality bar** — North Star locked before code; screenshots compared on a declared viewport.
- **Honest DoD** — cheap tests first, then browser, then visual, then shared UAT before prod.
- **Keeps `AGENTS.md` thin** — product/stack facts stay in AGENTS; process stays in the charter.

---

## Assumptions

The charter assumes roughly this shape of work:

1. **A human is accountable** for scope, North Star approval (when UI), and production promote.
2. **Work is ticketed** as Work Packages in *some* tracker (OpenProject, Linear, Jira, GitHub Issues, …) — name it in CONFIG.
3. **Agents can edit the repo** and run tests; secrets stay out of git.
4. **Optimistic concurrency is OK** — missing deps → stub + log assumption → reconcile before merge.
5. **One primary viewport** for MVP UI (default proposal `1920×1080`); multi-breakpoint comes later.
6. **Shared UAT is preferred** over laptop-localhost when the team has one; preview ≠ UAT unless waived.
7. **Precedence:** human message → `AGENTS.md` → `CONFIG.md` → `CHARTER_*` → skills → global defaults. Conflicts → ask, don’t invent.

If your team never does UI, never uses UAT, or never parallels agents, you can still use CORE + ROUTING and turn off Mocked Up / UAT tiers in CONFIG.

---

## Dependencies (required vs recommended)

### Required

| Need | Notes |
|------|--------|
| Git + a product repo | Charter installs as `.agent_charter/` inside it |
| A coding agent that can read markdown + run shell | Cursor, Codex, Claude Code, etc. |
| Network once at install | Clone/fetch this template (or use a local clone path) |
| Human answers at intake | Tracker, viewport, test commands, routing, UAT (or explicit “none”) |

**No** mandatory cloud account, npm package, or binary beyond git.

### Recommended (declare in CONFIG — not hard-wired)

| Capability | Why | Examples |
|------------|-----|----------|
| **Context graph** | Cheap, accurate “where is X?” before grep/open | [graft](https://github.com/search?q=graft) / repo `graft/` → set `graft_required: true` |
| **Model router** | Plan/review vs implement vs bulk on different lanes; save cost/quota | OmniRoute (or your HTTP router / profiles) — fill `plan_review` / `implement` / `bulk` |
| **Imagegen path** | North Star stills | OmniRoute imagegen, or any **declared** provider — forbid undeclared/legacy paths in CONFIG |
| **Browser automation** | Tier 1–2 validation | Playwright (+ Chrome) |
| **Project tracker** | WP status board | OpenProject, Linear, Jira, GitHub Issues, … |
| **Optional adhoc tracker** | Non-project reminders | Baserow, etc. |
| **Shared UAT runtime** | Tier 3 before prod | Devcontainers on a shared host, compose, PaaS preview pool |
| **Edge / prod deploy** | End of promote order | Cloudflare, Vercel, … — named in CONFIG `promote_order` |
| **Learnings on commit** | Light process improvement | `self_improvement: on_commit` |

OmniRoute and graft are **recommendations for teams that already use them**, not requirements to adopt this charter. The seed’s ROUTING table is an example; SETUP writes *your* lanes into CONFIG.

---

## Install (this is the whole UX)

1. Open your **product** repository in your coding agent.
2. Paste **only** this link (or the one-liner):

**https://github.com/asymetryk/agent-operating-charter**

```text
Install the Agent Operating Charter from https://github.com/asymetryk/agent-operating-charter into this repo and run the intake wizard.
```

3. Answer the intake questions; confirm; done.

The agent fetches [`BOOTSTRAP.md`](BOOTSTRAP.md) and runs the wizard — **no long prompt paste**.

---

## What gets installed

| Path | Purpose |
|------|---------|
| [`BOOTSTRAP.md`](BOOTSTRAP.md) | Intake wizard (URL / one-liner entrypoint) |
| [`seed/.agent_charter/`](seed/.agent_charter/) | Copied into the product repo as `.agent_charter/` |
| [`templates/`](templates/) | Optional seeds (AGENTS snippet, assumptions log, compare sheet, WP checklist) |
| [`examples/CONFIG.sample.md`](examples/CONFIG.sample.md) | Fictional filled config |
| [`INSTALL_PROMPT.md`](INSTALL_PROMPT.md) | Long-form fallback if the agent cannot fetch the web |

## Precedence (in consuming repos)

1. Human message  
2. Repo `AGENTS.md`  
3. `.agent_charter/CONFIG.md`  
4. `.agent_charter/CHARTER_*.md`  
5. Named skills / tools  
6. Global agent defaults (if any)

Conflicts → stop and ask.

## License

MIT — see [LICENSE](LICENSE).
