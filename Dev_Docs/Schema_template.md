# Schema Document

## Project: [MVP Name]
**Last Updated:** [Date]

---

## Purpose
This document provides explicit examples of all data structures used in this project.  
**Rule:** Show examples, don't just describe.

---

## Database Schemas

### [Table/Collection Name]
```json
{
  "fieldName": "data type (e.g., string, UUID, ISO timestamp)",
  "exampleField": "example value",
  "nestedObject": {
    "subField": "value"
  }
}
```

**Validation Rules:**
- [fieldName]: [validation rule]
- [exampleField]: [validation rule]

---

## API Request/Response Formats

### [Endpoint Name]
**Request:**
```json
{
  "parameter": "value",
  "exampleParam": "example"
}
```

**Success Response (200):**
```json
{
  "status": "success",
  "data": {
    "field": "value"
  }
}
```

**Error Response (4xx/5xx):**
```json
{
  "status": "error",
  "message": "Descriptive error message",
  "code": "ERROR_CODE"
}
```

---

## Configuration File Formats

### [Config File Name]
```json
{
  "setting": "value",
  "exampleSetting": "example"
}
```

**Required Fields:**
- [setting]: [purpose and valid values]

---

## Data Validation Rules

### [Data Type Name]
**Format:** [How should it look?]  
**Example:** `[concrete example]`  
**Validation:** [regex, range, enum, etc.]

---

## Component Data Contracts

### [Component Name] Input
```
Expected input format with examples
```

### [Component Name] Output
```
Expected output format with examples
```

---

## Notes
[Any special considerations, edge cases, or format decisions]
