# 🚀 1. Getting started exercises

In these exercises you will:
- Set up Copilot in your IDE
- Test inline completions
- Test the chat panel

### VS Code Setup

VS Code ships with a built-in Copilot extension. To make sure it's enabled:
1. Open the Extensions panel
1. Search for GitHub Copilot Chat
1. If it's not enabled, click on "Enable AI features"

GitHub Copilot requires an active subscription. Verify your subscription:
1. Open VS Code
1. Look for the Copilot icon in the status bar (bottom right)
1. Click on the icon. If it shows your subscription and AI credits, you're already authenticated. If you see the text "Sign in" next to the icon, click on it and proceed with authentication.

### Visual Studio Setup
For Visual Studio instructions, see the [official documentation](https://learn.microsoft.com/en-us/visualstudio/ide/visual-studio-github-copilot-install-and-states?view=visualstudio).

### Setting up the playground application
Check out the [README](../README.md#-getting-started) at the project root for instructions on how to build and run the application.

## ✍️ Exercise 1.1: Test Inline Completion
1. Open the file in `app/server/src/utils.ts`
1. Start typing the following. Copilot should start making suggestions on how to implement the rest of the function.
    ```ts
    function validateUsername(
    ````
1. Press tab to accept the suggested code.
1. Now let's generate a function from a comment. Write the following comment in the same file:
    ```ts
    // A function that returns the difference between two dates in milliseconds    
    ```
1. Wait for a moment. Copilot should make a suggestion of the implementation. Use `tab` to accept and `Esc` to dismiss it.

## 💬 Exercise 1.2: Test Copilot Chat panel
Let's make sure Copilot is functioning correctly.

1. Open Copilot Chat by pressing `Cmd+Shift+I` (Mac) or `Ctrl+Shift+I` (Windows/Linux), or click the speech bubble icon next to the search bar at the top.
1. Select "Ask" from the Agent menu below the chat input field.
1. Type the following prompt:
   ```text
    Tell me about the application in this repository
   ```
1. Copilot should respond with an explanation.
