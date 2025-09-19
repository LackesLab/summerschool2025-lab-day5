# Data Model: Multi-Agent AI System

**Feature**: Multi-Agent AI System Project Template
**Date**: 2025-09-18
**Status**: Draft

## Entity Overview

This data model defines the core entities for a multi-agent AI system that collaborates on feature development through a chat interface. All entities support the educational workflow from user input to final implementation documents.

## Core Entities

### FeatureRequest

**Purpose**: Represents a user-submitted feature description and its lifecycle

**Attributes**:
- `id`: Unique identifier (UUID)
- `original_text`: Raw user input description
- `timestamp`: Creation time (ISO 8601)
- `clarified_text`: Refined description after clarification process
- `status`: Enumeration [submitted, clarifying, processing, completed, failed]
- `session_id`: Links to student session
- `priority`: Optional priority level [low, medium, high]

**Validation Rules**:
- `original_text` must be non-empty, max 2000 characters
- `status` transitions: submitted → clarifying → processing → completed/failed
- `clarified_text` required before status can move to processing

**State Transitions**:
```
submitted → clarifying (when clarification questions generated)
clarifying → processing (when user answers all questions)
processing → completed (when all agents finish successfully)
processing → failed (when agent collaboration fails)
```

### Agent

**Purpose**: Represents an AI agent with specific role and current state

**Attributes**:
- `id`: Unique identifier (UUID)
- `name`: Human-readable name (e.g., "Clarification Agent")
- `role`: Enumeration [clarification, requirements, technical, product, testing]
- `status`: Enumeration [idle, active, completed, error]
- `current_task`: Description of active work
- `workflow_id`: Links to current workflow
- `capabilities`: List of supported operations
- `model_config`: LLM configuration parameters

**Validation Rules**:
- Each `role` can have only one active agent per workflow
- `status` must align with workflow progression
- `current_task` required when status is active

**Relationships**:
- Belongs to WorkflowStage
- Produces AgentOutput entries

### WorkflowStage

**Purpose**: Represents a discrete step in the feature development process

**Attributes**:
- `id`: Unique identifier (UUID)
- `name`: Stage name (e.g., "Requirements Analysis")
- `type`: Enumeration [clarification, requirements, tech_analysis, product_review, testing]
- `status`: Enumeration [pending, in_progress, completed, failed]
- `started_at`: Stage start time
- `completed_at`: Stage completion time
- `feature_request_id`: Links to parent feature request
- `prerequisites`: List of stage IDs that must complete first
- `parallel_allowed`: Boolean indicating if stage can run parallel to others

**Validation Rules**:
- All prerequisites must be completed before stage can start
- Completion time must be after start time
- Status progression: pending → in_progress → completed/failed

**Dependencies**:
- Clarification stage has no prerequisites
- Requirements stage requires clarification completion
- Technical/Product/Testing stages can run in parallel after requirements

### GeneratedDocument

**Purpose**: Represents structured output from agent collaboration

**Attributes**:
- `id`: Unique identifier (UUID)
- `title`: Document title
- `content`: Markdown-formatted content
- `document_type`: Enumeration [requirements, technical_analysis, product_review, implementation_guide, test_strategy]
- `generated_by`: Agent ID that created document
- `workflow_stage_id`: Links to producing stage
- `file_path`: Local file system path
- `created_at`: Generation timestamp
- `version`: Version number for iterative updates
- `template_used`: Reference to document template

**Validation Rules**:
- Content must be valid markdown
- File path must be writable and within project boundaries
- Version increments for updates to same document type in workflow

**File Organization**:
```
outputs/
├── {session_id}/
│   ├── {feature_request_id}/
│   │   ├── requirements.md
│   │   ├── technical_analysis.md
│   │   ├── product_review.md
│   │   ├── implementation_guide.md
│   │   └── test_strategy.md
```

### StudentSession

**Purpose**: Represents an individual learning session with progress tracking

**Attributes**:
- `id`: Unique identifier (UUID)
- `student_name`: Optional student identifier
- `started_at`: Session start time
- `last_activity`: Most recent interaction timestamp
- `feature_requests`: List of feature request IDs
- `progress_milestones`: Completed learning objectives
- `repository_path`: Project workspace directory
- `settings`: User preferences and configuration

**Validation Rules**:
- Session expires after 24 hours of inactivity
- Repository path must be valid and accessible
- Progress milestones append-only for learning tracking

### AgentOutput

**Purpose**: Captures intermediate results and agent reasoning for transparency

**Attributes**:
- `id`: Unique identifier (UUID)
- `agent_id`: Producing agent
- `content`: Structured output data
- `output_type`: Enumeration [clarification_questions, analysis_fragment, review_comment, final_document]
- `timestamp`: Creation time
- `confidence_score`: Agent's confidence in output (0.0-1.0)
- `reasoning`: Explanation of agent's decision process
- `citations`: Sources or context used

**Validation Rules**:
- Confidence score between 0.0 and 1.0
- Reasoning required for all outputs
- Content structure varies by output_type

## Relationships

### Primary Relationships
```
StudentSession 1:N FeatureRequest
FeatureRequest 1:N WorkflowStage
WorkflowStage 1:N Agent
Agent 1:N AgentOutput
WorkflowStage 1:N GeneratedDocument
```

### Cross-Entity Links
- `AgentOutput` references `GeneratedDocument` for final outputs
- `GeneratedDocument` can reference other documents for iterative updates
- `WorkflowStage` dependencies create DAG structure

## State Management

### Workflow Progression
1. **Submission**: FeatureRequest created with status 'submitted'
2. **Clarification**: Clarification agent activates, generates questions
3. **Processing**: Multiple agents work on parallel stages
4. **Completion**: Final documents generated, workflow marked complete

### Error Handling
- Agent failures mark their stage as 'failed'
- Failed stages can be retried with same or different agents
- Dependent stages wait for prerequisite recovery
- Complete workflow failure preserves partial results

### Persistence Strategy
- **In-Memory**: Active workflow state, agent status
- **File System**: Generated documents, session data
- **Metadata**: JSON files for entity relationships and history

## Validation Schema

### Data Integrity
- All timestamps in UTC ISO 8601 format
- UUIDs follow RFC 4122 standard
- File paths validated against project boundaries
- Markdown content validated for basic syntax

### Business Rules
- Maximum 3 active feature requests per session
- Agent collaboration timeout after 5 minutes
- Document regeneration preserves version history
- Failed workflows cleanly release resources

## Integration Points

### LangGraph Integration
- Agents map to LangGraph nodes
- WorkflowStage represents graph execution state
- AgentOutput captures intermediate node results

### Chainlit Integration
- StudentSession maps to Chainlit chat session
- Real-time updates via websocket for agent progress
- File downloads for GeneratedDocument access

### Educational Extensions
- Progress tracking for learning objectives
- Agent reasoning visualization
- Workflow replay for educational review

**Data Model Status**: ✅ Complete - Ready for contract definition and implementation