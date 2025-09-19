# Quickstart Guide: Multi-Agent AI System

**Target Time**: 15 minutes from clone to running system
**Prerequisites**: Python 3.11+, internet connection
**Learning Outcome**: Understand multi-agent collaboration patterns and build first feature workflow

## Quick Setup (5 minutes)

### 1. Environment Setup
```bash
# Clone the project template
git clone <repository-url> multi-agent-lab
cd multi-agent-lab

# Install UV package manager (if not already installed)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Initialize project and install dependencies
uv sync
```

### 2. Configuration
```bash
# Copy environment template
cp .env.example .env

# Add your LLM API key (choose one)
echo "OPENAI_API_KEY=your_key_here" >> .env
# OR
echo "ANTHROPIC_API_KEY=your_key_here" >> .env
```

### 3. Launch Application
```bash
# Start the Chainlit interface
uv run chainlit run src/main.py --watch
```

**Expected Result**: Browser opens to `http://localhost:8000` with chat interface

## First Feature Workflow (10 minutes)

### Step 1: Submit Feature Request
In the chat interface, type:
```
I want to build a user authentication system for my web application.
Users should be able to register, login, and reset their passwords.
```

**What happens**:
- System analyzes your input
- Clarification agent activates if needed
- Workflow status appears in sidebar

### Step 2: Answer Clarification Questions
The clarification agent may ask follow-up questions like:
- "What authentication method do you prefer? (email/password, OAuth, SSO)"
- "Do you need user profile management features?"
- "What are your security requirements?"

**Learning Point**: Notice how the agent identifies ambiguities automatically

### Step 3: Watch Agent Collaboration
Observe the real-time agent activity:
- **Requirements Agent**: Generates structured requirements document
- **Technical Agent**: Analyzes architecture and tech stack
- **Product Agent**: Reviews from business perspective
- **Testing Agent**: Creates testing strategy

**Learning Point**: Each agent has specialized knowledge and perspective

### Step 4: Review Generated Documents
Click download links for generated documents:
- `requirements.md` - Functional and non-functional requirements
- `technical_analysis.md` - Architecture recommendations
- `product_review.md` - Business feasibility assessment
- `test_strategy.md` - Comprehensive testing approach

**Learning Point**: Systematic software development process captured in documents

## Understanding the System

### Agent Roles Explained

**Clarification Agent**:
- Identifies unclear or ambiguous statements
- Asks targeted follow-up questions
- Ensures complete feature understanding
- *Educational Value*: Shows importance of requirement clarity

**Requirements Agent**:
- Converts user needs into structured requirements
- Creates acceptance criteria for each requirement
- Prioritizes features using MoSCoW method
- *Educational Value*: Demonstrates requirements engineering

**Technical Agent**:
- Recommends architecture patterns
- Suggests technology stack choices
- Identifies implementation challenges
- *Educational Value*: Technical decision-making process

**Product Agent**:
- Evaluates business value and feasibility
- Considers user experience implications
- Assesses market fit and competition
- *Educational Value*: Product management perspective

**Testing Agent**:
- Designs comprehensive testing strategy
- Creates specific test cases for requirements
- Plans different testing levels (unit, integration, system)
- *Educational Value*: Quality assurance methodology

### Repository Structure
```
multi-agent-lab/
├── src/
│   ├── agents/          # Individual agent implementations
│   ├── models/          # Data models and entities
│   ├── workflows/       # LangGraph workflow definitions
│   ├── ui/             # Chainlit interface components
│   └── main.py         # Application entry point
├── outputs/            # Generated documents by session
├── tests/              # Test suite
├── examples/           # Sample workflows and demos
├── docs/              # Detailed documentation
└── pyproject.toml     # Project configuration
```

## Try More Examples

### Example 2: E-commerce Feature
```
Create a shopping cart system where users can add products,
update quantities, and proceed to checkout.
```

### Example 3: Analytics Dashboard
```
Build a dashboard that shows user engagement metrics
with interactive charts and real-time updates.
```

### Example 4: File Processing System
```
Design a system that processes uploaded CSV files,
validates data, and generates summary reports.
```

## Advanced Learning Exercises

### Exercise 1: Agent Customization
1. Modify the Technical Agent to prefer specific technologies
2. Update prompts in `src/agents/technical_agent.py`
3. Test with same feature request - observe different recommendations

### Exercise 2: New Agent Type
1. Create a "Security Agent" that focuses on security considerations
2. Add security review stage to workflow
3. Generate security assessment documents

### Exercise 3: Custom Workflow
1. Design workflow for different domain (mobile apps, data science, etc.)
2. Modify agent collaboration pattern
3. Test with domain-specific feature requests

## Troubleshooting

### Common Issues

**"API key not found" error**:
- Verify `.env` file has correct API key
- Restart application after adding key

**Slow agent responses**:
- Check internet connection
- Verify API rate limits not exceeded
- Try with simpler feature description

**Documents not generating**:
- Check `outputs/` directory permissions
- Verify disk space available
- Review agent logs in terminal

**Chat interface not loading**:
- Confirm Python 3.11+ installed
- Check all dependencies installed with `uv sync`
- Try different browser or clear cache

### Getting Help

**Debug Mode**:
```bash
# Run with verbose logging
uv run chainlit run src/main.py --debug
```

**Check Agent Status**:
- Monitor workflow progress in browser sidebar
- Review agent reasoning in downloaded documents
- Check terminal output for detailed logs

## Next Steps

### For Students
1. **Experiment** with different types of feature requests
2. **Analyze** how agents make decisions and recommendations
3. **Customize** agent prompts and behaviors
4. **Extend** system with new agent types or workflows

### For Instructors
1. **Review** generated documents for teaching examples
2. **Assign** specific feature types for learning objectives
3. **Discuss** agent reasoning and decision-making processes
4. **Explore** different software development methodologies

### Advanced Topics
- Custom LLM integration
- Multi-language support
- Integration with external tools
- Production deployment patterns

## Validation Checklist

After completing quickstart, you should be able to:
- [ ] Submit feature requests via chat interface
- [ ] Interact with clarification questions
- [ ] Monitor real-time agent collaboration
- [ ] Download and review generated documents
- [ ] Understand each agent's role and contribution
- [ ] Navigate the repository structure
- [ ] Troubleshoot common issues

**Success Criteria**: Complete workflow from feature description to implementation documents in under 15 minutes

## Learning Objectives Achieved

✅ **Multi-Agent Systems**: Understand how AI agents collaborate
✅ **Software Development Process**: See systematic approach to feature development
✅ **Requirements Engineering**: Learn structured requirement gathering
✅ **Technical Decision Making**: Observe architecture and technology choices
✅ **Quality Assurance**: Understand comprehensive testing strategies
✅ **Product Management**: See business perspective on features

**Ready for**: Advanced exercises, custom implementations, and deeper exploration of AI agent patterns.