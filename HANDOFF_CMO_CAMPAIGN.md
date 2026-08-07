# CMO handoff — Agent Operating Charter campaign

**Audience for this note:** CMO / marketing agent (Substack + LinkedIn).  
**Product / story:** public open-source **Agent Operating Charter**.  
**Date:** 2026-08-06  
**Owner:** Howard (Asymetryk) — hand off for campaign generation only; not for code changes.

---

## Objective

Produce a **Substack essay + LinkedIn campaign** that positions the Agent Operating Charter as a practical, copy-pasteable way for teams to govern coding agents — without selling a SaaS, without claiming AGI, and without burying readers in tooling dogma.

**Deliverables expected from CMO agent:**

1. **Substack long-form** (≈1,200–2,000 words): narrative + clear CTA to the GitHub repo.
2. **LinkedIn campaign pack:**
   - 1 primary post (hook + proof + CTA)
   - 3–5 short follow-ups / carousel-friendly beats (or a 5–7 slide carousel outline)
   - 5–8 comment/reply starters for engagement
3. Suggested **titles / subject lines** (3–5 options each for Substack + LinkedIn).
4. A one-line **elevator** and a 3-bullet **why it matters** usable in both channels.

Pause for human approval before publishing or scheduling anything.

---

## Positioning (use this framing)

### What it is

A **small, public markdown pack** you drop into a product repo so coding agents share one operating system: work-package lifecycle, North Star UI gate, validation ladder, model routing, and a one-time intake wizard.

**Install UX:** paste the repo URL into your coding agent → intake wizard → `.agent_charter/` + `CONFIG.md`. No long prompt paste required.

**Public repo:** https://github.com/asymetryk/agent-operating-charter  

### What it is not

- Not an agent framework, runtime, or hosted product  
- Not “replace your engineers”  
- Not locked to one model vendor (OmniRoute / graft are *optional recommendations*, declared in CONFIG)  
- Not a dashboard or another process theater tool  

### Core tension (story fuel)

Teams keep re-pasting the same agent rules every chat. Parallel agents collide. UI ships without a visual North Star. “Done” means green unit tests while UAT and production gates are fuzzy. The charter turns that tribal knowledge into a **modular, repo-local contract**.

### Audience

Primary: founders, eng leads, and AI-forward operators running **Cursor / Codex / Claude Code** (or similar) on real product repos.  
Secondary: agency / platform teams selling AI-assisted delivery who need a credible governance story.

### Tone

Direct, operator-credible, lightly opinionated. Avoid hype words (autonomous swarm, AGI workforce). Prefer concrete nouns: Work Package, North Star, UAT, circuit breaker, file fence.

Brand: **Asymetryk** as publisher / steward of the open pack — not a hard sell of AIC (Infrastructure Cortex) in this campaign. AIC can appear as a *worked example* of Surface A/B UAT + charter, not the product pitch.

---

## Verified state (facts you can cite)

| Fact | Proof / link |
|------|----------------|
| Public MIT repo live | https://github.com/asymetryk/agent-operating-charter |
| URL-first install via `BOOTSTRAP.md` | README + BOOTSTRAP in that repo |
| Modules: CORE / DESIGN / ENGINEERING / ROUTING + SETUP/CONFIG | `seed/.agent_charter/` |
| Optional deps called out honestly | README “Dependencies” section |
| Worked example: SHI presentation Surface A/B UAT | `shi-presentation-a/b.tail21f530.ts.net` (internal pattern; **do not** over-expose private IPs in public posts unless Howard approves) |
| Worked example: AIC Surface A/B UAT live | `https://aic-cortex-a.tail21f530.ts.net` / `https://aic-cortex-b.tail21f530.ts.net` (Tailscale; audience may not resolve — prefer “shared UAT pool on a team workstation” language publicly) |
| AIC branch with charter + Surface compose | `cursor/agent-charter-surface-uat` on Asymetryk-Infrastructure-Cortex (pushed) |

**Safe public proof language:** “We run the same A/B UAT pool pattern on a shared Surface host with Tailscale HTTPS, and the charter encodes `spin_new` when a slot is busy.” Avoid dumping internal LAN IPs unless explicitly cleared.

---

## Message pillars (map content to these)

1. **Paste a link, not a novel** — intake wizard beats re-prompting.  
2. **Process lives beside the code** — `.agent_charter/` keeps `AGENTS.md` thin.  
3. **Optimistic concurrency with receipts** — stubs + Assumptions Log + merge gate.  
4. **UI with a North Star** — mockup lock before code; one primary viewport.  
5. **Honest definition of done** — tests → browser → visual → shared UAT → prod.  
6. **Vendor-agnostic with sharp defaults** — declare your router/imagegen/tracker in CONFIG.

---

## Suggested angles (pick 1 primary for Substack; remix for LinkedIn)

| Angle | Hook |
|-------|------|
| A | “We stopped pasting agent rules into every chat.” |
| B | “Your coding agents need a charter, not another framework.” |
| C | “Parallel agents collide until you fence files and log assumptions.” |
| D | “Green tests aren’t done — UAT before prod, written into the repo.” |
| E | “Open-source the operating system for your AI coding team.” |

---

## Campaign constraints / do-nots

- Do **not** claim the charter requires OmniRoute, graft, OpenProject, or Cloudflare.  
- Do **not** publish secrets, OAuth paths, or private Tailscale IPs without approval.  
- Do **not** frame as “set and forget autonomous agents.” Human review and prod gates stay explicit.  
- Do **not** turn the Substack into an AIC product launch — charter is the hero.  
- Keep CTAs to: star/clone GitHub, paste URL into your agent, run intake.  
- LinkedIn: prefer one strong CTA; avoid link-in-every-comment spam.

---

## Exact next steps (CMO agent)

1. Read https://github.com/asymetryk/agent-operating-charter (README + BOOTSTRAP.md). Skim module names only — don’t rewrite the charter.  
2. Draft **Substack** from Angle A or E (default: A). Include install one-liner + GitHub CTA.  
3. Draft **LinkedIn primary + 3 follow-ups** remixing pillars 1, 3, 5.  
4. Produce title options + elevator + 3-bullet why.  
5. Return drafts in one package for Howard’s edit/approve — **do not publish**.

---

## Useful references

| Resource | URL / path |
|----------|------------|
| Public charter | https://github.com/asymetryk/agent-operating-charter |
| Install one-liner | `Install the Agent Operating Charter from https://github.com/asymetryk/agent-operating-charter into this repo and run the intake wizard.` |
| Bootstrap entry | `BOOTSTRAP.md` in that repo |
| AIC local charter (private context) | `Asymetryk-Infrastructure-Cortex/.agent_charter/` |
| AIC Surface UAT compose | `Asymetryk-Infrastructure-Cortex/deployment/surface-preview/` |
| AIC branch | `cursor/agent-charter-surface-uat` |

---

## Parked for later

- Full AIC product marketing / WhiteFiber official-build story  
- Paid ads, email sequences beyond Substack  
- Logo/brand kit expansion  
- Committing SHI presentation charter changes (local + Surface synced; may still need PR)  
- Public screenshots of Tailscale UAT (capture only if Howard wants visual proof in the post)

---

## Resume note (for the CMO agent)

Howard wants a **Substack + LinkedIn campaign** about the open-source **Agent Operating Charter** (https://github.com/asymetryk/agent-operating-charter): URL-paste install, modular agent governance (lifecycle, North Star, validation, routing), vendor-agnostic CONFIG. Write drafts only; CTA = GitHub + intake wizard. Use operator tone; AIC/Surface A/B is optional proof of “shared UAT before prod,” not the product pitch. Do not publish until Howard approves.
