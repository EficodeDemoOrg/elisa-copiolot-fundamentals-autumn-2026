# 3. Agent Mode Exercises

Learn to delegate bounded test tasks, review generated tests, and refactor reusable Robot keywords.

## Prerequisites

Complete [Getting Started](01-getting-started.md) and [Chat Panel](02-chat-panel.md). Keep the app running and the test environment activated. Review all edits and commands.

For data-changing tests, also paste these rules:
```text
Create fixtures through the existing API: a unique RF-QA-<run-id> column and
cards inside it. Save returned IDs immediately. Teardown must clean only owned
IDs, even after partial setup or assertion failure. Deleting a column also
deletes its cards: never delete seed/existing columns or reset the JSON file.
Allow cleanup 404 only for already-removed owned records. Report other errors.
Use fresh browser contexts per test, configurable URLs, and state-based waits.
```

## Exercise 3.1: Appearance and Browser Compatibility

The developer exercise adds dark/light mode. Here, inspect the existing appearance and test a current workflow across browsers. Do not implement a theme switch.

1. Select **Agent** and attach the [board header](../apps/web/src/components/BoardHeader.tsx), [styles](../apps/web/src/index.css), and [filtering logic](../apps/web/src/lib/board.ts). Prompt:
   ```text
   Confirm which appearance controls exist. Record unsupported theme scenarios
   as future work. Create tests/robot/suites/search.robot using Browser and
   RequestsLibrary. Read the API routes and follow our fixture ownership rules.
   Add one test: create two cards, search for one card's unique title, assert
   only it is visible, then Clear filters and assert both owned cards reappear.
   Scope assertions to our fixtures. Use BASE_URL=http://localhost:5890,
   API_URL=http://localhost:5891, BROWSER=chromium, and HEADLESS=${TRUE} variables.
   Capture a screenshot in the Robot output directory. Do not edit the app.
   ```
2. Review the diff. Ask `Which assertion proves the other card is filtered out, and how does cleanup work if an assertion fails?` Reject invented locators or unsafe cleanup.
3. Run the same suite in two engines. Approve the Firefox download first:
   ```bash
   python -m robot --variable BROWSER:chromium --outputdir tests/robot/results/search-chromium tests/robot/suites/search.robot
   rfbrowser init firefox
   python -m robot --variable BROWSER:firefox --outputdir tests/robot/results/search-firefox tests/robot/suites/search.robot
   ```
4. Inspect reports and screenshots for missing or clipped controls. Ask Copilot to summarize actual results in your QA notes. Record unavailable engines as **not run**, not passed. Confirm owned fixtures were removed.

**Checkpoint:** Search has execution evidence across available engines. Screenshots support manual appearance review. These runs do not prove Safari, mobile, or full visual-regression coverage.

## Exercise 3.2: Card Deletion Confirmation

The [card dialog](../apps/web/src/components/CardDialog.tsx) currently uses native JavaScript `confirm('Delete this card?')`, not an HTML modal. Test this behavior without replacing it.

1. Select **Ask**, attach the card dialog and [card routes](../apps/server/src/routes/cards.ts), and ask: `Explain cancel versus confirm outcomes and Browser library's native-dialog handling. Verify keywords against our installed version. Why must the handler be armed before clicking?`
2. Select **Agent**, attach your existing fixture resources, and prompt:
   ```text
   Create tests/robot/suites/deletion.robot with two independent cases:
   Cancel Keeps Card and Confirm Deletes Card. Give each its own owned fixtures.
   Open the owned card and arm the native-confirmation handler before Delete card.
   Cancel: assert the detail dialog remains open and GET /api/board contains
   the card ID. Confirm: assert the dialog closes, the card disappears from the
   board, and a fresh GET /api/board no longer contains its ID. Make these
   assertions before teardown. Reuse supported library keywords and resources.
   Do not invent a GET-card-by-ID endpoint or replace the native confirmation.
   ```
3. Review the assertions and run:
   ```bash
   python -m robot --outputdir tests/robot/results/deletion tests/robot/suites/deletion.robot
   ```
4. Inspect both cases in the log. If one fails, attach the first failing keyword and relevant screenshot in **Ask**: `Classify this as fixture, locator, dialog timing, API, or possible app defect. Cite evidence and suggest one discriminating check, not blanket retries.` Approve only justified test corrections and rerun. Report app defects separately.

**Checkpoint:** Both confirmation branches have UI/API evidence, independent fixtures, and safe cleanup. Unresolved failures remain visible, not hidden by weaker assertions.

## Exercise 3.3: Refactoring Reusable Keywords

1. Capture a passing baseline before refactoring:
   ```bash
   python -m robot --outputdir tests/robot/results/before-refactor tests/robot/suites
   ```
2. In **Ask**, attach your suites and resources. Prompt:
   ```text
   Analyze Robot keyword reuse. Find duplicated fixture setup, browser actions,
   or cleanup. Propose one small extraction into tests/robot/resources/ with
   clear arguments and callers. Preserve visible scenario intent and assertions.
   If reuse is already good, suggest one documentation improvement instead.
   Make no edits yet.
   ```
3. Review the proposal, select **Agent**, and prompt: `Implement only the approved test refactor. Preserve test names, assertions, isolation, and failure reporting. Add concise [Documentation] to the touched keywords. Do not edit application code or introduce custom helper scripts.`
4. Review moved assertions, then run a dry run and real tests:
   ```bash
   python -m robot --dryrun --outputdir tests/robot/results/refactor-dryrun tests/robot/suites
   python -m robot --outputdir tests/robot/results/after-refactor tests/robot/suites
   ```
   Ask Copilot to compare before/after test names and results. Check one moved assertion yourself. Equal pass counts alone do not prove equivalent coverage.

**Checkpoint:** Shared keywords are clearer, documentation explains their responsibilities, and the same scenarios still execute with their original assertions.