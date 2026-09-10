# 💬 2. Chat Panel Exercises

In these exercises you will:
- Use slash commands as short hands for common prompts
- Use Copilot to answer questions and fix broken test cases
- Use Copilot to investigate which parts of the app need test automation the most
- Use Copilot to implement new test cases
- Add explicit contents to the prompt context

## ⌨️ Exercise 2.1: Essential Slash Commands

1. Make sure you have selected `Agent` in the agent selector menu (where other possible choices are Ask and Plan).

1. Open the models selector in the chat panel. Browse through the different models: high reasoning models like GPT-6 Astra or Claude Opus models, or the simpler models like Claude Haiku 4.5 or GPT-5 mini. Hover with your mouse on the model names to compare their costs in AI credits. *Note:* it depends on your organization which models are available. For the following exercises, select one of the lightweight models such as Claude Haiku 4.5 or Auto, which is a good default selection.

1. Type `/` in the chat. You should see a list of `slash commands` opening. Browse through the commands.

1. Open smoke.robot file, select one of the test cases by activating its text with your mouse. Note that you can see in the chat text field the file that is open and the activated rows of text: Copilot will automatically insert these into the *prompt context*. Send the following prompt to Copilot:

   ```
   /explain
   ```
You should receive a thorough explanation of the test case.

1. Issue `/clear` slash command to *archive the current chat session and to start a new one.*
   ```
   /clear
   ```

1. Make a deliberate error in the smoke.robot file (e.g. a typo in one of the key words). Select the code of the test case with the mouse and issue the following simple prompt:
   ```
   /fix
   ```
Review the proposed fix. If you're happy with it, tell Copilot to proceed with the fix:
   ```
   Implement the proposed fix
   ```

## 🤖 Exercise 2.2: Asking Questions and Planning Initial Robot Coverage

The following exercises call for a model capable of slightly deaper reasoning. Select e.g. GPT-5.6 Terra/Sol or Claude Sonnet 5 in the model selector of the chat panel.

1. Select **Ask** in the agent selector of the chat panel.

1. Prompt:
   ```text
   Identify three high-value scenarios in the Kanban application for which Robot Framework  test cases should be written first. Focus on end-to-end user-visible behavior, especially board interaction and filtering.
   
   For each scenario, provide the workflow goal, suggested test data, user actions, expected result, and risk if untested. Make no edits in the code or test cases. 
   ```
1. Select **Agent** in the agent selector of the chat panel.

1. Ask Copilot to implement one of the suggested test cases. Example:

   ```
   Implement a Robot Framework Browser end-to-end test for filtering Kanban cards by label according to your test case suggestion. Validate the new test after implementing it. Do not make any edits in the code base.
   ```

## 🔍 Exercise 2.3: Adding Context to Diagnose Failures

Switch back to a lightweight model for the following exercises.

1. Use `#` to add files to the context window:
   ```
   /explain #smoke.robot
   ```

1. Make a question about the official Robot Framework documentation:
   ```
   Check in the lastest Robot Framework documentation if variable names are case-sensitive or not #web https://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html
   ```

1. Make a deliberate error in one of the test cases and run the tests in the terminal. Use Copilot to detect the problem by prompting:

   ```
   Explain why the test cases failed #terminalLastCommand
   ```

1. Select a specific line in the terminal output and make a question about it using #terminalSelection chat variable.
