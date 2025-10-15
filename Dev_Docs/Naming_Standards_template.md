# Naming Standards

## Project: [MVP Name]
**Last Updated:** [Date]

---

## Purpose
Consistent naming prevents semantic duplication and improves code readability.  
**Rule:** Follow these conventions exactly. No exceptions without documentation.

---

## Functions

### Validation Functions
**Pattern:** `validate{Noun}()`  
**Examples:** `validateEmail()`, `validatePassword()`, `validateInput()`  
**Never use:** "check", "verify", "is{Noun}Valid"

### Data Retrieval Functions
**Pattern:** `get{Noun}()`  
**Examples:** `getUser()`, `getConfig()`, `getData()`  
**Never use:** "fetch", "retrieve", "load", "read"

### Data Storage Functions
**Pattern:** `save{Noun}()`  
**Examples:** `saveUser()`, `saveConfig()`, `saveData()`  
**Never use:** "store", "persist", "write", "update" (unless specifically updating)

### Boolean Check Functions
**Pattern:** `is{Adjective}()`  
**Examples:** `isValid()`, `isActive()`, `isEmpty()`  
**Never use:** "check", "has" (unless checking possession)

### Action Functions
**Pattern:** `{verb}{Noun}()`  
**Examples:** `createUser()`, `deleteRecord()`, `updateStatus()`  
**Use clear, specific verbs**

---

## Constants

### Format
**ALL_CAPS_SNAKE_CASE**

### Examples
- `MAX_RETRY_COUNT`
- `API_BASE_URL`
- `DEFAULT_TIMEOUT`
- `CONFIG_FILE_PATH`

---

## Classes/Components

### Format
**PascalCase**

### Examples
- `UserAuthentication`
- `DatabaseConnection`
- `ConfigManager`
- `DataSync`

---

## Variables

### Shared Variables (cross-file scope)
**Format:** camelCase  
**Examples:** `currentUser`, `appConfig`, `activeSession`

### Local Variables (function scope)
**Format:** camelCase  
**Examples:** `userInput`, `isValid`, `retryCount`

### Private Variables (class internal)
**Format:** _camelCase (leading underscore)  
**Examples:** `_internalState`, `_cacheData`

---

## Files and Modules

### Format
**snake_case** or **kebab-case** (per framework convention)

### Examples
- `user_authentication.py`
- `database-connection.js`
- `config_manager.py`

### File Size Limit
**Maximum 300 lines** before modular refactoring required.

---

## Project-Specific Additions

### [Custom Pattern]
**Pattern:** [Your convention]  
**Examples:** [Your examples]  
**Rationale:** [Why this pattern?]

---

## Notes
[Any domain-specific naming conventions or decisions]
