# 3. Agent mode exercises

In these exercises, you will learn how to implement complete features using agent mode. Agent mode is an autonomous, goal-oriented mode that iterates on a task until it is completed. It can read, write, and edit files, search for relevant context, and use built-in and MCP-provided tools.

## ✅ Prerequisites
https://docs.github.com/en/copilot/reference/ai-models/model-comparison#task-deep-reasoning-and-debugging

Select **Agent** in the Copilot chat panel. Select **Default Permissions** instead of using Autopilot.

While doing the exercises, consider which models would be suitable in different parts of the exercises.
* For small, simple changes and completions, `GPT-5.6 Luna` or `Claude Haiku 4.5` can be good choises.
* For most everyday coding tasks, `Claude Sonet 5` or `GPT-5.6 Terra` are good options
* For tasks that require heavy reasoning, `GPT-5.6 Sol` and `Claude Opus 5` can be good options, but use them cautiosly as they come with a cost.

## 🌗 Exercise 3.1: Implementation of dark / light modes
1. Make sure the [development environment is running](../README.md#-getting-started) and open it in your browser at `http://localhost:5890/`. Familiarize yourself with the user interface to get an idea what kind of application you're developing.
1. Open the Copilot chat panel and select the agent mode in the mode selector.
1. Let's start by creating a prompt to implement a dark/light mode switch:
    ```text
    Implement dark / light mode switch for the UI. Use the current color schema as the dark mode.
    ```
1. When the implementation finishes, check the results in the UI. 

## 🗑️ Exercise 3.2: Modal window for card deletion
Currently, when you are deleting a card in the UI, a standard JavaScript alert window appears. Let's change this to a nicer modal window.

1. Try to delete one of the cards in the UI. Can you see the boring JavaScript alert popping up?
1. Issue the following prompt to make it prettier: 
    ```text
    When a user clicks on "Delete card", a standard JavaScript alert window appears. Let's replace this with a modal window with look & feel that corresponds to the rest of the UI.
    ```
1. Verify that the implementation was successful by testing card deletion in the user interface.

## 🛠️ Exercise 3.3: Refactoring with agent mode
Agent mode can also be used for refactoring code.

1. Open `apps/web/src/lib/board.ts`. 
1. The `filterCards` function currently packs all rules into one function. Let's refactor it into clearer helper functions. Select the function code to target it with a prompt, then issue this prompt:
    ```text
    Refactor this function by splitting complex predicate logic into named helpers.
    ```
1. Verify that the refactoring cleaned up the code by moving the predicate logic into helpers.
