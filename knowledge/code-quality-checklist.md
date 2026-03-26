# Code Quality Checklist

Pre-delivery quality gates applied during Phase 4 and Phase 6 of the build process.

## Error Handling

| Check | Pass Criteria |
|-------|---------------|
| External API calls | Wrapped with timeout, retry, and error handling |
| Database operations | Connection errors caught, transactions rolled back on failure |
| File I/O | Handles missing files, permission errors, disk full |
| User input | Validated at boundary, rejected with descriptive error |
| Async operations | Unhandled promise rejections caught |
| Third-party SDKs | Errors caught and translated to domain errors |

## Input Validation

| Layer | Validation |
|-------|-----------|
| HTTP boundary | Type, length, format, range |
| Service layer | Business rule validation |
| Database layer | Constraints, foreign keys |

Rules:
- Allowlists over denylists
- Reject immediately with descriptive error
- Validate numeric ranges explicitly
- Reject NaN and Infinity for floats

## Security Checklist (OWASP Top 10)

| Category | Check |
|----------|-------|
| Injection | Parameterized queries, no string concatenation |
| Broken Auth | Token expiry, secure session handling |
| Sensitive Data | Encryption at rest and in transit |
| XXE | Disable external entity processing |
| Broken Access | RBAC/ABAC enforced at every endpoint |
| Misconfiguration | No debug mode in production, no default credentials |
| XSS | Output encoding, CSP headers |
| Deserialization | Input validation before deserialization |
| Components | No known CVEs in dependencies |
| Logging | No secrets in logs, structured logging format |

## Code Structure

| Check | Pass Criteria |
|-------|---------------|
| DRY | No logic duplicated across 2+ locations |
| Single responsibility | Each function does one thing |
| Naming | Functions describe action, variables describe content |
| Complexity | Cyclomatic complexity < 10 per function |
| File length | < 300 lines per file |
| Function length | < 50 lines per function |
| Import order | Stdlib, third-party, local — separated |
| Dead code | No unused imports, functions, or variables |

## Configuration

| Check | Pass Criteria |
|-------|---------------|
| No hardcoded secrets | All secrets via environment variables |
| No hardcoded URLs | Base URLs in config |
| .env.example exists | All required vars documented |
| Config validation | App fails fast on missing required config |
| Environment separation | Dev/staging/prod configs isolated |

## Pre-Delivery Gates

1. All tests pass (zero failures)
2. Coverage thresholds met
3. Linting clean (zero errors)
4. Type checking passes
5. No TODO/FIXME/HACK in delivered code
6. Security scan clean
7. API documentation generated
8. README with setup instructions
