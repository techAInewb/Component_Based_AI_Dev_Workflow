# Quick Start Guide

## Your First Project with This Workflow

### Step 1: Setup (5 minutes)

1. **Copy templates to your project:**
   ```bash
   mkdir my-project/docs
   cp templates/* my-project/docs/
   ```

2. **Open your AI assistant** (Claude, ChatGPT, Perplexity, etc.)

3. **Upload these files to your AI assistant:**
   - `AI_Component_Development_Workflow.md`
   - All template files from `docs/`

4. **Start the conversation:**
   ```
   "I'm starting a new desktop application project using the AI-Assisted 
   Component Development Workflow. I've uploaded the master workflow and 
   all templates. Let's begin planning."
   ```

---

### Step 2: Planning Phase (30-60 minutes)

Work with your AI assistant to fill out these documents in order:

#### A. Product Requirements Document (PRD)
**Prompt your AI assistant:**
```
"Let's fill out the PRD template. My project is [brief description]. 
Help me define the MVP scope, components, and exclusions."
```

**What you'll define:**
- Core functionality (what it does)
- 3-5 main components
- Success criteria
- What you're NOT building

#### B. Implementation Plan
**Prompt your AI assistant:**
```
"Based on the PRD, help me create an Implementation Plan with build 
order. Which components have no dependencies and can be built first?"
```

**What you'll create:**
- Build Order 1: Foundation (no dependencies)
- Build Order 2+: Components that depend on Order 1
- Integration checkpoints between orders

#### C. Schema Document
**Prompt your AI assistant:**
```
"For each component in the Implementation Plan, help me define the 
data structures with concrete examples."
```

**What you'll provide:**
- Database/storage formats with example values
- API request/response formats (if applicable)
- Configuration file structures

#### D. Function Registry
**Prompt your AI assistant:**
```
"Based on our Implementation Plan, what are the core functions we'll 
need for each component? Let's populate the Function Registry."
```

**What you'll list:**
- Key functions for each component
- File locations (estimated)
- Import statements

---

### Step 3: First Component Implementation (30 minutes)

#### A. Create Kilo Prompt
**Work with your AI assistant:**
```
"I'm ready to implement [Component Name] from Build Order 1. Help me 
create a comprehensive Kilo prompt following the workflow guidelines."
```

Your prompt should include:
- Component purpose and scope
- Links to Schema sections
- Links to Naming Standards
- Current Function Registry excerpt
- 300-line file limit reminder
- Explicit instruction to check Function Registry before creating functions

#### B. Run Kilo Architect Mode
1. Paste prompt into Kilo
2. Use architect mode to generate implementation ToDo list.
3. Review plan with your AI assistant
4. Approve and execute

#### C. Review Implementation
1. Kilo updates Component Registry and Function Registry
2. Copy Kilo's response and paste into AI assistant session
3. Review with AI assistant:
   - Any unexpected functions created?
   - Files within 300-line limit?
   - Implementation matches schema?

---

### Step 4: Validation (15 minutes)

#### A. Manual Testing
1. Run your application: `npm run dev` (or appropriate command)
2. Test the component functionality manually
3. Verify it works as expected

#### B. Update Documentation
**Tell your AI assistant:**
```
"Component [Name] passed manual validation. Update the Component 
Registry status to VALIDATED."
```

#### C. Decision Point
- ✅ **Component works?** → Proceed to next component
- ❌ **Component broken?** → Debug issue, or rollback via Kilo checkpoint, revise prompt

---

### Step 5: Repeat for Remaining Components

For each subsequent component:
1. Consult Implementation Plan for build order
2. Verify dependencies are VALIDATED
3. Create Kilo prompt (include all context docs)
4. Implement → Review → Test → Validate
5. Update Component Registry

---

### Step 6: Integration Testing

After completing a full build order:
1. Refer to Integration Checkpoint in Implementation Plan
2. Test component connections manually
3. Verify data flows correctly between components
4. Update Component Registry to INTEGRATED

---

## Common First-Time Mistakes

### ❌ Skipping Schema Examples
**Don't:** "User object has name and email fields"  
**Do:** 
```json
{
  "userId": "550e8400-e29b-41d4-a716-446655440000",
  "name": "John Doe",
  "email": "john@example.com"
}
```

### ❌ Building Out of Order
**Don't:** Build User Profile before User Authentication exists  
**Do:** Follow Implementation Plan build order strictly

### ❌ Trusting Passing Tests
**Don't:** "Tests pass, ship it!"  
**Do:** Manually run and test every component

### ❌ Ignoring 300-Line Limit
**Don't:** Let files grow to 500+ lines  
**Do:** Split into modules when approaching 300 lines

---

## Expected Timeline (First Project)

| Phase | Time | Output |
|-------|------|--------|
| Planning | 1-2 hours | All docs filled out |
| First Component | 1 hour | Working, validated component |
| Subsequent Components | 30-45 min each | Component library grows |
| Integration | 30 min per checkpoint | Verified connections |

**Total for 5-component MVP:** ~8-10 hours spread over 2-3 days

---

## Getting Help

### If Kilo hallucinates:
1. Check Schema Document - are examples explicit?
2. Check Function Registry - was it included in prompt?
3. Rollback and add more specific constraints

### If components won't integrate:
1. Check Schema Document - do data formats match?
2. Check Implementation Plan - are dependencies validated?
3. Test components individually first

### If functions are duplicated:
1. Check Function Registry - was it updated by Kilo?
2. Check Naming Standards - are you following conventions?
3. Search registry before next implementation

---

## Success Indicators

You're on the right track if:
- ✅ No component depends on unvalidated components
- ✅ Function Registry grows predictably with each component
- ✅ No files exceed 300 lines
- ✅ Integration testing finds issues early, not at the end
- ✅ AI assistant helps troubleshoot by referencing docs

---

## Next Steps After Your First MVP

1. **Archive your docs** - Save filled templates as reference
2. **Document lessons learned** - What worked? What didn't?
3. **Refine prompts** - Save successful Kilo prompts as templates
4. **Update workflow** - Found a better way? Document it
5. **Share experience** - Open an issue or PR with improvements

---

**Ready to start? Create your first project folder and begin with the PRD!**
