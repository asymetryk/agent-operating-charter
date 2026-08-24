# AGENT OPERATING CHARTER: UI/UX & DESIGN SYSTEM

Requires `CONFIG.md` (`setup_complete: true`). Non-UI WPs skip this file when `skip_mocked_up_for_non_ui: true`.

## 1. North Star generation pipeline

Before writing front-end code, establish a visual benchmark during **Mocked Up**:

```
[Requirements] → [Image Gen Prompts] → [Mockup Variants]
        → [Persona Judges] → [Scoring Loop] → [Human Lock] → [North Star Locked]
```

1. **Prompting:** Generate mockups via `CONFIG.md` → `imagegen` (see `CHARTER_ROUTING.md`). Apply repo design tokens / baseline UI guidance. Do **not** use undeclared image providers.
2. **Multi-persona judging:** Score variants with personas from `CONFIG.md` → `personas_path` (e.g. Power User, Executive, First-Time Onboarder, or repo-specific set).
3. **Scoring criteria:**
   * **Clarity** — information hierarchy obvious?
   * **Efficiency** — minimize clicks / cognitive load?
   * **Alignment** — design tokens / existing product language?
4. **Iterative refinement:** Re-prompt until `persona_threshold` is met.
5. **Human lock:** If `human_north_star_approval_required: true`, discuss and obtain human approval in the dedicated Buzz WP thread, then record that approval on the OpenProject WP before **Developing**.
6. **Artifact:** Save as `NORTH_STAR_WP_[ID].png` on the WP / `evidence_log` path (and repo docs path if used, e.g. `docs/**/mockups/`).

## 2. Primary viewport constraint

From `CONFIG.md` → `primary_viewport` (screenshot resolution — **not** the UAT host):

* **Single primary viewport** for design + visual validation (default often `1920x1080`; mobile e.g. `390x844` when that is the primary).
* **Do not** design/test secondary viewports during initial MVP of the feature.
* **Viewport expansion** only after Human Review on the primary viewport (or explicit WP scope).

UAT host / promote path lives in `CONFIG.md` Environments and `CHARTER_ENGINEERING.md`.

## 3. Skills / tools (invoke if present; do not re-author)

Wire concrete skill names in `CONFIG.md` / `CHARTER_ROUTING.md` for your toolchain (imagegen, baseline UI, frontend quality gate, etc.).

## 4. Browser

Use `CONFIG.md` → `browser` (default Chrome). No Edge-by-default.
