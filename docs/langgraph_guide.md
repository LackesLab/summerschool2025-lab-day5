# LangGraph Primer

This guide explains how the template uses LangGraph to orchestrate agent workflows and how you can extend the graph for the full multi-agent experience.

## Current Workflow

`src/workflows/example_workflow.py` now compiles a single-node chat graph:

```python
graph = StateGraph(WorkflowState)
graph.add_node("model", generate_reply)
graph.set_entry_point("model")
graph.add_edge("model", END)
```

- `WorkflowState` stores a `messages` list annotated with `add_messages`, so LangGraph appends the LLM response to the existing conversation automatically.
- `generate_reply` calls either the OpenRouter-backed ChatOpenAI instance or a local echo fallback and returns `{"messages": [ai_message], "response": ai_message.content}`.
- `src/main.py` keeps the compiled graph in memory and feeds it the running conversation each time Chainlit receives a message.

## Adding New Nodes

1. Create an async function that accepts the shared state and returns a partial state update, e.g. `{ "clarifications": [...] }`.
2. Register the node with `graph.add_node("clarification", clarification_agent)`.
3. Link execution order with `graph.add_edge("clarification", "requirements")`.
4. Recompile the graph before use by calling `graph.compile()`.

Nodes run sequentially by default. To run branches in parallel, register multiple edges from a node and ensure the downstream state keys do not overwrite each other unintentionally.

## Maintaining State

- Store immutable user inputs on the state to make every node deterministic.
- Use distinct keys (`clarifications`, `requirements`, `technical_review`) for each agent output.
- When writing to disk, prefer the utilities in `src/utils/file_utils.py` so directory structures stay consistent.

## Error Handling

- Wrap `ainvoke()` calls in try/except blocks and surface user-friendly messages when things fail (see `src/main.py`).
- Use `utils.logging.get_logger()` for structured logging to both console and `outputs/logs/app.log`.
- Consider returning fallback messages in each node to avoid terminating the whole graph on recoverable issues.

## Next Steps for Students

- Introduce a supervisor node that routes between agent stages based on conversation context.
- Stream incremental results back to Chainlit using LangGraph's async generator APIs.
- Add checkpointing (LangGraph Checkpoint) for long-running workflows so users can revisit partial progress.
- Experiment with parallel branches, e.g. run product and testing agents simultaneously once requirements are ready.
