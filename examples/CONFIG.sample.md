---
# Fictional example only — do not copy as-is into a real product without SETUP.
setup_complete: true
setup_completed_at: "2026-01-15"
repo_name: "example-app"
---

# Agent Charter — project config (example)

## Tracker

- **wp_status_authority:** `OpenProject`
- **wp_status_location:** `https://openproject.example.com/projects/example-app`
- **non_project_tracker:** `Baserow`  # adhoc / reminders only
- **evidence_log:** OpenProject WP attachments + `docs/evidence/`
- **assumptions_log:** `docs/assumptions-log.md`

## Viewport

- **primary_viewport:** `1920x1080`
- **secondary_viewports_mvp:** none
- **browser:** Chrome

## Environments & UAT

- **uat_host:** `shared-uat`           # e.g. Surface WSL host
- **uat_runtime:** `docker-compose`
- **uat_url_or_path:** `https://app-a.example.ts.net`  # or rely on uat_instances
- **uat_instances:** |
    A | http://100.64.0.1:4173 | https://app-a.example.ts.net
    B | http://100.64.0.1:4174 | https://app-b.example.ts.net
- **uat_if_busy:** `spin_new`
- **localhost_default:** false
- **preview_env:** `example-app-preview`
- **production_env:** `example-app`
- **promote_order:** `UAT → preview → production`
- **prod_gate:** Human Review + green UAT proof before production

## Model routing

- **plan_review:** team plan/review model (High)
- **implement:** team implement worker
- **bulk:** team bulk worker
- **imagegen:** team declared imagegen skill only
- **parent_only:** merge, DoD judgment, integration, architecture lock
- **forbid:** undeclared image providers
- **default_reasoning:** `high`

## Design gate

- **human_north_star_approval_required:** true
- **personas_path:** `docs/personas.md`
- **persona_threshold:** "≥3/4 pass, zero P0"

## Engineering

- **test_commands:** `npm test && npm run typecheck`
- **graft_required:** true
- **branch_pattern:** `wp-<id>-short-slug`
- **merge_style:** `squash-via-pr`
- **secrets_path:** `~/.config/secrets/`
- **commit_policy:** commit only when human explicitly asks
- **self_improvement:** `on_commit`
- **skip_mocked_up_for_non_ui:** true
- **circuit_breaker_strikes:** 2

## Waivers

-
