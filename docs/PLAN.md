# Autonoannounce Plan (v0.1)

## Goal
Ship a production-usable local TTS queue skill with measurable foreground speed and clear operations docs.

## Scope (v0.1)
1. Baseline skill in repo (`skills/local-tts-queue`) with benchmark harness and references.
2. Fast foreground benchmark mode (default compact/no-status).
3. Full diagnostic mode for deep troubleshooting.
4. Runbook + config contract + perf SLO docs.
5. Initial GitHub project hygiene (milestone, issues, branch protection).

## Non-goals (for now)
- Full queue architecture refactor (coalescing/priority/TTL/prefetch)
- Multi-host playback orchestration
- Rich dashboarding/observability UI

## Definition of Done
- Skill is in repo and runnable.
- README points to plan + quickstart benchmark command.
- Milestone and issues exist for tracked execution.
- Main branch is protected (PR required).
