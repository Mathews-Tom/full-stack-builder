# Scaffolding Patterns

Standard project scaffolding structures by ecosystem. Use as reference when initializing new projects.

## Python (FastAPI / Django)

```
project/
├── pyproject.toml
├── .env.example
├── src/
│   └── <package>/
│       ├── __init__.py
│       ├── main.py
│       ├── config.py
│       ├── models/
│       ├── routes/
│       ├── services/
│       ├── schemas/
│       └── utils/
├── tests/
│   ├── conftest.py
│   ├── unit/
│   └── integration/
├── migrations/
│   └── versions/
└── docker/
    ├── Dockerfile
    └── docker-compose.yml
```

**Config files:** `pyproject.toml` (uv/poetry), `ruff.toml`, `mypy.ini`, `.pre-commit-config.yaml`

## TypeScript (Next.js / Express)

```
project/
├── package.json
├── tsconfig.json
├── .env.example
├── src/
│   ├── app/ or routes/
│   ├── lib/
│   ├── types/
│   ├── middleware/
│   ├── services/
│   └── utils/
├── tests/
│   ├── setup.ts
│   ├── unit/
│   └── integration/
├── prisma/ or drizzle/
│   └── schema.prisma
└── docker/
    └── Dockerfile
```

**Config files:** `tsconfig.json`, `eslint.config.js`, `.prettierrc`, `vitest.config.ts`

## Go

```
project/
├── go.mod
├── cmd/
│   └── server/
│       └── main.go
├── internal/
│   ├── config/
│   ├── handler/
│   ├── model/
│   ├── repository/
│   └── service/
├── pkg/
├── migrations/
└── tests/
```

## Scaffold Checklist

| Step | Action | Verify |
|------|--------|--------|
| 1 | Initialize package manager | `build` succeeds |
| 2 | Configure linting + formatting | `lint` runs clean |
| 3 | Configure type checking | `typecheck` passes |
| 4 | Set up test framework | Empty test run passes |
| 5 | Create .env.example | All required vars documented |
| 6 | Set up database migrations | Migration framework initializes |
| 7 | Add Dockerfile | Container builds |
| 8 | Configure CI pipeline | Pipeline runs green |

## Build Order Principle

1. Shared types and interfaces
2. Configuration and environment loading
3. Database models and migrations
4. Repository/data access layer
5. Service/business logic layer
6. API routes/handlers
7. Middleware (auth, logging, error handling)
8. Integration wiring and entry point
