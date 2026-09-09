# 2. Chat Panel Exercises

Learn to ask useful testing questions, generate an API test with slash commands, and provide failure context.

## Prerequisites

Complete [Getting Started](01-getting-started.md). Keep the app running and the test environment activated.

Use **Ask** for investigation and **Agent** only for approved test edits. Attach files through **Add Context** or the `#` picker. If a slash command is unavailable, send the same prompt without the slash command. Use the new-chat button instead of `/clear`.

## Exercise 2.1: Asking Questions and Finding Coverage Gaps

1. Select **Ask**. Attach your Robot smoke suite, [filtering logic](../apps/web/src/lib/board.ts), and [existing unit tests](../apps/web/src/lib/board.test.ts).
2. Prompt:
   ```text
   Explain the Kanban app's main workflows to a tester and how to run our Robot
   tests versus npm test. Compare existing Robot coverage with source behavior.
   Identify three missing Robot scenarios, including filter boundary cases.
   For each, give source evidence, test data, action, expected result, and risk.
   Do not count Vitest tests as Robot coverage or claim unrun tests have passed.
   Distinguish observed implementation from approved requirements. Make no edits.
   ```
3. Challenge one suggestion: `Show the source or existing assertion supporting this claim. Otherwise mark it as an assumption.` Check that claim in the UI.
4. Ask Copilot to format the three reviewed gaps as a small Markdown coverage table. Place it in your test-side QA notes for later exercises.

**Checkpoint:** Three concrete coverage gaps are supported by evidence, not invented features or a guessed coverage percentage.

## Exercise 2.2: Essential Slash Commands

1. Select **Agent**. Attach the [board route](../apps/server/src/routes/board.ts), [route registration](../apps/server/src/index.ts), and [shared types](../packages/shared/src/index.ts). Prompt:
   ```text
   /tests Create tests/robot/suites/api.robot using RequestsLibrary, not Vitest.
   Add one read-only GET /api/board test with API_URL=http://localhost:5891.
   Assert status 200, parse the JSON with library APIs, and verify the board
   has name plus columns, cards, labels, and members collections of list type.
   Do not assume seed names, IDs, or counts. Close sessions in teardown.
   Do not edit application files. Explain the generated Robot assertions.
   ```
2. Review the diff. The response is the board object itself, not nested under a `board` key. Run:
   ```bash
   python -m robot --outputdir tests/robot/results/api tests/robot/suites/api.robot
   ```
3. Confirm **1 test, 1 passed, 0 failed** and inspect its report. Switch to **Ask**, select the request and assertions, and prompt:
   ```text
   /explain Explain these Robot steps and their likely failure messages.
   Which incorrect responses could return 200 but still fail our assertions?
   ```
4. Start a clean chat with `/clear` or the new-chat button. Reattach relevant files. Do not assume earlier context carries over.

**Checkpoint:** A passing API test checks response content as well as status, and you can explain its assertions.

## Exercise 2.3: Adding Context to Diagnose Failures

1. In the API test only, deliberately change the expected status from `200` to `418`. Run it with a separate output directory:
   ```bash
   python -m robot --outputdir tests/robot/results/api-failure tests/robot/suites/api.robot
   ```
2. Select **Ask**. Attach the API test and **last terminal command** from the `#` picker, often named `#terminalLastCommand`. Prompt:
   ```text
   /fix Explain this failure before proposing edits. I deliberately changed
   the expected status. Compare expected and actual with the board route.
   Suggest the smallest test-only correction. Do not accept arbitrary statuses,
   ignore errors, remove assertions, or change the application.
   ```
3. Select the failing keyword's output and add **terminal selection** context, often `#terminalSelection`. Ask `Does this excerpt show a setup error or an executed assertion failure? What evidence tells you?` If the picker options are unavailable, paste the command and a short sanitized excerpt. Use **Problems** context for editor diagnostics, not runtime assertions.
4. Restore the correct expectation yourself, or approve that one edit in **Agent**. Rerun the API command from Exercise 2.2 and confirm it passes with content assertions intact.

**Checkpoint:** Copilot diagnosed an actual failure from explicit context, and you verified a narrow correction without modifying the app.

Optional: Repeat the diagnostic prompt in fresh chats with two available models and identical context. Compare accuracy and clarity. Choose a model based on evidence, not its name.