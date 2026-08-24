# Agent Operating Charter

Modular governance for coding agents in **this** repository. Process lives here; product facts stay in `AGENTS.md`; OpenProject and Buzz locations plus other filled answers live in `CONFIG.md`.

**Re-install / upgrade from:** https://github.com/asymetryk/agent-operating-charter  
(Paste that URL into the agent and say “re-run intake” or “refresh charter process files”.)

## Files

| File | Role |
|------|------|
| `SETUP.md` | First-run questionnaire + mismatch audit |
| `CONFIG.md` | Repo-specific answers (created at setup) |
| `CONFIG.example.md` | Blank template |
| `CHARTER_CORE.md` | OpenProject WP lifecycle and Wiki record, Buzz collaboration, assumptions, circuit breaker |
| `CHARTER_DESIGN.md` | North Star / UI pipeline |
| `CHARTER_ENGINEERING.md` | Fencing, validation, merge, UAT |
| `CHARTER_ROUTING.md` | Model / skill / parent-worker routing |

## Agent entry protocol

1. Read `CONFIG.md`.
2. If missing, `setup_complete: false`, or `charter_version` is missing/below `2` → run `SETUP.md`. **Do not start WP work.**
3. Run mismatch checks in `SETUP.md` against `AGENTS.md` / global defaults.
4. Verify the configured OpenProject project/wiki and Buzz channel before WP work.
5. If blocking mismatches → stop and resolve with the human.
6. Follow CORE → DESIGN / ENGINEERING / ROUTING as the WP type requires.

## Precedence (highest first)

1. Human message for this turn
2. Repo `AGENTS.md`
3. `.agent_charter/CONFIG.md`
4. `.agent_charter/CHARTER_*.md`
5. Skills / tools named by ROUTING
6. Global agent defaults (if any)

If two layers conflict, stop and ask — do not silently pick one.
