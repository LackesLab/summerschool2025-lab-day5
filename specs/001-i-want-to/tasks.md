# Tasks: Multi-Agent AI System Project Template Setup

**Scope**: Create foundational project template for students to build upon
**Students will implement**: Agent logic, complex workflows, document generation, advanced features

## Architecture Overview
```
Basic Chainlit UI (@cl.on_message)
    ↓
Simple LangGraph example (1 node)
    ↓
File structure for student development
```

## Template Foundation Structure
```
src/
├── agents/          # (Empty - students implement)
├── workflows/       # Basic example + structure
├── utils/           # Helper functions
└── main.py         # Working Chainlit app

outputs/            # Directory for generated documents
examples/           # Sample inputs for testing
docs/              # Student guides and exercises
tests/             # Basic test structure
```

## Phase 3.1: Project Setup
- [x] T001 Create UV project with pyproject.toml (Python 3.11+, LangGraph, Chainlit, LangChain)
- [x] T002 [P] Create directory structure (src/, outputs/, examples/, docs/, tests/)
- [x] T003 [P] Setup .env.example with LLM API key placeholders
- [x] T004 [P] Create .gitignore for Python/AI project
- [x] T005 [P] Setup basic pytest configuration

## Phase 3.2: Basic Chainlit UI
- [x] T006 Create working Chainlit app in src/main.py with @cl.on_message
- [x] T007 [P] Add basic session handling (@cl.on_chat_start)
- [x] T008 [P] Create simple message response (echo user input)
- [x] T009 [P] Add basic file upload capability for future document downloads

## Phase 3.3: Simple LangGraph Example
- [x] T010 Create basic WorkflowState class in src/workflows/state.py
- [x] T011 Implement simple "echo agent" node in src/workflows/example_workflow.py
- [x] T012 Connect LangGraph workflow to Chainlit in src/main.py
- [x] T013 [P] Add basic error handling for workflow execution

## Phase 3.4: File Structure & Utilities
- [x] T014 [P] Create outputs directory structure with session folders
- [x] T015 [P] Add basic file utility functions in src/utils/file_utils.py
- [x] T016 [P] Create placeholder files in src/agents/ with docstring templates
- [x] T017 [P] Add basic logging configuration in src/utils/logging.py

## Phase 3.5: Documentation & Examples
- [x] T018 [P] Create comprehensive README.md with setup and architecture explanation
- [x] T019 [P] Add sample feature requests in examples/sample_requests.txt
- [x] T020 [P] Create student exercise guide in docs/exercises.md
- [x] T021 [P] Document the basic LangGraph pattern in docs/langgraph_guide.md

## Phase 3.6: Testing Foundation
- [x] T022 [P] Create basic test for Chainlit message handling in tests/test_main.py
- [x] T023 [P] Add test for simple workflow execution in tests/test_workflow.py
- [x] T024 [P] Create test structure templates for students

## Dependencies
- T001 → All other tasks (project setup first)
- T006-T009 → T012 (Chainlit before LangGraph integration)
- T010-T011 → T012 (workflow components before integration)
- T014-T017 can run in parallel with UI/workflow tasks

## Parallel Execution Examples
```bash
# Setup phase:
Task: "Create directory structure (src/, outputs/, examples/, docs/, tests/)"
Task: "Setup .env.example with LLM API key placeholders"
Task: "Create .gitignore for Python/AI project"
Task: "Setup basic pytest configuration"

# Documentation phase:
Task: "Create comprehensive README.md with setup and architecture explanation"
Task: "Add sample feature requests in examples/sample_requests.txt"
Task: "Create student exercise guide in docs/exercises.md"
Task: "Document the basic LangGraph pattern in docs/langgraph_guide.md"
```

## What Students Will Build
The template provides foundation for students to implement:

### Agent Development
- `src/agents/clarification_agent.py` - Analyze user input for clarification needs
- `src/agents/requirements_agent.py` - Generate structured requirements
- `src/agents/technical_agent.py` - Technical analysis and recommendations
- `src/agents/product_agent.py` - Product management perspective
- `src/agents/testing_agent.py` - Testing strategy and test plans

### Advanced Workflows
- Multi-agent collaboration patterns
- Parallel agent execution
- Error handling and recovery
- Real-time progress streaming

### Document Generation
- Markdown document creation
- File organization by session
- Download functionality
- Template-based generation

### UI Enhancements
- Real-time agent progress display
- Document preview and download
- Session management
- Error display and handling

## Success Criteria for Template
1. ✅ `uv sync && uv run chainlit run src/main.py` works immediately
2. ✅ Students can chat with basic echo functionality
3. ✅ Simple LangGraph example demonstrates the pattern
4. ✅ Clear file structure for student development
5. ✅ Comprehensive documentation for 15-minute onboarding
6. ✅ Students understand how to extend with their own agents

## Validation Checklist
- [ ] Project runs immediately after clone and `uv sync`
- [ ] Basic chat interface functional
- [ ] Simple LangGraph workflow executes
- [ ] File structure supports planned student development
- [ ] Documentation enables 15-minute onboarding
- [ ] Clear extension points for student implementation
