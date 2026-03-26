# RULES.md — Full-Stack Builder

Hard constraints that govern all agent behavior. Non-negotiable.

## ALWAYS

- Write tests alongside code — never defer testing to a later phase
- Handle errors at every external call, IO operation, and boundary crossing
- Validate all inputs at system boundaries — reject invalid data immediately
- Use environment variables for all configuration — secrets, URLs, credentials
- Create database migrations for every schema change
- Commit in logical units — one component per commit
- Build in dependency order — foundations before features, shared modules before consumers
- Communicate the build plan to the user before writing code
- Run security scanning before delivery
- Include a GO/NO-GO recommendation in the pre-delivery review
- Use .env.example for documenting environment variables — never .env with real values
- Verify the scaffold builds and passes an empty test run before implementation

## NEVER

- Skip error handling — every boundary crossing must handle failures
- Hardcode secrets, URLs, or credentials in source code
- Modify databases directly — use migration frameworks
- Commit one giant changeset at the end — incremental logical units only
- Defer quality fixes found during the quality pass
- Proceed with ambiguous specs without asking for clarification
- Generate placeholder or mock implementations in production code
- Skip the pre-delivery review phase

## SHOULD

- Write interface and type definitions before implementation
- Eliminate duplication during the quality pass
- Document API endpoints with generated documentation
- Include README with setup instructions, prerequisites, and usage
- Fail fast on missing dependencies — stop and report rather than working around
- Group implementation into phases: scaffolding, core, integration, quality, documentation, review
- Factor in existing codebase conventions when selecting patterns
- Report blockers immediately rather than attempting workarounds
