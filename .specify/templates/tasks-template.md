# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[meaningful-feature-name]/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found at /specs/[meaningful-feature-name]/plan.md"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Single project**: `src/`, `tests/` at repository root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume single project - adjust based on plan.md structure

## Phase 3.1: Setup
- [ ] T001 Create project structure per implementation plan
- [ ] T002 Initialize [language] project with [framework] dependencies
- [ ] T003 [P] Configure linting and formatting tools

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**

### Unit Tests (Red Phase)
- [ ] T004 [P] Unit test User model validation in tests/unit/test_user_model.py
- [ ] T005 [P] Unit test UserService business logic in tests/unit/test_user_service.py
- [ ] T006 [P] Unit test CLI commands in tests/unit/test_cli_commands.py
- [ ] T007 [P] Unit test input validation in tests/unit/test_validation.py

### Integration Tests (Red Phase)
- [ ] T008 [P] Contract test POST /api/users in tests/contract/test_users_post.py
- [ ] T009 [P] Contract test GET /api/users/{id} in tests/contract/test_users_get.py
- [ ] T010 [P] Integration test user registration in tests/integration/test_registration.py
- [ ] T011 [P] Integration test auth flow in tests/integration/test_auth.py

### Performance Tests (Red Phase)
- [ ] T012 [P] Load test user creation endpoint in tests/performance/test_user_creation_load.py
- [ ] T013 [P] Response time validation for API endpoints in tests/performance/test_response_times.py

## Phase 3.3: Core Implementation (Green Phase - ONLY after tests are failing)
- [ ] T014 [P] User model in src/models/user.py
- [ ] T015 [P] UserService CRUD in src/services/user_service.py
- [ ] T016 [P] CLI --create-user in src/cli/user_commands.py
- [ ] T017 POST /api/users endpoint
- [ ] T018 GET /api/users/{id} endpoint
- [ ] T019 Input validation
- [ ] T020 Error handling and logging

## Phase 3.4: Integration (Green Phase)
- [ ] T021 Connect UserService to DB
- [ ] T022 Auth middleware
- [ ] T023 Request/response logging
- [ ] T024 CORS and security headers

## Phase 3.5: Refinement & Testing (Refactor Phase)
- [ ] T025 [P] Refactor code to improve testability and maintainability
- [ ] T026 [P] Optimize test performance and execution time
- [ ] T027 [P] Add edge case coverage based on implementation discoveries
- [ ] T028 [P] Update test documentation and fixtures

## Phase 3.6: Polish & Documentation
- [ ] T029 [P] Update docs/api.md with latest implementation details
- [ ] T030 [P] Remove code duplication identified during testing

## Phase 3.7: Code Quality & Performance
- [ ] T031 [P] Run code complexity analysis and refactor if complexity > 10
- [ ] T032 [P] Ensure code coverage meets requirements: 90% line, 85% branch coverage
- [ ] T033 [P] Performance testing: validate response times < 200ms (95th percentile)
- [ ] T034 [P] Technical debt assessment and documentation

## Phase 3.8: Security & Compliance
- [ ] T035 [P] Run security vulnerability scanning and address findings
- [ ] T036 [P] Validate secrets management and encryption implementation
- [ ] T037 [P] License compliance check for all dependencies
- [ ] T038 [P] Accessibility compliance validation (WCAG 2.1 AA)

## Phase 3.9: Integration & E2E Testing
- [ ] T039 [P] End-to-end testing for critical user journeys
- [ ] T040 [P] Cross-browser and cross-device testing validation
- [ ] T041 [P] Integration testing with external services
- [ ] T042 [P] Load testing with 2x expected peak load

## Phase 3.10: Documentation & Release Preparation
- [ ] T043 [P] Complete API documentation with OpenAPI specification
- [ ] T044 [P] Update architecture documentation and diagrams
- [ ] T045 [P] Prepare release notes and changelog
- [ ] T046 [P] Final validation and rollback procedure testing

## Phase 3.11: Final Validation
- [ ] T047 Run manual-testing.md validation scenarios
- [ ] T048 Final test suite validation and coverage verification

## Dependencies
- Tests (T004-T013) before implementation (T014-T020)
- T014 blocks T015, T021
- T022 blocks T024
- Implementation before refinement (T025-T028)
- Refinement before polish (T029-T032)

## Parallel Example
```
# Launch all tests together (T004-T013):
Task: "Unit test User model validation in tests/unit/test_user_model.py"
Task: "Unit test UserService business logic in tests/unit/test_user_service.py"
Task: "Unit test CLI commands in tests/unit/test_cli_commands.py"
Task: "Unit test input validation in tests/unit/test_validation.py"
Task: "Contract test POST /api/users in tests/contract/test_users_post.py"
Task: "Contract test GET /api/users/{id} in tests/contract/test_users_get.py"
Task: "Integration test registration in tests/integration/test_registration.py"
Task: "Integration test auth in tests/integration/test_auth.py"
Task: "Load test user creation endpoint in tests/performance/test_user_creation_load.py"
Task: "Response time validation in tests/performance/test_response_times.py"
```

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Commit after each task
- Avoid: vague tasks, same file conflicts

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - Each contract file → contract test task [P]
   - Each endpoint → implementation task
   
2. **From Data Model**:
   - Each entity → model creation task [P]
   - Relationships → service layer tasks
   
3. **From User Stories**:
   - Each story → integration test [P]
   - Quickstart scenarios → validation tasks

4. **Ordering**:
   - Setup → Tests → Models → Services → Endpoints → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [ ] All contracts have corresponding tests
- [ ] All entities have model tasks
- [ ] All tests come before implementation
- [ ] Parallel tasks truly independent
- [ ] Each task specifies exact file path
- [ ] No task modifies same file as another [P] task