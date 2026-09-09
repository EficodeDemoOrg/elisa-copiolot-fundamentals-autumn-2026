# 🚀 01. Getting Started Exercises (Robot Framework Edition)

Learn to set up Robot Framework with Copilot, use inline completions, and ask questions about the Kanban app. No application programming is required.

## ✅ Prerequisites

### VS Code Setup

VS Code ships with a built-in Copilot extension. To make sure it's enabled:
1. Open the Extensions panel.
1. Search for GitHub Copilot Chat.
1. If it's not enabled, click "Enable AI features".

GitHub Copilot requires an active subscription. Verify your subscription:
1. Open VS Code.
1. Look for the Copilot icon in the status bar (bottom right).
1. Click the icon. If it shows your subscription and AI credits, you're already authenticated. If you see the text "Sign in" next to the icon, click it and follow the sign-in steps.

### Visual Studio Setup
For Visual Studio instructions, see the [official documentation](https://learn.microsoft.com/en-us/visualstudio/ide/visual-studio-github-copilot-install-and-states?view=visualstudio).

### Setting Up the Playground Application
Check out the [README](../README.md#-getting-started) at the project root for instructions on how to build and run the application.

Note: The playground application must be running in a separate terminal for the exercises to work.

## 🛠️ Exercise 1.1: Set Up Robot Framework and Validate It

1. Open the Copilot Chat panel. Select **Agent** and send these prompts one at a time. Review each result before continuing.
   ```text
   Prepare Robot Framework with Browser and RequestsLibrary under tests/robot/. Put the dependencies in requirements.txt. Do not install them or change application code yet. Do not generate any test cases yet.
   ```

1. Review the generated files and, if necessary, ask Copilot to explain them to you:
   ```text
   Explain the purpose of #requirements.txt.
   ```
   Note: Start typing `#requirements.txt` and select the correct file when it appears. The result in the chat panel will look like this: `#file:requirements.txt`.


1. Create and activate an isolated environment using the commands for your shell:
   **macOS / Linux:**
   ```bash
   python3 -m venv tests/robot/.venv
   source tests/robot/.venv/bin/activate
   ```
   **Windows PowerShell:**
   ```powershell
   py -m venv tests/robot/.venv
   .\tests\robot\.venv\Scripts\Activate.ps1
   ```

1. In the activated environment, install the dependencies and the browser:
   ```bash
   python -m pip install -r tests/robot/requirements.txt
   rfbrowser init chromium
   ```

1. Ask Copilot (with **Agent** still selected) to generate a smoke test:
   ```text
   Create one simple read-only smoke test in tests/robot/suites/smoke.robot that verifies that the board loads. Inspect the app to choose useful checks. Only create the test case, do not run it.
   ```

1. Run the smoke test in the activated environment:
   ```bash
   python -m robot --outputdir tests/robot/results/smoke tests/robot/suites/smoke.robot
   ```

1. Confirm **1 test, 1 passed, 0 failed**. Open the generated report and keyword log from the output directory in your browser. If setup or execution fails, attach the relevant terminal output in **Ask** mode:
   ```text
   Explain the first failure: environment, unavailable app, locator, or assertion?
   Suggest one next check and the smallest test-only correction. Do not remove
   assertions. Give the rerun command and distinguish a dry run from real execution.
   ```

**Checkpoint:** A real browser test passes before you continue. Reactivate this environment in each new test terminal.

## ✍️ Exercise 1.2: Test Inline Completion

**Note:** Inline completions will not work if your IDE identifies the file as a plain text file. Either install the RobotCode extension (VS Code) or enable Copilot for plain text files in your IDE settings (in VS Code, open Settings and search for `github.copilot.enable`).

1. Open your smoke suite. Add a test named `Labels Control Is Visible`, copying the browser/context/page setup from the existing test.

1. Type this indented comment and wait for Copilot's inline suggestion:
   ```robotframework
       # Assert that the Labels button in the board header is visible.
   ```

1. Accept the suggestion with `Tab` or dismiss it with `Esc`.

1. Rerun the smoke command above. Check that both tests pass. If a test fails, select the failing test's code and ask Copilot:
   ```
   Explain why this test fails and suggest a fix. See #terminalLastCommand for the error message.
   ```
The chat variable `#terminalLastCommand` appends the last command run in the terminal and its output to your prompt.

**Checkpoint:** You verified an inline suggestion against the UI and executed it.
