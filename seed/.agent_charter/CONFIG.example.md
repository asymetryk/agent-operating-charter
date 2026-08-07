---
# Copy to CONFIG.md during SETUP. Do not commit secrets.
setup_complete: false
setup_completed_at: null
repo_name: ""
---

# Agent Charter — project config

## Tracker

- **wp_status_authority:** ``       # e.g. OpenProject | Linear | Jira | GitHub Issues | Other
- **wp_status_location:** ``        # project URL / id
- **non_project_tracker:** ``       # optional: adhoc / reminders only
- **evidence_log:** ``              # where screenshots, test logs, comments go
- **assumptions_log:** ``           # wiki page, doc path, or tracker field

## Viewport (screenshot target — not the UAT host)

- **primary_viewport:** `1920x1080`
- **secondary_viewports_mvp:** none
- **browser:** Chrome

## Environments & UAT

- **uat_host:** ``                  # e.g. shared workstation, VM pool, k8s, cloud preview
- **uat_runtime:** ``               # e.g. devcontainer | docker-compose | bare | paas
- **uat_url_or_path:** ``           # primary URL, or use uat_instances below
- **uat_instances:** ``             # optional pool, e.g. A/B rows: label | lan | https
- **uat_if_busy:** `spin_new`       # spin_new = use free instance or provision another; wait | fail
- **localhost_default:** false
- **preview_env:** ``               # optional pre-prod
- **production_env:** ``
- **promote_order:** ``             # e.g. UAT → preview → production
- **prod_gate:** ``                 # what must be green before production

## Model routing

- **plan_review:** ``
- **implement:** ``
- **bulk:** ``
- **imagegen:** ``                  # declared image path only
- **parent_only:** merge, DoD judgment, integration, architecture lock
- **forbid:** ``                    # e.g. undeclared image providers
- **default_reasoning:** ``         # e.g. high | medium

## Design gate

- **human_north_star_approval_required:** true
- **personas_path:** ``
- **persona_threshold:** "≥3/4 pass, zero P0"

## Engineering

- **test_commands:** ``
- **graft_required:** false
- **branch_pattern:** "wp-<id>-short-slug"
- **merge_style:** ``               # ff-only-after-rebase | squash-via-pr | other
- **secrets_path:** ``
- **commit_policy:** "commit only when human explicitly asks"
- **self_improvement:** `on_commit`
- **skip_mocked_up_for_non_ui:** true
- **circuit_breaker_strikes:** 2

## Waivers

<!-- Human-approved deviations, with date and reason -->

-
