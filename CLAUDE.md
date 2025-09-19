# Multi-Agent AI System Development Guidelines

Auto-generated from feature plans. Last updated: 2025-09-18

## Project Overview
Educational project template for summer school students building multi-agent AI systems using Python, LangGraph, and Chainlit.

## Active Technologies
- **Language**: Python 3.11+ (required for async LangGraph features)
- **Package Manager**: UV (10-100x faster than pip)
- **Agent Framework**: LangGraph (stateful multi-agent orchestration)
- **UI Framework**: Chainlit (conversational interface with LangGraph integration)
- **LLM Integration**: LangChain ecosystem (OpenAI, Anthropic, etc.)
- **Testing**: pytest for unit/integration tests

## Project Structure
```
src/
├── agents/          # Individual agent implementations
├── models/          # Data models and entities
├── workflows/       # LangGraph workflow definitions
├── ui/             # Chainlit interface components
└── main.py         # Application entry point

tests/
├── contract/       # Contract testing for agent interactions
├── integration/    # End-to-end workflow testing
└── unit/          # Individual component testing

outputs/           # Generated documents by session
examples/          # Sample workflows and demos
docs/             # Detailed documentation
```

## Development Commands
```bash
# Project setup
uv sync                           # Install dependencies
uv add <package>                  # Add new dependency

# Development
uv run chainlit run src/main.py --watch  # Start dev server
uv run pytest                    # Run tests
uv run pytest --cov              # Run tests with coverage

# Agent development
uv run python scripts/test_agent.py  # Test individual agents
uv run python scripts/validate_workflow.py  # Validate LangGraph workflows
```

## Code Style
- **Async/Await**: Use async patterns for LangGraph integration
- **Type Hints**: Required for all public interfaces
- **Docstrings**: Document agent behaviors and workflow stages
- **Error Handling**: Graceful fallbacks for LLM API failures
- **Configuration**: Use environment variables for API keys and settings

## Agent Development Patterns

### Agent Implementation
```python
from langchain_core.messages import HumanMessage
from langgraph.prebuilt import ToolNode

class RequirementsAgent:
    """Generates structured requirements from clarified user input."""

    async def process(self, state: WorkflowState) -> dict:
        # Agent logic here
        return {"requirements_document": result}
```

### Workflow Definition
```python
from langgraph.graph import StateGraph, END

workflow = StateGraph(WorkflowState)
workflow.add_node("clarification", clarification_agent)
workflow.add_node("requirements", requirements_agent)
workflow.add_edge("clarification", "requirements")
```

### Chainlit Integration
```python
@cl.on_message
async def handle_message(message: cl.Message):
    # Stream workflow execution
    async for chunk in workflow.astream({"user_input": message.content}):
        # Update UI with agent progress
```

## Testing Guidelines

### Contract Tests
Test agent input/output contracts match specifications in `/contracts/`

### Integration Tests
Test complete workflows from user input to document generation

### Unit Tests
Test individual agent logic and data model validation

## Educational Considerations

### Learning Objectives
- Multi-agent collaboration patterns
- Software development workflows
- Requirements engineering
- Technical decision making
- Quality assurance processes

### Student Onboarding
- 15-minute quickstart from setup to running system
- Clear documentation of agent roles and responsibilities
- Progressive examples from simple to complex
- Visible agent reasoning for educational value

## Recent Changes
- 001-i-want-to: Added Python 3.11+, UV, LangGraph, Chainlit stack for multi-agent educational system

<!-- MANUAL ADDITIONS START -->
<!-- Add custom development notes, team conventions, or project-specific guidelines here -->
<!-- MANUAL ADDITIONS END -->