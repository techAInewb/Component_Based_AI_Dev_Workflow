# API Contract Document

## Project: [MVP Name]
**Last Updated:** [Date]

---

## Purpose
Define exact API specifications for external integrations or internal translation layers.

**Note:** Only include this document if your MVP has APIs or translation layers.

---

## Authentication

### Method
[API Key / OAuth / JWT / etc.]

### Implementation
```
[Show exact header format or auth flow]
```

---

## Endpoints

### [Endpoint Name]
**Method:** GET/POST/PUT/DELETE  
**Path:** `/api/v1/[resource]`  
**Authentication Required:** Yes/No

**Request Headers:**
```
Content-Type: application/json
Authorization: Bearer [token]
```

**Request Body:**
```json
{
  "parameter": "value",
  "example": "data"
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

**Error Responses:**

**400 Bad Request:**
```json
{
  "status": "error",
  "message": "Invalid parameter",
  "code": "INVALID_PARAM"
}
```

**401 Unauthorized:**
```json
{
  "status": "error",
  "message": "Authentication required",
  "code": "AUTH_REQUIRED"
}
```

**Rate Limiting:**
- [Requests per minute/hour]
- [Throttling behavior]

---

### [Another Endpoint]
[Repeat structure for each endpoint]

---

## Error Codes

| Code | Meaning | Action |
|------|---------|--------|
| `ERROR_CODE` | [Description] | [How to handle] |
| `ANOTHER_CODE` | [Description] | [How to handle] |

---

## Notes
[API version strategy, deprecation policy, etc.]
