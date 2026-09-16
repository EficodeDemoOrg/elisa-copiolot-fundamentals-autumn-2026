# 🗺️ 3. Plan and Agent Mode Exercises

In these exercises, you will:
- Select suitable models for planning and implementation
- Create plans for QA-related improvements
- Refine the plans with Copilot until they are satisfactory
- Hand off a finalized plan to an implementation agent
- Save a finalized plan in a separate file, then use it to guide an implementation agent in a separate chat context

## ✅ Prerequisites

Select **Plan** in the Copilot chat panel. Select **Default Permissions** instead of using Autopilot.

Consider which models would be suitable for creating and implementing plans.

For plan creation, a model capable of deeper reasoning and greater context awareness is recommended, such Claude Opus 5. For a simpler code base such as this a less expensive model such as Claude Sonnet 5 can do the job.

When implementing the plan – assuming the plan is thorough and detailed – a less sophisticated model can be used. For instance GPT-5.3-Codex or GPT-5.6 Terra could be good choices.

## 🧪 Exercise 3.1: Smoke test suite

1. Ensure **Plan** is selected in the Copilot chat panel. Ask Copilot to inspect the application and the existing Robot Framework tests, then create a smoke test suite plan:
	```text
	Create a plan for a Robot Framework smoke test suite for the whole Kanban application. Inspect the application and existing tests first. Limit the number of test cases to 10 most critical ones.

	Describe the test cases at a conceptual level. For each test case, state what it should test and its expected result. Prioritize important user-visible workflows. Focus on test intent rather than low-level implementation details.
	```

1. Review the proposed plan. Answer any questions the plan agent may have. Review tha plan and if needed, ask Copilot to improve it until it covers the most critical paths e.g. in board interactions, cards, columns, labels, and filtering.

1. Next let's move to the implementation phase. First select a model you want to use for the immplementation of the plan, e.g. GPT-5.6 Terra, After that click on the **Start Implementation** button to hand off the finalized plan to an implementation agent.

1. Validate the generated tests by reviewing each test case. Check that its workflow and assertions make sense and match the expected application behavior. Ask Copilot to correct any issues, then run the full test suite and review the results.

## 🗄️ Exercise 3.2: Development environment test data strategy

1. Let's plan a mechanism for initializing/resettig the local development environment database with test data. Ensure **Plan** is selected in the Copilot chat panel. Ask Copilot to inspect the existing database and seed setup, then create a plan:
	```text
	Create a plan for a mechanism that lets a tester initialize or reset the Kanban application's development database with known test data. Inspect the existing database and seed setup first.

	Also design a rich, realistic data set for regression and exploratory testing. It should represent the application's important entities, relationships, states, and useful edge cases. Make initialization repeatable and convenient for testers. Do not implement anything yet.
	```

1. Review the proposed plan and ask Copilot to improve it until the initialization mechanism is clear and the data set provides broad, meaningful test coverage.

1. Select **Open in Editor** to open the finalized plan in a separate file. Save it as `test-data-plan.prompt.md` in the workspace.

1. Open a new Copilot chat, select **Agent**, and choose a suitable model for implementation. Type `#`, select the saved plan file, and ask the agent to implement it:
	```text
	Implement #test-data-plan.prompt.md
	```

1. Test the implementation by using the new mechanism to initialize the development database. Start the application and inspect it in a browser. Confirm that the planned data is present and that its important variations and edge cases are displayed correctly.
