# Student Exercises

Use these exercises to explore the template and expand the multi-agent workflow incrementally.

## Exercise 1: Customize the Chat Workflow
- Modify `src/workflows/example_workflow.py` to post-process the LLM reply (e.g., append a static checklist or confidence score).
- Update `src/main.py` to store the enriched reply using `save_text()` from `src/utils/file_utils.py`.
- Validate behaviour manually through the Chainlit UI.

## Exercise 2: Prompt the Clarification Agent
- Implement `ClarificationAgent.run()` so it returns two clarifying questions when the raw input lacks details such as audience or success metrics.
- Add a new node to the workflow that calls the agent and streams its questions back to the user.
- Record the clarifying questions in the session directory for later review.

## Exercise 3: Generate Requirements Drafts
- Use `RequirementsAgent.run()` to transform clarified inputs into a basic Markdown document.
- Persist the document under `outputs/documents/requirements_<session>.md` using the file utilities.
- Share your prompt engineering notes in `docs/` alongside the quickstart guide.

## Exercise 4: Testing Foundations
- Create unit tests for the helper functions in `src/utils/file_utils.py`.
- Write an integration test that injects a stub LLM into the workflow and asserts the crafted response (or the fallback notice).
- Run tests with `uv run pytest` and capture results in your pull request.

## Exercise 5: Product and Testing Feedback Loops
- Populate `ProductAgent.run()` and `TestingAgent.run()` with templated analyses.
- Update the workflow graph to incorporate both agents after the requirements step.
- Surface their outputs in the Chainlit UI and store them in the session directory for download.
