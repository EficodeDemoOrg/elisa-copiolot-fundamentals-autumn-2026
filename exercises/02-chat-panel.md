# 💬 2. Chat Panel Exercises

In these exercises, you will learn how to:
- Ask questions about the project
- Use slash commands
- Add context explicitly

## 💬 Exercise 2.1: Asking basic questions
Ask mode is great for learning about the project you're working on and its technologies. Its tool selection is restricted to reading and research, so it won't be able to make changes, even if it wanted to. However, it can propose code; it's up to you to explicitly include that code from the chat panel in the files.

1. Open Copilot Chat by pressing `Cmd+Shift+I` (Mac) or `Ctrl+Shift+I` (Windows/Linux), or click the speech bubble icon next to the search bar at the top.
1. Select "Ask" from the Agent menu below the chat input field.
1. Type the following prompts:
    **Introduce the app features**
    ```text
    Tell me about the board application's main features
    ```
    **Running the unit tests**
   ```text
   How do I run unit tests in this project?
   ```
   **Starting the development server**
   ```text
   How do I start the development server?
   ```

## 🧰 Exercise 2.2: Essential slash commands
Slash commands are shortcuts that enable you to quickly perform common tasks in Copilot without extensive typing. 

### Unit test generation
`/tests` is a great way to quickly generate unit tests for selected code.

1. Select `Agent` in the agent menu.
1. Open `apps/web/src/lib/board.ts`
1. Select one function in the file and prompt:
    ```text
    /tests
    ```
1. Copilot should propose test cases for the function in the chat window. When it's done, ask Copilot to implement them by prompting simply:
    ```text
    Implement
    ```

### Other useful slash commands
Also try the following useful slash commands.

1. **Open a new chat session.** A new, clean chat session can be opened by prompting:
    ```text
    /clear
    ```
    This can also be achieved by clicking on the plus icon at the top of the chat panel.
1. **Explain selected code.** Select a piece of code and prompt:
    ```text
    /explain
    ```

1. **Propose a fix for the problems in the selected code.** Make a breaking change somewhere in the code and use this prompt to fix it:
    ```text
    /fix
    ```

## 🧭 Exercise 2.3: Adding context
Providing the right context for Copilot is essential in making it work optimally. Copilot is good at finding relevant context autonomously, but you can also use # to explicitly add specific information into the context. 

Try the following prompts to test adding explicit context. Make sure you're using the **Ask agent** by selecting it in the agent menu.

1. **File references.** Write # + filename and accept the file suggestion with Tab. Copilot will turn this into a file reference => #file:<filename>
    ```text
    #file:db.ts What's the purpose of this file?
    ```
1. **Last terminal command.** Explain what happened in the last terminal command and its output. In the terminal, run this (faulty) command:
    ```bash
    npm start dev
    ```
    Now analyze the error message using Copilot:
    ```text
    #terminalLastCommand What did I do wrong?
    ```
1. **Terminal selection.** You can also select specific lines on the terminal and use this reference to inject it into the context:
    ```text
    #terminalSelection explain the stack trace
    ```
1. **Problems.** Add IDE-detected problems to the context to solve them using Copilot:
    ```text
    #problems What's causing this error?
    ```
