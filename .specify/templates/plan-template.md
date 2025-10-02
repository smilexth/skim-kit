
# Implementation Plan: [FEATURE]

**Branch**: `[meaningful-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[meaningful-feature-name]/spec.md`

## User Story Validation
**Story Clarity Status**: [Fully clarified/Needs clarification/Not started]
**User Confirmation**: [User has confirmed story understanding/Waiting for confirmation]
**Acceptance Criteria**: [Complete and testable/Incomplete clarification needed]
**Scope Boundaries**: [Clearly defined/Ambiguous - needs clarification]

## Execution Flow (/plan command scope)
```
1. Load feature spec from Input path
   → If not found: ERROR "No feature spec at {path}"
2. Fill Technical Context (scan for NEEDS CLARIFICATION)
   → Detect Project Type from file system structure or context (web=frontend+backend, mobile=app+api)
   → Set Structure Decision based on project type
3. Fill the Constitution Check section based on the content of the constitution document.
4. Evaluate Constitution Check section below
   → If violations exist: Document in Complexity Tracking
   → If no justification possible: ERROR "Simplify approach first"
   → Update Progress Tracking: Initial Constitution Check
5. Execute Phase 0 → research.md
   → If NEEDS CLARIFICATION remain: ERROR "Resolve unknowns"
6. Execute Phase 1 → contracts, data-model.md, quickstart.md, agent-specific template file (e.g., `CLAUDE.md` for Claude Code, `.github/copilot-instructions.md` for GitHub Copilot, `GEMINI.md` for Gemini CLI, `QWEN.md` for Qwen Code or `AGENTS.md` for opencode).
7. Re-evaluate Constitution Check section
   → If new violations: Refactor design, return to Phase 1
   → Update Progress Tracking: Post-Design Constitution Check
8. Plan Phase 2 → Describe task generation approach (DO NOT create tasks.md)
9. STOP - Ready for /tasks command
```

**IMPORTANT**: The /plan command STOPS at step 7. Phases 2-4 are executed by other commands:
- Phase 2: /tasks command creates tasks.md
- Phase 3-4: Implementation execution (manual or via tools)

## Summary
[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context
**Language/Version**: [e.g., Python 3.11, Swift 5.9, Rust 1.75 or NEEDS CLARIFICATION]  
**Primary Dependencies**: [e.g., FastAPI, UIKit, LLVM or NEEDS CLARIFICATION]  
**Storage**: [if applicable, e.g., PostgreSQL, CoreData, files or N/A]  
**Testing**: [e.g., pytest, XCTest, cargo test or NEEDS CLARIFICATION]  
**Target Platform**: [e.g., Linux server, iOS 15+, WASM or NEEDS CLARIFICATION]
**Project Type**: [single/web/mobile - determines source structure]  
**Performance Goals**: [domain-specific, e.g., 1000 req/s, 10k lines/sec, 60 fps or NEEDS CLARIFICATION]  
**Constraints**: [domain-specific, e.g., <200ms p95, <100MB memory, offline-capable or NEEDS CLARIFICATION]  
**Scale/Scope**: [domain-specific, e.g., 10k users, 1M LOC, 50 screens or NEEDS CLARIFICATION]

## Infrastructure Requirements
**Infrastructure Needs**: [None/Basic/Advanced - indicates if infrastructure planning required]
**Deployment Target**: [AWS/Azure/GCP/On-premise/Hybrid or NEEDS CLARIFICATION]
**Infrastructure Scale**: [Single app/Microservices/Distributed or NEEDS CLARIFICATION]
**Management Approach**: [Managed/Self-hosted/Container orchestration or NEEDS CLARIFICATION]
**Automation Level**: [Manual/Partial automation/Full GitOps or NEEDS CLARIFICATION]
**Compliance Requirements**: [None/Security standards/Data residency/Audit or NEEDS CLARIFICATION]
**DevOps Maturity**: [Basic/Intermediate/Advanced - determines pipeline complexity]
**Monitoring Needs**: [Basic health/Application performance/Business metrics or NEEDS CLARIFICATION]

## Code Quality & Security Scanning Requirements
**Code Scanning Needs**: [None/Basic quality analysis/Comprehensive quality + security scanning]
**Quality Analysis**: [Bug detection/Code smells/Technical debt measurement/Coding standards enforcement]
**Security Scanning**: [OWASP Top 10/CWE compliance/Hardcoded secrets detection/Dependency vulnerability analysis]
**Coverage Requirements**: [Line/Branch coverage tracking/Mutation testing/Duplication analysis]
**Quality Gates**: [Bug severity thresholds/Vulnerability thresholds/Maintainability ratings]
**Scanning Integration**: [PR analysis/Main branch analysis/Incremental analysis/Baseline establishment]

## Multi-Agent Worktree Requirements
**Multi-Agent Scenario**: [Single agent/Multiple agents required/Worker agents needed]
**Worktree Strategy**: [No worktrees needed/Dedicated worktrees per agent/Shared worktrees]
**Agent Coordination**: [Sequential execution/Parallel execution/Coordinated parallel]
**Worktree Isolation**: [Complete isolation required/Partial sharing allowed/Shared workspace]

## Constitution Check
*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

### Core Principles Compliance
- [ ] Simplicity First: Simplest solution implemented, complexity justified by need
- [ ] Safety by Default: No force flags, reversible operations, explicit confirmations
- [ ] Incremental Development: Work broken into <1 hour increments, independently deployable
- [ ] Orchestrator-Worker Pattern: Clear separation of planning vs execution responsibilities
- [ ] Explicit Over Implicit: Absolute file paths, explicit output locations, auditable config
- [ ] Meaningful Naming Convention: Descriptive names for specs, no numeric prefixes or generic identifiers
- [ ] GitHub CLI Repository Creation: Use gh repo create for repository operations
- [ ] Code Review Standards: Systematic code review with assignment matrix and SLA requirements
- [ ] CI/CD Pipeline Standards: Mandatory quality gates and deployment procedures
- [ ] Error Handling & Logging: Structured logging with correlation IDs and proper error handling

### User Story Clarification Compliance
- [ ] Story Understanding: User story is clearly understood in its entirety
- [ ] Objective Clarity: Business objective and user value proposition are unambiguous
- [ ] Scope Definition: Boundaries of included/excluded features are explicitly defined
- [ ] Acceptance Criteria: Clear, measurable, and testable acceptance criteria established
- [ ] Context Understanding: Business context, user personas, and usage scenarios understood
- [ ] Constraint Identification: Technical and business constraints are identified
- [ ] User Confirmation: User has explicitly confirmed story understanding
- [ ] Planning Gate Enforcement: All ambiguities resolved before proceeding to planning

### Git Worktree & Multi-Agent Compliance
- [ ] Multi-Agent Scenario Assessment: Need for multiple agents properly evaluated and documented
- [ ] Worktree Creation Standards: Worktree naming conventions and isolation requirements followed
- [ ] Worktree Management Standards: Proper branch management and synchronization procedures
- [ ] Multi-Agent Coordination: Conflict prevention and communication protocols established
- [ ] Worktree Safety Standards: Path validation, permission management, and backup procedures
- [ ] Agent Lifecycle Management: Proper initialization, monitoring, and cleanup procedures
- [ ] Performance Optimization: Resource allocation and parallel operation optimization

### Infrastructure & DevOps Compliance
- [ ] Infrastructure Development Standards: User clarification completed, infrastructure choices documented
- [ ] Infrastructure Clarification Requirements: Deployment target, scale, management approach defined
- [ ] IaC Standards: Tool selection justified, modular design, state management planned (if applicable)
- [ ] DevOps Pipeline Standards: User clarification completed, pipeline complexity matches requirements
- [ ] DevOps Clarification Process: Deployment frequency, environment strategy, quality gates defined
- [ ] Monitoring & Observability: Scope requirements, alerting strategy, retention period clarified

### Code Quality & Security Scanning Compliance
- [ ] Code Quality Analysis Standards: Bug detection, code smells, technical debt measurement implemented
- [ ] Security Scanning Requirements: OWASP Top 10 coverage, CWE compliance, secrets detection enabled
- [ ] Code Scanning Integration: CI/CD pipeline integration, quality gate enforcement, incremental analysis
- [ ] Quality Gate Standards: Bug severity thresholds, vulnerability thresholds, coverage requirements defined
- [ ] Reporting Standards: Dashboard integration, trend analysis, PR comments, notifications configured

### Development Workflow Compliance
- [ ] Task Management: TodoWrite used for tracking, single task focus, immediate completion
- [ ] Code Change Process: Context understood, patterns preserved, changes tested before commit
- [ ] Communication Standards: File-based outputs, structured formats, clear naming conventions
- [ ] Safety Guidelines: Interactive confirmations, no force operations, pre-execution validation
- [ ] Resource Management: Concurrent workers limited to 5-10, performance monitored
- [ ] Branch Management: Branch lifecycle rules, merge strategies, hotfix procedures
- [ ] Release Management: Release planning, versioning, validation, rollback procedures
- [ ] Communication & Collaboration: Meeting standards, knowledge sharing, incident response
- [ ] Documentation Standards: API docs, code comments, architecture documentation
- [ ] Tooling & Development Environment: IDE standards, setup procedures, debugging

### Workflows & Planning Compliance
- [ ] Testing Discipline: Manual testing checklist completed before pushing changes
- [ ] GitHub Workflow: Issue creation process followed with structured format
- [ ] Branch Management: Feature branches created from main, proper naming conventions
- [ ] Commit Standards: Structured commit messages with What/Why/Impact sections
- [ ] Pull Request Process: No self-merging, proper review流程 followed
- [ ] Planning Structure: Planning issues include Overview, Current State, Proposed Solution, Acceptance Criteria

### Operational Safety Compliance
- [ ] Repository Usage: Correct repository targeting, no upstream operations without permission
- [ ] Command Safety: No force flags (-f, --force) used, safe command options only
- [ ] Git Operations: No force push/checkout/clean, history preservation maintained
- [ ] Pull Request Safety: No self-merging, explicit user permission required
- [ ] File Operations: Interactive deletion (rm -i), reversible operations, backups maintained
- [ ] Package Management: No force installation, controlled updates, lockfile reviews

### Development Methodology Compliance
- [ ] Test-Driven Development: TDD methodology with Red-Green-Refactor cycle followed
- [ ] Spec-Driven Development: Specifications created as executable artifacts guiding development
- [ ] Research-Driven Implementation: Web research conducted before all technology decisions
- [ ] Open Source First: OSS solutions prioritized over commercial alternatives

### Methodology Compliance
- [ ] Spec-Driven Development: Specifications guide all development
- [ ] Template Consistency: All templates maintain consistent structure
- [ ] Documentation Standards: Comprehensive documentation for all components
- [ ] Research-Driven Implementation: Research precedes all decisions
- [ ] Open Source First: OSS solutions prioritized

### Security & Compliance
- [ ] Dependency Management: No critical vulnerabilities, automated vulnerability scanning
- [ ] Data Handling: PII protection, secure config management, data minimization principles
- [ ] AI Agent Security: Auditability, no credential exposure, secure AI interactions
- [ ] System Configuration: Asia/Bangkok timezone standard
- [ ] Security Review Process: Security checklist completed for all changes
- [ ] Secrets Management: Encrypted storage, regular rotation, audit logging
- [ ] Security Testing: SAST/DAST scanning, penetration testing, vulnerability assessment
- [ ] License Compliance: Open source license scanning and approval process
- [ ] Data Privacy: GDPR/CCPA compliance, privacy impact assessments
- [ ] Accessibility: Documentation accessibility for all users

### Quality Assurance
- [ ] Testing Mandate: TDD with appropriate coverage for project type
- [ ] Definition of Done: All constitutional requirements met
- [ ] Static Analysis: Code quality and validation gates
- [ ] Code Quality Metrics: Coverage thresholds, complexity limits, technical debt tracking
- [ ] Documentation Standards: Complete documentation coverage
- [ ] Template Validation: All templates pass structural validation

### Technology Selection Compliance
- [ ] OSS-First Evaluation: All commercial alternatives documented
- [ ] License Compatibility: OSS with permissive licenses verified
- [ ] Community Viability: OSS project health and support assessed
- [ ] Commercial Justification: Business requirements documented if commercial selected
- [ ] Prohibited Technologies: No prohibited commercial software included

### Documentation & Visualization Compliance
- [ ] Mermaid Diagrams: Workflow and architecture diagrams included when requested
- [ ] Table Standards: Structured data presented in Markdown tables
- [ ] Chart Requirements: Performance and quality metrics visualized
- [ ] User-Requested Visualizations: Diagrams provided when explicitly asked
- [ ] Accessibility: All visualizations include descriptive explanations

### Directory Structure Compliance
- [ ] Documentation-Only Areas: specs/, docs/, prompts/ contain only explanatory content
- [ ] Artifact-Only Areas: artifacts/, deploy/, build/ contain only deployment materials
- [ ] Source Code Separation: src/, tests/, lib/ contain only code-related files
- [ ] No Mixed Content: Directories have single, clear purpose with no mixed types
- [ ] Gitignore Configuration: Artifact directories properly gitignored

### Development Environment Compliance
- [ ] Platform Priority: macOS and Linux as primary platforms verified
- [ ] Windows Support: WSL2 configuration for Windows development verified
- [ ] Cross-Platform Tools: Scripts use cross-platform commands validated
- [ ] Containerization: Docker configuration consistent across platforms
- [ ] Documentation: Platform-specific setup guides provided
- [ ] Shell Configuration: Fish shell for macOS, bash for Linux/Windows specified
- [ ] Script Compatibility: All project scripts use bash syntax for compatibility

### Demonstration & Script Compliance
- [ ] User-Requested Scripts: Shell scripts provided when users request testing/demos/simulations
- [ ] Script Organization: scripts/, scripts/test/, scripts/demo/, scripts/simulate/ directories planned
- [ ] Platform Support: Scripts compatible with macOS (fish), Linux (bash), Windows (WSL2 bash)
- [ ] Script Standards: Proper permissions, error handling, documentation included
- [ ] Self-Contained Scripts: Dependencies and setup instructions clearly documented

### Template & Scripting Compliance
- [ ] Template Structure: All templates follow consistent structure
- [ ] Script Organization: Scripts organized in appropriate directories
- [ ] Platform Support: Scripts compatible across target platforms
- [ ] Documentation: All scripts include proper documentation
- [ ] Error Handling: Comprehensive error handling in all scripts

### Research & Due Diligence Compliance
- [ ] Current Information: Web research conducted for latest technology updates
- [ ] Security Review: Security advisories and vulnerabilities checked and documented
- [ ] Alternative Analysis: Alternative solutions researched and evaluated
- [ ] Best Practices: Current best practices identified and documented
- [ ] Research Documentation: All research findings documented with sources and dates

## Project Structure

### Documentation (this feature)
```
specs/[meaningful-feature]/
├── plan.md              # This file (/plan command output)
├── research.md          # Phase 0 output (/plan command)
├── data-model.md        # Phase 1 output (/plan command)
├── quickstart.md        # Phase 1 output (/plan command)
├── contracts/           # Phase 1 output (/plan command)
└── tasks.md             # Phase 2 output (/tasks command - NOT created by /plan)
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. Delete unused options and expand the chosen structure with
  real paths (e.g., apps/admin, packages/something). The delivered plan must
  not include Option labels.
-->
```
# [REMOVE IF UNUSED] Option 1: Single project (DEFAULT)
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [REMOVE IF UNUSED] Option 2: Tool/Utility (when command-line tool detected)
bin/
├── [executable-name]
└── scripts/

lib/
├── core/
├── utils/
└── templates/

# [REMOVE IF UNUSED] Option 3: Multi-module project (when multiple components detected)
packages/
├── [module-1]/
├── [module-2]/
└── shared/
```

**Structure Decision**: [Document the selected structure and reference the real
directories captured above]

## Phase 0: Outline & Research
1. **Extract unknowns from Technical Context** above:
   - For each NEEDS CLARIFICATION → research task
   - For each dependency → best practices task
   - For each integration → patterns task

2. **Generate and dispatch research agents**:
   ```
   For each unknown in Technical Context:
     Task: "Research {unknown} for {feature context}"
   For each technology choice:
     Task: "Find best practices for {tech} in {domain}"
   ```

3. **Consolidate findings** in `research.md` using format:
   - Decision: [what was chosen]
   - Rationale: [why chosen]
   - Alternatives considered: [what else evaluated]

**Output**: research.md with all NEEDS CLARIFICATION resolved

## Phase 1: Design & Contracts
*Prerequisites: research.md complete*

1. **Extract entities from feature spec** → `data-model.md`:
   - Entity name, fields, relationships
   - Validation rules from requirements
   - State transitions if applicable

2. **Generate API contracts** from functional requirements:
   - For each user action → endpoint
   - Use standard REST/GraphQL patterns
   - Output OpenAPI/GraphQL schema to `/contracts/`

3. **Generate contract tests** from contracts:
   - One test file per endpoint
   - Assert request/response schemas
   - Tests must fail (no implementation yet)

4. **Extract test scenarios** from user stories:
   - Each story → integration test scenario
   - Quickstart test = story validation steps

5. **Update agent file incrementally** (O(1) operation):
   - Run `.specify/scripts/bash/update-agent-context.sh claude`
     **IMPORTANT**: Execute it exactly as specified above. Do not add or remove any arguments.
   - If exists: Add only NEW tech from current plan
   - Preserve manual additions between markers
   - Update recent changes (keep last 3)
   - Keep under 150 lines for token efficiency
   - Output to repository root

**Output**: data-model.md, /contracts/*, failing tests, quickstart.md, agent-specific file

## Phase 2: Task Planning Approach
*This section describes what the /tasks command will do - DO NOT execute during /plan*

**Task Generation Strategy**:
- Load `.specify/templates/tasks-template.md` as base
- Generate tasks from Phase 1 design docs (contracts, data model, quickstart)
- Each contract → contract test task [P]
- Each entity → model creation task [P] 
- Each user story → integration test task
- Implementation tasks to make tests pass

**Ordering Strategy**:
- TDD order: Tests before implementation 
- Dependency order: Models before services before UI
- Mark [P] for parallel execution (independent files)

**Estimated Output**: 25-30 numbered, ordered tasks in tasks.md

**IMPORTANT**: This phase is executed by the /tasks command, NOT by /plan

## Phase 3+: Future Implementation
*These phases are beyond the scope of the /plan command*

**Phase 3**: Task execution (/tasks command creates tasks.md)  
**Phase 4**: Implementation (execute tasks.md following constitutional principles)  
**Phase 5**: Validation (run tests, execute quickstart.md, performance validation)

## Complexity Tracking
*Fill ONLY if Constitution Check has violations that must be justified*

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |


## Progress Tracking
*This checklist is updated during execution flow*

**Phase Status**:
- [ ] Phase 0: Research complete (/plan command)
- [ ] Phase 1: Design complete (/plan command)
- [ ] Phase 2: Task planning complete (/plan command - describe approach only)
- [ ] Phase 3: Tasks generated (/tasks command)
- [ ] Phase 4: Implementation complete
- [ ] Phase 5: Validation passed

**Gate Status**:
- [ ] Initial Constitution Check: PASS
- [ ] Post-Design Constitution Check: PASS
- [ ] All NEEDS CLARIFICATION resolved
- [ ] Complexity deviations documented

---
*Based on Constitution v3.0.0 - See `/memory/constitution.md`*
