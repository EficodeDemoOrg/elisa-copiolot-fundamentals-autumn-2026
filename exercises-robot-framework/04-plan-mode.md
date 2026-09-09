# 4. Plan Mode Exercises

Learn to review requirements, create QA plans, and hand off approved documentation work to Agent mode.

## Prerequisites

Complete [Getting Started](01-getting-started.md), [Chat Panel](02-chat-panel.md), and [Agent Mode](03-agent-mode.md). Bring your coverage notes and Robot test results.

Select **Plan** in Copilot Chat. If unavailable, use **Ask** with "Plan only. Do not edit or run anything." Handoff labels vary by version. Select **Agent** manually when needed. Review permissions instead of choosing autopilot.

## Exercise 4.1: Create and Hand Off a Test Plan

The developer exercise implements card checklists. Here, review that proposed feature as a tester. Checklist controls are not implemented in the current app.

1. Select **Plan** and attach the [card dialog](../apps/web/src/components/CardDialog.tsx) and [shared types](../packages/shared/src/index.ts). Prompt:
   ```text
   Plan QA for this proposed requirement: "Users can define checklists inside
   cards. Ticking boxes updates progress above the checklist, e.g. 3/7 done."
   Verify current implementation, then identify missing, ambiguous, or untestable
   acceptance criteria. Ask me three important clarification questions first.
   Consider empty lists, deleting checked items, and persistence after reload.
   Produce at most five prioritized scenarios with data, actions, expected
   results, and requirement links. Separate agreed criteria from assumptions.
   Mark checklist scenarios FUTURE / NOT EXECUTABLE. Do not implement the
   feature, invent endpoints, or create tests expecting nonexistent controls.
   ```
2. Answer with instructor-approved assumptions or **product decision needed**. Review the plan and ask Copilot to replace one vague criterion with a measurable example. Check that unanswered questions remain visible.
3. Hand off to **Agent**, attach the reviewed plan, and prompt:
   ```text
   Save only the approved QA plan to tests/robot/docs/checklist-test-plan.md.
   Preserve open questions and future/not-executable labels. Do not implement
   the feature, generate runnable checklist tests, or edit application files.
   ```
4. Review the saved document. Select one scenario and ask **Ask** mode: `Which requirement supports this expected result, and what must exist before this scenario can execute?` Verify the answer against the plan and current UI.

**Checkpoint:** A reviewed test plan has measurable proposed criteria and explicit blockers. Saving a plan does not establish test coverage or a passing result.

## Exercise 4.2: Plan JSON-to-PostgreSQL Migration Validation

The app currently uses lowdb with a local JSON file. There is no configured PostgreSQL database. Plan migration testing without installing or migrating anything.

1. Select **Plan** and attach the [database implementation](../apps/server/src/db.ts), [seed data](../apps/server/data/db.seed.json), [shared types](../packages/shared/src/index.ts), and your API test. Prompt:
   ```text
   Create a QA validation plan for a future JSON-to-PostgreSQL migration that
   preserves existing board behavior. Do not plan application implementation.
   Inventory boards, columns, cards, labels, members, and their relationships.
   Cover preservation of IDs, ordering, optional dates, and label/assignee links.
   Include before/after comparisons, existing UI/API regression tests, rollback
   validation, and measurable go/no-go criteria. Counts alone are insufficient.
   Ask about the target schema, isolated test environment, and rollback policy.
   Separate checks executable today from database checks blocked by missing
   infrastructure or decisions. Use synthetic data. Never request secrets or
   propose destructive resets. Do not install drivers or run migration tools.
   ```
2. Review the draft. Ask `What data loss could equal record counts miss? What evidence would demonstrate a successful rollback?` Record unknown schema or environment details as undecided, not invented facts.
3. Use **Save plan** if available, or switch to **Agent** with the reviewed plan and prompt:
   ```text
   Save only tests/robot/docs/storage-migration-test-plan.md. Keep future
   PostgreSQL checks marked blocked. Do not implement migrations, add database
   dependencies, execute database commands, or modify application configuration.
   ```
4. Run the existing read-only API test against today's JSON-backed app:
   ```bash
   python -m robot --outputdir tests/robot/results/storage-baseline tests/robot/suites/api.robot
   ```
   Attach the test and result summary in **Ask**: `Which plan claims does this run support, and which remain untested? Explain why response-shape checks do not prove persistence or migration success.` Add the real baseline outcome to the plan. Leave PostgreSQL checks **not run / blocked**.

**Checkpoint:** The plan distinguishes current baseline evidence from future database and rollback checks. No application or database changes were made.