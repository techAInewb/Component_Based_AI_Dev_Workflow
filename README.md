# AI-Assisted Component Development Workflow

A complete workflow and template system for solo developers building desktop applications using AI coding agents (specifically optimized for VS Code + Kilo/Cline).

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

---

## 📖 What Is a Component?

**A component is a complete feature, not necessarily a single file.**

### Complexity Determines Decomposition

**Simple Component:**
- Single file (e.g., `config_loader.py`)
- One Kilo prompt
- One testable outcome

**Complex Component:**
- Multiple files (e.g., "Download Model from Hugging Face")
- Multiple Kilo prompts (authenticate → fetch → download → save)
- Each prompt has one measurable, testable outcome
- Component validated when all pieces work together end-to-end

**Key Principle:** Component = feature boundary, not file count. Decomposition scales with complexity.

---

## 📚 What's Included

### Core Documentation
- **AI_Component_Development_Workflow.md** - Complete methodology guide (19k+ words)

### Project Templates (7 Documents)
All templates are minimal markdown scaffolds that provide structure without constraint:

**Planning Documents** (in `/Planning_Docs/` - for you + AI Assistant):
1. **PRD_template.md** - Product Requirements Document
2. **Implementation_Plan_template.md** - Build order and dependency tracking

**Execution Documents** (in `/Dev_Docs/` - provided to Kilo):
3. **Schema_template.md** - Data structure examples
4. **Naming_Standards_template.md** - Consistent naming conventions (pre-filled)
5. **Function_Registry_template.md** - Prevent function duplication
6. **Component_Registry_template.md** - Track component status and metrics
7. **API_Contract_template.md** - API specification (optional, use if needed)

---

## 🚀 Quick Start

### 1. Read the Master Workflow
Start by reading `AI_Component_Development_Workflow.md` to understand the complete methodology.

### 2. Start a New Project
Copy templates to your project directory:

```bash
# Planning docs for you + AI Assistant
cp -r Planning_Docs/ my-new-project/Planning_Docs/

# Execution docs for Kilo
cp -r Dev_Docs/ my-new-project/Dev_Docs/
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
- For complex components: Break into multiple atomic prompts

### 5. Validation Phase (You)
- Manual functionality testing
- Review registries for unexpected additions
- Update Component Registry status
- Each atomic prompt outcome must be tested

### 6. Integration Phase
Follow Implementation Plan checkpoints to connect components and test integration points.

---

## 🎓 Why This Workflow Exists

**Problem:** AI coding agents hallucinate, duplicate code, and generate fake passing tests.

**Solution:** This workflow prevents failures through:
- **Explicit schemas with examples** (prevents hallucination)
- **Function registries** (prevents duplication)
- **Build order enforcement** (prevents dependency issues)
- **Manual validation** (catches fake test success)
- **Component isolation** (reduces complexity)
- **Atomic prompting** (enables precise testing)

---

## 📖 Key Concepts

### Two-Tier Architecture
- **AI Assistant** maintains context, creates prompts, validates results
- **Kilo** is stateless, receives isolated instructions, implements code

### Component-Based Development
Build one complete feature at a time in dependency order. Validate before proceeding.

### Atomic Prompting for Complex Features
Break complex components into multiple prompts, each with one measurable outcome.

### Known Good State
Never build on unvalidated components. Always maintain a functional baseline.

### 300-Line File Limit
After 500 lines, AI coding agents' parsing degrades. We enforce 300-line maximum per file.

### Manual Validation
Passing unit tests don't guarantee working code. Human testing is mandatory.

---

## 🛠️ Technology Agnostic

While developed for desktop apps with Electron, this workflow adapts to:
- Any programming language
- Any framework
- Any AI coding agent that accepts prompts
- Mobile, web, or desktop platforms

---

## 📝 Documentation Philosophy

Templates provide **structure, not content**. Markdown headings create semantic guardrails that AI assistants understand naturally without verbose explanations.

Components are **features, not files**. Complexity dictates decomposition level.

---

## 🤝 Contributing

This workflow emerged from tracking 49+ function duplication errors across multiple MVP development cycles. It represents real-world lessons learned.

**Contributions welcome for:**
- Additional failure modes and solutions
- Framework-specific adaptations
- Integration with other AI coding tools
- Success stories and case studies

See CONTRIBUTING.md for guidelines.

---

## 📄 License

MIT License - Use freely, modify as needed, share improvements.

---

## 🙏 Credits

Developed through iterative refinement with AI assistants (Claude, Perplexity) as thought partners. Special recognition to the autistic pattern recognition that made tracking 49 duplication errors possible.

---

## 🔗 Related Resources

- [VS Code Kilo Extension](https://marketplace.visualstudio.com/)
- [Component-Based Architecture Principles](https://en.wikipedia.org/wiki/Component-based_software_engineering)
- [Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering)

---

## 💡 Philosophy

> "AI claims of completion mean nothing until you verify functionality yourself."

This workflow embodies human-in-the-loop development where AI accelerates implementation but humans validate reality.

---

**Built by developers, for developers who want to ship working code with AI assistance.**
