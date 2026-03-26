# Testing Strategy

Reference for test-alongside development across implementation sprints.

## Coverage Thresholds

| Scope | Minimum |
|-------|---------|
| Overall codebase | 80% |
| New/modified code | 90% |
| Critical paths (auth, payments, API) | 95% |

## Test Pyramid

| Level | Count | Speed | Scope | Dependencies |
|-------|-------|-------|-------|--------------|
| Unit | Many | < 100ms each | Single function/class | Mocked |
| Integration | Moderate | < 5s each | 2+ real components | Real DB, real FS |
| E2E | Few | < 60s each | Full user flow | Real/staging infra |

## Test Naming Convention

```
test_<unit>_<scenario>_<expected_outcome>
```

Examples:
- `test_create_user_valid_input_returns_user_id`
- `test_create_user_duplicate_email_raises_conflict`
- `test_transfer_insufficient_funds_returns_400`

## Arrange-Act-Assert Pattern

```
# Arrange — set up preconditions
# Act    — execute the behavior under test
# Assert — verify the expected outcome
```

One logical assertion per test. Multiple `assert` statements acceptable when verifying a single behavior.

## What to Mock

| Mock | Do Not Mock |
|------|-------------|
| External HTTP APIs | Code under test |
| System clock | Data structures |
| Random/UUID generation | Pure utility functions |
| Environment variables | DB queries in integration tests |
| File system (unit tests only) | Internal module boundaries |

## Mock Boundaries

- Mock at the boundary, not deep in the call chain
- Verify mock interactions only when the interaction IS the behavior
- Prefer fakes over mocks when the fake is simpler
- Max 2 mocked dependencies per test — more indicates excessive coupling

## Test File Placement

| Convention | When |
|------------|------|
| `tests/unit/<module>_test.py` | Python projects |
| `tests/integration/<feature>_test.py` | Python integration |
| `__tests__/<module>.test.ts` | TypeScript colocated |
| `tests/<module>.test.ts` | TypeScript separate |

## CI Gate Requirements

- Zero failures, zero unannotated skips
- Coverage thresholds met
- No flaky tests (quarantine with linked issue)
- Max runtime: 10 min unit, 30 min integration
- Tests run in parallel, no order dependency
