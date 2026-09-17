# 🧭 4. Plan mode exercises

In this exercise, you will learn how to
- Make an implementation plan for a feature
- Use handoffs to hand of the implementation from Plan mode to Agent mode

## ✅ Prerequisites

Select **Plan** in the Copilot chat panel. Select **Default Permissions** instead of using Autopilot.

Consider which models would be suitable for creating and implementing plans.

For plan creation, a model capable of deeper reasoning and greater context awareness is recommended, such Claude Opus 5. For a simpler code base such as this a less expensive model such as Claude Sonnet 5 can do the job.

When implementing the plan – assuming the plan is thorough and detailed – a less sophisticated model can be used. For instance GPT-5.3-Codex or GPT-5.6 Terra could be good choices.

For a thorough list of models and best use cases for them, see [the official documentation](https://docs.github.com/en/copilot/reference/ai-models/model-comparison). Check out the sections that discuss models for different types of tasks.

## 📋 Exercixe 4.1: Create and implement the plan
Let's suppose we want to implement a feature that enables adding checklists inside the cards.
1. Select Plan mode in the mode selector
1. Issue the following prompt:
    ```text
    Implement a feature that enables users to define checklists inside cards. When the checklists boxes are ticked, the progress of the checklist is updated above the tasklist, e.g. "3/7 done". 
    ```
1. Hit enter to start the planning. Plan mode may ask you questions to make clarification for the plan. Answer the questions and wait for the plan to finish.
1. When the plan finishes, review it carefully. If you are not happy about some aspect of the plan, refine the plan by asking Copilot to make changes into it.
1. When the plan is completed, Copilot offers you three options (handovers):
    - Start implementation
    - Implement using autopilot
    - Save plan in a file
   Choose "Implement using autopilot". This will start implementation in a mode where Copilot will autonomously decide what to do when it reaches a point of decisio in regards to e.g. implementation details.
1. When the implementation is ready, verify it in the UI.

## 🐘 Exercise 4.2: Plan migration from JSON to PostgreSQL
Let's suppose we want to migrate the current file-based data store into a PostgreSQL database while keeping all existing board functionality working.
1. Select Plan mode in the mode selector
1. Issue the following prompt:
    ```text
    Create an implementation plan to migrate the application data store from the current JSON file database into PostgreSQL. The plan should include:
    - A target schema for boards, columns, cards, labels, and their relationships
    - A migration approach for existing data so no current data is lost
    - A rollout strategy that minimizes downtime and risk
    - A rollback strategy in case migration fails
    - Validation and test steps to verify behavior remains unchanged after migration
    ```
1. Hit enter to start planning. Plan mode may ask clarifying questions about details such as database hosting, migration timing, and compatibility expectations. Answer the questions and wait for the plan to finish.
1. When the plan finishes, review it carefully. If you are not happy about some aspect of the plan, refine it by asking Copilot to improve specific parts such as schema details, migration sequencing, or rollback safety.
1. When the plan is completed, Copilot offers you three options (handovers):
    - Start implementation
    - Implement using autopilot
    - Save plan in a file
   Choose "Save plan in a file" so you can inspect migration phases and risk controls before implementation.
1. Open the created plan file and start implementation by explicitly referencing it in your next prompt so Copilot follows the agreed migration phases and constraints.
1. When the implementation is ready, verify it in the UI and by running relevant tests to confirm behavior matches the pre-migration version.

