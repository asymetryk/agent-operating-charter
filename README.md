# Agent Operating Charter

Modular governance for coding agents: OpenProject work packages and Wikis, Buzz discussion threads, one lifecycle, a North Star design gate, a validation ladder, and configurable execution routing.

---

## What it is

A **small markdown pack** (`.agent_charter/`) you install into a product repo so coding agents share the same operating rules:

| Module | Covers |
|--------|--------|
| **CORE** | OpenProject WP lifecycle and Wiki record, Buzz discussion/decisions, assumptions, circuit breaker, parent vs worker |
| **DESIGN** | North Star mockups → persona scoring → human lock before UI code |
| **ENGINEERING** | File fencing, validation tiers (tests → browser → visual → UAT), merge/promote |
| **ROUTING** | Which model/skill lane for plan / implement / bulk / imagegen; parent-only judgment |
| **SETUP + CONFIG** | One-time intake wizard; OpenProject and Buzz locations plus repo-specific answers live in `CONFIG.md` |

It is **process + config**, not a runtime, SaaS, or agent framework. Agents read the files; your existing IDE/agent (Cursor, Codex, etc.) executes the work.

---

## Why use it

- **Shared operating record** — OpenProject holds WPs and durable Wiki context; Buzz holds one project channel with one thread per WP.
- **Parallel agents without collisions** — strict file fences + stub/assumption protocol.
- **UI quality bar** — North Star locked before code; screenshots compared on a declared viewport.
- **Honest DoD** — cheap tests first, then browser, then visual, then shared UAT before prod.
- **Keeps `AGENTS.md` thin** — product/stack facts stay in AGENTS; Bootstrap and shared agent context stay in the OpenProject Wiki; process stays in the charter.

---

## Assumptions

The charter assumes roughly this shape of work:

1. **A human is accountable** for scope, North Star approval (when UI), and production promote.
2. **Work is managed as OpenProject Work Packages.** Durable Bootstrap and shared project knowledge live in the project's OpenProject Wiki; discussion and decision-making happen in one Buzz project channel with one thread per WP.
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
| Human answers at intake | OpenProject project/wiki and Bootstrap page, Buzz channel, viewport, test commands, routing, UAT (or explicit “none” where allowed) |
| OpenProject access | Project Work Packages and project Wiki |
| Buzz access | One project channel; one dedicated thread per OpenProject WP |

No mandatory npm package or agent runtime is imposed. The charter does require access to OpenProject and Buzz; either service may be hosted or self-hosted.

### Recommended (declare in CONFIG — not hard-wired)

| Capability | Why | Examples |
|------------|-----|----------|
| **Context graph** | Cheap, accurate “where is X?” before grep/open | [graft](https://github.com/search?q=graft) / repo `graft/` → set `graft_required: true` |
| **Model router** | Plan/review vs implement vs bulk on different lanes; save cost/quota | OmniRoute (or your HTTP router / profiles) — fill `plan_review` / `implement` / `bulk` |
| **Imagegen path** | North Star stills | OmniRoute imagegen, or any **declared** provider — forbid undeclared/legacy paths in CONFIG |
| **Browser automation** | Tier 1–2 validation | Playwright (+ Chrome) |
| **OpenProject/Buzz automation** | Reduce manual status, Wiki, channel, and thread updates | Declared API, CLI, or MCP integrations |
| **Optional adhoc tracker** | Non-project reminders | Baserow, etc. |
| **Shared UAT runtime** | Tier 3 before prod | Devcontainers on a shared host, compose, PaaS preview pool |
| **Edge / prod deploy** | End of promote order | Cloudflare, Vercel, … — named in CONFIG `promote_order` |
| **Learnings on commit** | Light process improvement | `self_improvement: on_commit` |

OmniRoute and graft are **recommendations for teams that already use them**, not requirements to adopt this charter. The seed’s ROUTING table is an example; SETUP writes *your* lanes into CONFIG.

OpenProject and Buzz are fixed collaboration surfaces in this charter. Model, router, image generation, browser automation, UAT, and deployment choices remain configurable.

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
