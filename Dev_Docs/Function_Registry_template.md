# Function Registry

## Project: [MVP Name]
**Last Updated:** [Date]

---

## Purpose
Track all functions with their file location and import statement to prevent duplication.

**Format:** `functionName(params) -> returnType | filepath | import statement`

---

## Registry

### Foundation Functions (Build Order 1)

```
connectDB() -> Connection | database.py | import {connectDB} from './database'
closeDB(connection) -> void | database.py | import {closeDB} from './database'
loadConfig(path) -> Config | config.py | import {loadConfig} from './config'
```

### [Component Name] Functions (Build Order 2)

```
[Add functions here as they are planned or implemented]
```

### [Component Name] Functions (Build Order 3)

```
[Add functions here as they are planned or implemented]
```

---

## Usage Instructions

### During Planning
Add expected core functions for each component

### During Implementation
Kilo checks this registry before creating new functions and adds any helpers created

### During Validation
Review for unexpected additions (indicates scope creep)

---

## Notes
[Function deprecations, renames, or special considerations]
