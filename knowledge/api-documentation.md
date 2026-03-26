# API Documentation

Reference for generating and structuring API endpoint documentation.

## Endpoint Documentation Format

```markdown
### <METHOD> <path>

<One-line description>

**Auth:** Bearer token | API key | None
**Rate limit:** X req/min

#### Request

| Parameter | Location | Type | Required | Description |
|-----------|----------|------|----------|-------------|
| id | path | string (UUID) | Yes | Resource identifier |
| limit | query | integer | No | Max results (default: 20, max: 100) |

#### Request Body

\```json
{
  "field": "type — description"
}
\```

#### Response — 200 OK

\```json
{
  "id": "uuid",
  "created_at": "ISO 8601"
}
\```

#### Errors

| Status | Code | Description |
|--------|------|-------------|
| 400 | VALIDATION_ERROR | Invalid request body |
| 401 | UNAUTHORIZED | Missing or invalid token |
| 404 | NOT_FOUND | Resource does not exist |
| 409 | CONFLICT | Resource already exists |
| 429 | RATE_LIMITED | Too many requests |
```

## REST Conventions

| Action | Method | Path | Status |
|--------|--------|------|--------|
| List | GET | /resources | 200 |
| Create | POST | /resources | 201 |
| Read | GET | /resources/:id | 200 |
| Update (full) | PUT | /resources/:id | 200 |
| Update (partial) | PATCH | /resources/:id | 200 |
| Delete | DELETE | /resources/:id | 204 |

## Error Response Structure

```json
{
  "error": {
    "code": "MACHINE_READABLE_CODE",
    "message": "Human-readable description",
    "details": [
      { "field": "email", "issue": "must be a valid email address" }
    ]
  }
}
```

## Pagination

```json
{
  "data": [],
  "pagination": {
    "total": 142,
    "limit": 20,
    "offset": 0,
    "has_more": true
  }
}
```

## Documentation Checklist

| Item | Required |
|------|----------|
| All endpoints listed | Yes |
| Auth requirements per endpoint | Yes |
| Request/response examples | Yes |
| Error codes and descriptions | Yes |
| Rate limits documented | Yes |
| Pagination format shown | Yes (if applicable) |
| Query parameter constraints | Yes |
| Enum values listed | Yes (if applicable) |

## OpenAPI Spec Sections

| Section | Purpose |
|---------|---------|
| `info` | Title, version, description |
| `servers` | Base URLs per environment |
| `paths` | Endpoint definitions |
| `components/schemas` | Reusable data models |
| `components/securitySchemes` | Auth methods |
| `tags` | Endpoint grouping |
