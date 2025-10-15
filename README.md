# AI-Assisted Component Development Workflow

A complete workflow and template system for solo developers building desktop applications using AI coding agents (specifically optimized for VS Code + Kilo/Claude).

## 🎯 What This Is

This repository provides a battle-tested workflow for component-based development using a two-tier AI approach:
- **Planning Tier:** You + AI Assistant create documentation and prompts
- **Execution Tier:** Kilo (or similar coding agent) implements components

**Key Features:**
- Prevents common AI coding failures (hallucination, scope creep, fake test success)
- Component-based architecture with dependency management
- Built-in function duplication prevention
- Manual validation over automated testing
- Proven through multiple MVP development cycles

## 📚 What's Included

### Core Documentation
- **AI_Component_Development_Workflow.md** - Complete methodology guide (17k+ words)

### Project Templates (7 Documents)
All templates are minimal markdown scaffolds that provide structure without constraint:

1. **PRD_template.md** - Product Requirements Document
2. **Implementation_Plan_template.md** - Build order and dependency tracking
3. **Schema_template.md** - Data structure examples
4. **Naming_Standards_template.md** - Consistent naming conventions (pre-filled)
5. **Function_Registry_template.md** - Prevent function duplication
6. **Component_Registry_template.md** - Track component status and metrics
7. **API_Contract_template.md** - API specification (optional, use if needed)

## 🚀 Quick Start

### 1. Read the Master Workflow
Start by reading `AI_Component_Development_Workflow.md` to understand the complete methodology.

### 2. Start a New Project
Copy all templates from the `templates/` folder to your project directory:

```bash
cp -r templates/ my-new-project/docs/
```

### 3. Planning Phase (You + AI Assistant)
Feed the master workflow document to your AI assistant, then work together to fill out:
- PRD (scope and boundaries)
- Implementation Plan (build order)
- Schema (data structures with examples)
- Function Registry (planned core functions)

### 4. Implementation Phase (Kilo)
Create prompts that include:
- Specific component from Implementation Plan
- Links to Schema, Naming Standards, Function Registry
- Explicit constraints (300-line file limit, etc.)

### 5. Validation Phase (You)
- Manual functionality testing
- Review registries for unexpected additions
- Update Component Registry status

### 6. Integration Phase
Follow Implementation Plan checkpoints to connect components and test integration points.

## 🎓 Why This Workflow Exists

**Problem:** AI coding agents hallucinate, duplicate code, and generate fake passing tests.

**Solution:** This workflow prevents failures through:
- **Explicit schemas with examples** (prevents hallucination)
- **Function registries** (prevents duplication)
- **Build order enforcement** (prevents dependency issues)
- **Manual validation** (catches fake test success)
- **Component isolation** (reduces complexity)

## 📖 Key Concepts

### Two-Tier Architecture
- **AI Assistant** maintains context, creates prompts, validates results
- **Kilo** is stateless, receives isolated instructions, implements code

### Component-Based Development
Build one component at a time in dependency order. Validate before proceeding.

### Known Good State
Never build on unvalidated components. Always maintain a functional baseline.

### 300-Line File Limit
After 500 lines, AI coding agents' parsing degrades. We enforce 300-line maximum.

### Manual Validation
Passing unit tests don't guarantee working code. Human testing is mandatory.

## 🛠️ Technology Agnostic

While developed for desktop apps with Electron, this workflow adapts to:
- Any programming language
- Any framework
- Any AI coding agent that accepts prompts
- Mobile, web, or desktop platforms

## 📝 Documentation Philosophy

Templates provide **structure, not content**. Markdown headings create semantic guardrails that AI assistants understand naturally without verbose explanations.

## 🤝 Contributing

This workflow emerged from tracking 149+ AI implementation and coding errors across multiple successful MVP development cycles. It represents real-world lessons learned to the development of complex desktop applications.

**Contributions welcome for:**
- Additional failure modes and solutions
- Framework-specific adaptations
- Integration with other AI coding tools
- Success stories and case studies

## 📄 License

MIT License - Use freely, modify as needed, share improvements.

## 🙏 Credits

Developed by Ryan Connelly through iterative refinement with AI assistants as thought partners.

## 🔗 Related Resources

- [VS Code Kilo Extension](https://marketplace.visualstudio.com/)
- [Component-Based Architecture Principles](https://en.wikipedia.org/wiki/Component-based_software_engineering)
- [Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

## 💡 Philosophy

> "AI claims of completion mean nothing until you verify functionality yourself."

This workflow embodies human-in-the-loop development where AI accelerates implementation but humans validate reality.

---

**Built by developers, for developers who want to ship working code with AI assistance.**
