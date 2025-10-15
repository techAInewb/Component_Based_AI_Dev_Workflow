# AI-Assisted Component Development Workflow

## Purpose
This workflow is designed for solo developers or small teams using a two-tier AI development approach: an AI assistant for planning and prompt creation, paired with Kilo (coding agent) for implementation. It emphasizes component-based, incremental development with human validation at every step.

---

## Two-Tier AI Development Architecture

### Planning Tier (You + AI Assistant)
- Create and maintain all planning documentation
- Determine component build order and dependencies  
- Construct detailed prompts for Kilo
- Validate implementation results
- Maintain project context across sessions

### Execution Tier (Kilo Coding Agent)
- Receives isolated, self-contained prompts with embedded documentation
- Has no memory between tasks
- Implements specific components based on explicit instructions
- Updates tracking documents (Component Registry, Function Registry)
- Uses Kilo checkpoints for rollback capability

**Key Principle**: Kilo is stateless. All context must be provided in each prompt via linked documentation.

---

## Development Phases

### Phase 1: Planning & Documentation (You + AI Assistant)
**Goal**: Define the complete project architecture before any code is written.

**Activities**:
1. Create Product Requirements Document (PRD)
2. Create Implementation Plan with build order
3. Create Schema Document with examples
4. Create Naming Standards document
5. Create Function Registry with planned functions
6. Create API Contract (if applicable)
7. Initialize Component Registry

**Output**: Complete planning documentation set that prevents hallucination and scope creep.

---

### Phase 2: Component Implementation (Kilo)
**Goal**: Build one component at a time in dependency order.

**Activities**:
1. Consult Implementation Plan for next component in build order
2. You and AI Assistant create Kilo prompt including:
   - Component specification from PRD
   - Links to Schema Document
   - Links to Naming Standards
   - Current Function Registry
   - Explicit file structure and line limits
   - Exact runtime commands (e.g., "npm run dev")
3. Kilo architect mode creates implementation plan
4. Review and approve plan with AI Assistant
5. Kilo implements component
6. Kilo updates Component Registry and Function Registry

**Output**: Implemented component with updated registries.

---

### Phase 3: Validation (You + AI Assistant)
**Goal**: Verify component functions correctly before integration.

**Activities**:
1. Kilo provides code manifest - paste into AI Assistant session
2. Review Function Registry for unexpected additions
3. Manual functionality testing by you
4. Verify component stays within 300-line file limits
5. Check for function duplication
6. Update Component Registry status to VALIDATED

**Rollback Triggers**:
- Kilo created functions not in Function Registry → Immediate rollback
- File exceeds 300 lines → Rollback, redesign as modules
- Implementation diverges from schema → Rollback, clarify schema
- Three failed iterations on same component → Rollback, rethink approach

**Output**: Validated component ready for integration.

---

### Phase 4: Integration Testing (You)
**Goal**: Verify components work together as defined in Implementation Plan.

**Activities**:
1. Follow Integration Plan checkpoints
2. Connect components per dependency graph
3. Manual testing of integration points
4. Verify data flows between components
5. Update Component Registry status to INTEGRATED

**Output**: Integrated, functional component cluster.

---

## Document Structure

### Planning Documents (You + AI Assistant - Never Given to Kilo)

#### 1. Product Requirements Document (PRD)
**Purpose**: Define MVP scope and boundaries.

**Contents**:
- MVP scope definition
- Component list with clear boundaries
- Success criteria per component
- **Explicit exclusions** (what NOT to build)
- User stories or use cases
- Acceptance criteria

**Why**: Prevents Issue #2 (Scope creep). Provides clear boundaries for what Kilo should build.

---

#### 2. Implementation Plan
**Purpose**: Orchestrate component build order and integration strategy.

**Contents**:
```markdown
# Implementation Plan

## Build Order 1: Foundation Components
**No dependencies**

### Database Connection Component
- Functions: connectDB(), closeDB(), query()
- Files: database.py (~100 lines)
- Dependencies: None
- Integration: Used by all data components

### Configuration Manager Component
- Functions: loadConfig(), getConfig(), saveConfig()
- Files: config.py (~80 lines)
- Dependencies: None
- Integration: Used by all components

## Build Order 2: Authentication Layer
**Depends on: Build Order 1**

### User Authentication Component
- Functions: validateCredentials(), login(), logout(), hashPassword()
- Files: auth_module.py (~150 lines), auth_utils.py (~60 lines)
- Dependencies: Database Connection, Configuration Manager
- Integration: Used by User Profile, Session Manager

## Integration Checkpoint 1
Test all Build Order 1-2 connections before proceeding.

## Build Order 3: User Management
**Depends on: Build Order 2**
[Continue pattern...]
```

**Why**: 
- Prevents building components before their dependencies exist
- Identifies integration test points
- Provides visual dependency graph
- Guides prompt sequencing

**Never provided to Kilo** - Used by you and AI Assistant to maintain development direction.

---

### Execution Documents (Provided to Kilo in Prompts)

#### 3. Schema Document
**Purpose**: Provide explicit data structure examples to prevent hallucination.

**Contents**:
- Database schemas with field types
- API request/response formats with examples
- Configuration file structures
- Data validation rules
- TypeScript interfaces or equivalent

**Example**:
```json
{
  "user": {
    "userId": "string (UUID)",
    "email": "string (valid email format)",
    "passwordHash": "string (bcrypt hash)",
    "createdAt": "ISO 8601 timestamp"
  }
}
```

**Why**: Prevents Issue #1 (Improper implementation). Kilo implements what you show, not what it invents.

---

#### 4. Naming Standards
**Purpose**: Ensure consistent naming to prevent semantic duplication.

**Contents**:
```markdown
# Naming Standards

## Functions
- Validation: validate{Noun}() - e.g., validateEmail()
- Retrieval: get{Noun}() - e.g., getUser()
- Storage: save{Noun}() - e.g., saveSettings()
- Boolean checks: is{Adjective}() - e.g., isValid()

## Constants
- ALL_CAPS_SNAKE_CASE - e.g., MAX_RETRY_COUNT, API_BASE_URL

## Classes/Components
- PascalCase - e.g., UserAuthentication, DataSync

## Shared Variables (cross-file)
- camelCase - e.g., currentUser, appConfig

## Files/Modules
- snake_case or kebab-case per framework convention
- Maximum 300 lines before modular refactoring required
```

**Why**: Prevents Issue #3 (Semantic duplication). `validateEmail()` vs `checkEmailValidity()` vs `isEmailValid()` all become `validateEmail()`.

---

#### 5. Function Registry
**Purpose**: Track all functions with location and import to prevent duplication.

**Format** (one line per function):
```
functionName(params) -> returnType | filepath.py | import {functionName} from './filepath'
```

**Example**:
```markdown
# Function Registry

validateEmail(email) -> bool | auth_utils.py | import {validateEmail} from './auth_utils'
hashPassword(pwd) -> str | auth_utils.py | import {hashPassword} from './auth_utils'
connectDB() -> Connection | database.py | import {connectDB} from './database'
sanitizeInput(input) -> str | auth_utils.py | import {sanitizeInput} from './auth_utils'
```

**Workflow**:
- **Planning Phase**: Add planned core functions
- **Implementation Phase**: Kilo checks registry before creating functions, adds new ones as created
- **Validation Phase**: Review for unexpected additions (scope creep indicator)

**Why**: 
- Prevents cross-file duplication (Issue #2 cause)
- Provides import statements Kilo can copy directly
- Flags when Kilo builds beyond scope

---

#### 6. API Contract (Optional)
**Purpose**: Define API integration patterns.

**Contents**:
- Endpoint definitions
- Authentication requirements
- Request/response examples
- Error handling specifications
- Rate limiting rules

**When to include**: Only if your MVP has external APIs or internal translation layers.

---

### Tracking Documents (Updated by Kilo, Reviewed by You)

#### 7. Component Registry
**Purpose**: Track implementation status and file metrics.

**Format**:
```markdown
# Component Registry

## User Authentication Component
**Status**: VALIDATED  
**Build Order**: 2  
**Files**:
- auth_module.py (148 lines) - Core logic
- auth_utils.py (62 lines) - Helper functions

**Functions**:
- Core: validateCredentials(), login(), logout()
- Utils: hashPassword(), sanitizeInput()

**Dependencies**:
- Uses: Database Connection, Configuration Manager
- Used By: User Profile Component, Session Manager Component

**Integration Tests**: ✓ Passed (Auth → Database, Auth → Config)

---

## User Profile Component
**Status**: IN PROGRESS  
**Build Order**: 3  
**Files**:
- profile.py (estimating 180 lines)

**Functions**:
- Core: createProfile(), getProfile(), updateProfile()

**Dependencies**:
- Uses: User Authentication, Database Connection
- Used By: Settings Component
```

**Status Values**:
- **PLANNED**: Documented in Implementation Plan, not started
- **IN PROGRESS**: Kilo currently implementing
- **IMPLEMENTED**: Code complete, not yet tested
- **VALIDATED**: Human tested, functional in isolation
- **INTEGRATED**: Connected to dependencies, integration tested
- **BLOCKED**: Waiting on dependency completion

**Why**: Provides at-a-glance project status and catches monolithic files early.

---

## Critical Workflow Rules

### 1. File Length Enforcement
- **Hard limit**: 300 lines per file
- **Enforcement**: .vscode rules + Kilo system prompts
- **Detection**: Component Registry tracks line counts
- **Action**: If approaching 300 lines during planning, split into modules before implementation

**Why**: After 500 lines, Kilo's parsing degrades, causing function duplication.

---

### 2. Build Order Adherence
- **Never build a component before its dependencies**
- **Consult Implementation Plan before each prompt**
- **Kilo prompt must reference which build order it's implementing**

**Why**: Building out of order causes Kilo to hallucinate dependencies or create duplicates.

---

### 3. Function Registry Discipline
- **Include Function Registry in every Kilo prompt**
- **Instruct Kilo**: "Check Function Registry before creating new functions"
- **Review after implementation**: Any functions not pre-approved indicate scope creep

**Why**: Primary defense against cross-file duplication.

---

### 4. Manual Validation Mandatory
- **Never rely on passing unit tests**
- **Human functional testing required for every component**
- **Only mark components VALIDATED after manual verification**

**Why**: Addresses Issue #3 (Fake test success from hardcoded responses).

---

## Testing Philosophy

### No Automated Test Suites
- **Do not create comprehensive test suites during initial development**
- **Reason**: Test maintenance overhead without value in component-based solo development
- **Exception**: Kilo may generate unit tests as behavioral documentation

---

### Manual Testing Workflow
1. **Component Testing**: Test each component in isolation after implementation
2. **Integration Testing**: Test component connections at build order checkpoints
3. **Functional Testing**: Verify actual application behavior, not just test passage
4. **Document Results**: Update Component Registry with test outcomes

---

### Runtime Command Precision
- **Always specify exact commands in Kilo prompts**
- **Example**: "Run `npm run dev` to test the Electron app" (not "npm start")
- **Why**: Kilo sometimes selects wrong commands, causing false failures

---

## Failure Recovery Procedures

### Rollback Triggers
Execute immediate rollback via Kilo checkpoints if:
1. Kilo creates functions not in Function Registry (scope creep)
2. File exceeds 300 lines (monolithic structure)
3. Implementation diverges from Schema Document
4. Three iterations fail to achieve component functionality

---

### Function Duplication Resolution
1. Search Function Registry for function name
2. If duplicate found, rollback implementation
3. Update prompt to explicitly reference existing function
4. If semantic duplicate (different name, same purpose), update Naming Standards
5. Re-implement with clarified standards

---

### Integration Failure Resolution
1. Rollback to last validated component
2. Review Integration Plan for missing dependencies
3. Verify data format consistency via Schema Document
4. Test components individually before re-integration

---

## Kilo Prompt Schema

### Standard Component Implementation Prompt Structure

```markdown
# Component Implementation: [Component Name]

## Context
Building [Component Name] as part of Build Order [X].
This component [brief purpose statement].

## Dependencies
This component depends on:
- [Dependency 1] (Build Order [Y]) - Status: VALIDATED
- [Dependency 2] (Build Order [Z]) - Status: VALIDATED

## Documentation References
- Schema: [Link to specific section of Schema Document]
- Naming Standards: [Link to Naming Standards]
- Function Registry: [Embed relevant excerpt]

## Implementation Requirements

### Files to Create
- [filename.py] (~[estimated lines]) - [purpose]
- [filename_utils.py] (~[estimated lines]) - [purpose]

### Functions to Implement
Core:
- functionName(params) -> returnType - [purpose]

Utils:
- helperFunction(params) -> returnType - [purpose]

### Constraints
- Maximum 300 lines per file
- Check Function Registry before creating new functions
- Follow Naming Standards exactly
- Implement data structures per Schema Document section [X.Y]

### Testing
Run `[exact command]` to test component functionality.

## Update Requirements
After implementation:
1. Update Component Registry with actual line counts
2. Update Function Registry with any helper functions created
3. Provide code manifest for validation

## Architect Mode
Please create an implementation plan following these requirements.
```

---

## Common Failure Modes & Solutions

### Issue #1: Improper Implementation of Instructions
**Root Cause**: Kilo invents structure when not given explicit examples.

**Solution**: 
- Provide examples in Schema Document
- Reference specific schema sections in prompts
- Include "implement exactly as shown" instructions

---

### Issue #2: Building Beyond Requested Scope
**Root Cause**: Kilo fills in perceived gaps without authorization.

**Solution**:
- PRD with explicit exclusions
- Function Registry check before creation
- Review Component Registry for unexpected additions
- Rollback immediately when detected

---

### Issue #3: Fake Test Success
**Root Cause**: Unit tests with hardcoded success responses.

**Solution**:
- Mandatory human functional testing
- Never rely on "tests pass" as validation
- Skip automated test suite creation
- Focus on manual component verification

---

## Workflow Checklist

### Project Initialization
- [ ] Create PRD with scope and exclusions
- [ ] Create Implementation Plan with build order
- [ ] Create Schema Document with examples
- [ ] Create Naming Standards
- [ ] Initialize Function Registry with planned functions
- [ ] Create API Contract (if needed)
- [ ] Initialize Component Registry

### Per-Component Workflow
- [ ] Consult Implementation Plan for next component
- [ ] Verify dependencies are VALIDATED
- [ ] Create Kilo prompt with embedded documentation
- [ ] Review Kilo's architect plan with AI Assistant
- [ ] Approve and execute implementation
- [ ] Review Component Registry updates
- [ ] Review Function Registry for unexpected additions
- [ ] Manual functionality testing
- [ ] Update Component Registry to VALIDATED
- [ ] Proceed to next component or integration checkpoint

### Integration Checkpoint Workflow
- [ ] Review Implementation Plan for integration requirements
- [ ] Connect components per dependency specifications
- [ ] Manual integration testing
- [ ] Verify data flows match Schema Document
- [ ] Update Component Registry to INTEGRATED
- [ ] Document integration test results

---

## Project Archive & Reuse

After successful MVP completion:
1. Archive all planning documents as templates
2. Document lessons learned in workflow refinements
3. Save successful Kilo prompts as reusable templates
4. Export Function Registry patterns for future projects
5. Update this workflow with improvements

---

## Workflow Maintenance

This workflow is a living document. After each project:
- Add new failure modes and solutions
- Refine prompt schemas based on what worked
- Update naming standards with new patterns
- Document Kilo limitations discovered
- Share improvements across projects

---

**End of Workflow Document**
