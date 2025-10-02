<!--
Sync Impact Report:
Version change: 2.3.1 → 2.4.0 (minor version)
Modified principles: N/A
Added sections: Principle VI - Meaningful Naming Convention
Removed sections: N/A
Templates requiring updates: ✅ plan-template.md (updated with naming convention compliance), ✅ tasks-template.md (updated with naming convention compliance), ✅ spec-template.md (updated with naming convention compliance), ⚠ command templates (needs updating for naming convention compliance)
Follow-up TODOs: Update all templates to enforce meaningful naming conventions in git worktrees and branches
-->

# Skim-Kit Constitution

## Core Principles

### I. Simplicity First
Start with the simplest possible solution that works. Complexity must be justified by demonstrable need. All features begin as minimal implementations, then iterate based on actual usage patterns. YAGNI (You Aren't Gonna Need It) is the default position - prove necessity before adding complexity.

### II. Safety by Default
NEVER use force flags (-f, --force) in any commands or operations. All operations must be reversible or have explicit confirmation steps. Prefer interactive confirmation over automatic execution for destructive operations. Use safe defaults: read-only first, explicit write permissions, verbose logging.

### III. Incremental Development
Break all work into small, testable increments that can be completed in under 1 hour. Each increment must be independently valuable and deployable. Complex features are delivered through multiple small phases, not monolithic implementations.

### IV. Orchestrator-Worker Pattern
Claude acts as orchestrator: planning, coordination, GitHub operations, monitoring. Codex workers handle execution: file operations, code changes, analysis tasks. Clear separation of concerns with file-based communication between components. Parallel execution preferred when tasks are independent.

### V. Explicit Over Implicit
All file paths must be absolute, not relative. All output locations must be specified explicitly. Configuration and parameters must be visible and auditable. No hidden side effects or magical behaviors.

### VI. Meaningful Naming Convention
All specifications in git worktrees or branches MUST use meaningful, descriptive names that clearly communicate the feature purpose. NEVER use numeric prefixes (e.g., 001-, 002-) or generic identifiers. Names must be human-readable and instantly understandable. Examples: `user-authentication-system` instead of `001-read-this-n8n`.

## Architecture & Technology Mandates

### Technology Stack
- **Framework**: Spec-Kit methodology implementation
- **Languages**: TypeScript for tooling, Markdown for documentation
- **Templates**: Structured Markdown templates in .specify/templates/
- **Version Control**: Git with conventional commits (MUST use git for all Git operations)
- **GitHub CLI**: GitHub CLI (gh) for GitHub operations (MUST use gh for all GitHub API operations)
- **AI Integration**: Multi-agent support (Claude, Copilot, Gemini, etc.)
- **Developer Environment**: macOS and Linux as primary platforms, Windows as alternative

### Development Methodology Requirements
- **Test-Driven Development**: All new functionality MUST follow TDD methodology with Red-Green-Refactor cycle
- **Spec-Driven Development**: Specifications are living, executable artifacts that guide development
- **Research-Driven Implementation**: All decisions MUST be preceded by comprehensive web research
- **Open Source First**: Technology selections MUST prioritize OSS solutions over commercial alternatives

### Quality & Safety Standards
- **Code Quality**: Code quality, consistency, and maintainability take precedence over rapid prototyping
- **Safety by Default**: NEVER use force flags, prefer reversible operations and explicit confirmations
- **Incremental Delivery**: Work must be broken into small increments completable in under 1 hour
- **Explicit Configuration**: All file paths absolute, all outputs specified explicitly

### Architectural Pattern
The system MUST follow the Spec-Kit workflow architecture:
- Phase 1: Specification (/specify command)
- Phase 2: Technical Planning (/plan command)
- Phase 3: Task Generation (/tasks command)
- Phase 4: Implementation (/implement command)
- Phase 5: Analysis (/analyze command)

### Template Consistency
All templates MUST maintain consistent structure and naming conventions. Changes to templates must propagate across all dependent artifacts. Cross-template references must be kept in sync.

### Technology Selection Guidelines
All technology choices MUST follow OSS-First principles with documented justification:

#### Open Source Preference
- **Default Choice**: OSS solutions MUST be the default choice for all technology needs
- **Community Support**: Prioritize OSS with active communities, regular updates, and proven adoption
- **License Compatibility**: All OSS MUST have permissive licenses (MIT, Apache 2.0, BSD, GPL compatible)
- **Long-term Viability**: Evaluate OSS project health, maintenance history, and corporate backing

#### Commercial Software Evaluation Process
Commercial solutions MAY be considered ONLY when all OSS alternatives have been evaluated and found insufficient:
1. **Requirement Analysis**: Document specific business requirements that cannot be met by OSS
2. **Market Research**: Identify and evaluate all available OSS alternatives
3. **Gap Analysis**: Document functionality gaps between OSS and commercial options
4. **Cost-Benefit Analysis**: Include licensing, maintenance, support, and opportunity costs
5. **Vendor Assessment**: Evaluate commercial vendor stability, support quality, and lock-in risks
6. **Approval Process**: Commercial selections require documented justification and maintainer approval

#### Preferred OSS Categories
- **Databases**: PostgreSQL, MongoDB, Redis, SQLite (OSS-native)
- **Messaging**: RabbitMQ, Apache Kafka, NATS (OSS-native)
- **Monitoring**: Prometheus, Grafana, Jaeger (OSS-native)
- **Containerization**: Docker, Kubernetes, Podman (OSS-native)
- **CI/CD**: Jenkins, GitLab CI, GitHub Actions (OSS-friendly)
- **Development Tools**: VS Code, Git, Docker Desktop (OSS-friendly)

#### Prohibited Commercial Technologies
- **Proprietary Databases**: Oracle Database, SQL Server (unless mandated by client)
- **Enterprise Software**: SAP, Salesforce (unless client requirement)
- **Development Tools**: Commercial IDEs without OSS alternatives
- **Cloud Lock-in Services**: AWS/Azure/GCP proprietary services when OSS alternatives exist

### Directory Structure Standards
All project directories MUST follow strict separation of concerns between documentation and artifacts:

#### Documentation-Only Directories
- **specs/**: Feature specifications, plans, and analysis documents ONLY
- **docs/**: General documentation, guides, and explanatory content ONLY
- **prompts/**: AI agent prompts and instructions ONLY
- **.specify/**: Spec-Kit configuration and templates ONLY
- **README.md**: Project overview and setup instructions ONLY
- **research/**: Research findings, analysis, and technology evaluations ONLY

#### Artifact-Only Directories
- **artifacts/**: Build outputs, compiled binaries, deployment packages ONLY
- **deploy/**: Deployment configurations, scripts, and manifests ONLY
- **build/**: Build scripts, compilation tools, and intermediate files ONLY
- **dist/**: Distribution packages and release artifacts ONLY
- **bin/**: Executable binaries and runtime tools ONLY

#### Containerization Directories
- **docker/**: Docker-related files and configurations ONLY
- **docker/compose/**: Docker Compose files for different environments ONLY
- **docker/images/**: Custom Dockerfile and image build contexts ONLY
- **docker/scripts/**: Docker utility and management scripts ONLY
- **.env.example**: Environment variable template with documentation ONLY

#### Source Code Directories
- **src/**: Source code implementation ONLY
- **tests/**: Test code and test fixtures ONLY
- **lib/**: Library dependencies and vendor code ONLY
- **config/**: Runtime configuration files ONLY

#### Script Directories
- **scripts/**: All demonstration, testing, and simulation scripts
- **scripts/test/**: Test scripts for validation and verification ONLY
- **scripts/demo/**: Demonstration scripts for showcasing features ONLY
- **scripts/simulate/**: Simulation scripts for testing scenarios ONLY
- **scripts/setup/**: Environment setup and bootstrap scripts ONLY

#### Strict Separation Rules
- **NO Artifacts in Docs**: NEVER place build outputs, deployment scripts, or binaries in documentation directories
- **NO Documentation in Artifacts**: NEVER place explanatory content, specs, or README files in artifact directories
- **Reference Links**: Documentation MAY reference artifacts using relative links, but artifacts MUST NOT embed documentation
- **Clear Boundaries**: Each directory MUST have a single, clear purpose with NO mixed content types
- **Clean Builds**: Artifact directories MUST be gitignored and regenerated during build processes

#### Exception Handling
- **Configuration Examples**: Documentation MAY include configuration examples in code blocks
- **Diagram Sources**: Diagram source files (Mermaid, PlantUML) belong in documentation directories
- **Template Files**: Build and deployment templates belong in artifact directories
- **Scripts**: Documentation scripts belong in docs/, build scripts belong in build/ or deploy/

### Containerization & Docker Standards
All multi-service applications MUST follow comprehensive containerization practices:

#### Docker Compose Requirements
- **Multi-Service Support**: MUST provide docker-compose.yml when application has 2+ services
- **Environment Separation**: MUST use separate .env files with clear organization and access
- **Development Focus**: Docker Compose MUST be optimized for development workflows
- **Service Dependencies**: MUST properly define service dependencies and startup order
- **Volume Management**: MUST use appropriate volumes for data persistence and development

#### Environment Configuration Standards
- **.env File Organization**: MUST have .env.example with all required variables documented
- **Environment Access**: Environment files MUST be easy to access and modify
- **Variable Naming**: MUST use consistent naming conventions (SERVICE_VARIABLE format)
- **Secrets Management**: MUST separate secrets from non-sensitive configuration
- **Development Overrides**: MUST support environment-specific overrides

#### Docker Architecture Research Requirements
- **Pre-Implementation Research**: MUST conduct Docker architecture research before implementation
- **Service Design**: MUST evaluate monolith vs microservices containerization approaches
- **Resource Planning**: MUST analyze resource requirements and optimization strategies
- **Network Design**: MUST plan service communication and network topology
- **Data Persistence**: MUST design data persistence strategies for stateful services

#### Containerization Best Practices
- **Single Responsibility**: Each container MUST have a single primary responsibility
- **Stateless Design**: Services MUST be stateless where possible, externalize state
- **Health Checks**: All services MUST implement appropriate health checks
- **Logging**: Services MUST log to stdout/stderr for centralized collection
- **Graceful Shutdown**: Services MUST handle SIGTERM gracefully

#### Docker Compose File Structure
- **Version Specification**: MUST use Docker Compose v3+ format
- **Service Definition**: Each service MUST have clear image, ports, and environment configuration
- **Network Configuration**: MUST define custom networks for service isolation
- **Volume Configuration**: MUST use named volumes for persistent data
- **Development Services**: MUST include development tools (database admin, monitoring)

#### Development Workflow Integration
- **Hot Reload**: MUST support hot reload for development efficiency
- **Debugging**: MUST support debugging configuration for containers
- **Testing Integration**: MUST integrate with testing frameworks and pipelines
- **IDE Integration**: MUST support IDE integration with containerized services
- **Documentation**: MUST include comprehensive Docker usage documentation

## Quality Assurance & Testing

### Testing Mandate
All new functionality MUST be developed using Test-Driven Development (TDD) methodology. Every feature MUST include unit tests with a minimum of 90% code coverage and at least one integration test for primary use cases.

### Definition of Done
A task is considered 'Done' only when:
- Code is implemented and follows constitutional principles
- All required tests are passing with 90%+ coverage
- Documentation is updated and consistent
- Changes are reviewed for constitutional compliance
- Templates are synchronized if changes affect them

### Static Analysis & Quality Gates
All Markdown files MUST pass structural validation. All command scripts MUST be tested for functionality. Constitution compliance checks MUST pass for all changes.

### Testing Strategy & Requirements
All code MUST follow comprehensive testing principles ensuring reliability, maintainability, and confidence in deployments:

#### Unit Testing Principles
- **Test Isolation**: Each unit test MUST be independent and not rely on other tests or external state
- **Fast Execution**: Unit tests MUST complete quickly (<100ms per test) to enable rapid feedback
- **Clear Assertions**: Tests MUST have explicit assertions with descriptive failure messages
- **Edge Case Coverage**: Tests MUST cover boundary conditions, error cases, and null inputs
- **Mock External Dependencies**: Tests MUST use mocks/stubs for external services and databases

#### Integration Testing Principles
- **Real Environment**: Integration tests MUST run against realistic test environments
- **Contract Validation**: Tests MUST validate API contracts and data exchange formats
- **Database Interactions**: Tests MUST verify database operations and data integrity
- **Service Communication**: Tests MUST verify inter-service communication patterns
- **Error Propagation**: Tests MUST validate error handling across service boundaries

#### Test Organization & Structure
- **Test Naming**: Tests MUST use descriptive names following "Given_When_Then" pattern
- **Arrange-Act-Assert**: Tests MUST follow AAA structure for clarity and maintainability
- **Test Data Management**: Tests MUST create and cleanup their own data using fixtures
- **Test Categories**: Tests MUST be categorized (unit, integration, e2e) for selective execution
- **Documentation**: Complex test scenarios MUST include explanatory comments

#### Performance & Load Testing
- **Response Time Validation**: Tests MUST validate response times meet performance requirements
- **Load Testing**: Critical paths MUST have load tests verifying scalability
- **Resource Usage**: Tests MUST monitor memory, CPU, and connection usage
- **Stress Testing**: System MUST be tested beyond expected load to identify breaking points

#### Test-Driven Development (TDD) Process
- **Red Phase**: Write failing test before implementation code
- **Green Phase**: Write minimal code to make test pass
- **Refactor Phase**: Improve code while keeping tests green
- **Cycle Repetition**: TDD cycle MUST be repeated for each feature increment
- **Regression Prevention**: Tests MUST prevent reintroduction of fixed bugs

#### Test Environment & CI/CD Integration
- **Automated Execution**: Tests MUST run automatically on every commit and pull request
- **Parallel Execution**: Tests MUST support parallel execution to reduce feedback time
- **Environment Parity**: Test environments MUST mirror production configuration
- **Test Reporting**: Test results MUST be visible and easily accessible
- **Gatekeeping**: Tests MUST block merges when failing or coverage drops below threshold

## Twelve-Factor Development Principles

### Factor I: Codebase
One codebase tracked in revision control, multiple deployments. MUST use Git with single repository per application. All branches and deployments track the same codebase.

### Factor II: Dependencies
All dependencies MUST be explicitly declared and isolated. Use dependency management tools (package.json, requirements.txt, etc.). Never rely on system-wide packages.

### Factor III: Config
Store configuration in environment variables. NEVER store configuration in code. Separate config from code to support different deployment environments without code changes.

### Factor IV: Backing Services
Treat backing services (databases, queues, caches) as attached resources. MUST be configurable via connection strings in environment variables. Support local and cloud provider variations.

### Factor V: Build, Release, Run
Strictly separate build and run stages. Build stage transforms code repo into executable bundle. Release stage combines build with config. Run stage executes the application.

### Factor VI: Processes
Execute the app as one or more stateless processes. State MUST be stored in external backing services. Processes MUST be disposable and can be restarted without data loss.

### Factor VII: Port Binding
Export services via port binding. Apps MUST be self-contained and expose HTTP as a service by binding to a port. Handle incoming requests directly without embedding webserver.

### Factor VIII: Concurrency
Scale out via the process model. All work MUST be done by processes. Share-nothing architecture enables horizontal scaling and load distribution.

### Factor IX: Disposability
Maximize robustness with fast startup and graceful shutdown. Processes MUST handle SIGTERM gracefully for zero-downtime deployments. Support sudden death/failure scenarios.

### Factor X: Dev/Prod Parity
Keep development, staging, and production as similar as possible. Minimize gaps between development and production environments. Use same backing services, dependencies, and configurations.

### Factor XI: Logs
Treat logs as event streams. Logs MUST be written to stdout/stderr as unstructured streams. Execution environment collects, buffers, and routes log streams to final destinations.

### Factor XII: Admin Processes
Run admin/management tasks as one-off processes. Administrative scripts MUST run in identical execution environment as regular application processes with same configuration.

## Security & Compliance

### Dependency Management
No dependencies with known critical or high-severity vulnerabilities are permitted. All AI agent integrations must follow secure practices. No sensitive information may be logged or committed.

### Data Handling
No Personally Identifiable Information (PII) may be logged in plain text. All configuration must be managed through environment variables or secure configuration management, never committed to repositories.

### AI Agent Security
All AI agent interactions must be logged for auditability. No credentials or API keys may be exposed in templates or documentation. Agent instructions must not contain sensitive information.

### System Configuration Standards
All cloud regions MUST use the Asia/Bangkok timezone (UTC+7) as the standard timezone configuration. This ensures consistent timestamp handling across all deployment environments and simplifies debugging and log analysis.

## Development Workflow & Tooling

### Version Control Strategy
All development MUST occur on feature branches named using the format 'feat/DESCRIPTION or fix/DESCRIPTION'. Commits MUST follow the Conventional Commits specification. All merges to 'main' MUST be done via pull requests.

### Template Management
All templates must be versioned and synchronized. Template changes must trigger consistency checks across all dependent files. Template validation must pass before changes are accepted.

### Multi-Agent Support
The system MUST support multiple AI agents (Claude, Copilot, Gemini, etc.) with consistent interfaces. Agent-specific instructions must be isolated and not affect core functionality.

### Development Environment Standards
All development MUST prioritize Unix-like environments with Windows as supported alternative:

#### Primary Development Platforms
- **macOS**: First-priority development environment with full tooling support
- **Linux**: First-priority development environment with full tooling support
- **Windows**: Supported alternative environment with compatibility layer

#### Platform-Specific Requirements
- **macOS**: Use Homebrew for package management, fish shell as primary with Terminal.app or iTerm2
- **Linux**: Use native package managers (apt, yum, pacman) based on distribution, bash as primary shell
- **Windows**: Use WSL2 (Windows Subsystem for Linux) for Unix-like compatibility, bash as primary shell

#### Cross-Platform Tooling
- **Command Line Tools**: All scripts MUST use cross-platform commands (bash, sh, python)
- **Development Tools**: Prefer tools with native macOS/Linux support and Windows compatibility
- **Containerization**: Docker MUST be used for consistent development environments across platforms
- **Path Handling**: All scripts MUST handle Unix (/) and Windows (\) path separators correctly

#### Shell Configuration & Scripting
- **Fish Shell (macOS)**: Use fish configuration files (~/.config/fish/config.fish) for aliases and functions
- **Bash Shell (Linux/Windows)**: Use bash configuration files (~/.bashrc, ~/.bash_profile) for aliases and functions
- **Cross-Shell Scripts**: All project scripts MUST use bash syntax for maximum compatibility
- **Shell Functions**: Provide both fish and bash versions of custom shell functions in documentation
- **Environment Variables**: Set environment variables in shell-agnostic ways (export commands work in both shells)

#### Development Environment Setup
- **Shell Environment**: fish shell as primary on macOS, bash as primary on Linux, WSL2 bash on Windows
- **Node.js/npm**: Cross-platform installation using official installers or version managers
- **Git**: Cross-platform configuration with consistent line ending settings
- **IDE/Editor**: VS Code with cross-platform extensions and consistent configuration

#### Windows-Specific Considerations
- **WSL2 Requirement**: Windows development MUST use WSL2 for Unix-like environment
- **File System**: Use WSL2 file system for development, avoid Windows file system limitations
- **Permissions**: Ensure proper file permissions in WSL2 environment
- **Performance**: Optimize Docker Desktop and WSL2 settings for development performance

#### Documentation and Training
- **Setup Guides**: Platform-specific setup documentation MUST be provided
- **Troubleshooting**: Common platform-specific issues MUST be documented
- **Tooling Instructions**: Installation and configuration instructions for each platform
- **Best Practices**: Platform-specific development best practices MUST be documented

### Documentation Standards
All changes must be documented in appropriate specification files. Constitution changes must include version bump rationale and impact analysis. All Markdown files must follow consistent formatting and structure.

### Research Standards & Requirements
All implementation decisions MUST be based on current, verified information from web research:

#### Pre-Implementation Research Requirements
- **Technology Selection**: MUST research latest versions, release notes, and breaking changes
- **Security Advisories**: MUST check for known vulnerabilities and security recommendations
- **Community Status**: MUST verify project health, maintenance status, and community support
- **Alternative Analysis**: MUST research and compare alternative solutions and approaches
- **Best Practices**: MUST identify current best practices and implementation patterns

#### Research Documentation Standards
- **Research Findings**: MUST document research results with sources and dates
- **Decision Rationale**: MUST document reasoning behind technology choices and approach decisions
- **Alternative Evaluation**: MUST document considered alternatives and rejection reasons
- **Risk Assessment**: MUST document identified risks and mitigation strategies
- **Reference Links**: MUST include reference links to research sources and documentation

#### Research Validation Process
- **Source Verification**: MUST use authoritative sources (official docs, well-maintained community resources)
- **Recency Validation**: MUST ensure information is current (preferably within last 6-12 months)
- **Multiple Sources**: MUST cross-reference information from multiple sources when possible
- **Community Consensus**: MUST verify community consensus on best practices and approaches
- **Expert Opinions**: MUST consider expert opinions and thought leadership when available

#### Research Scope & Areas
- **Framework Updates**: Latest features, deprecation notices, migration guides
- **Library Versions**: Recent updates, breaking changes, new features
- **Tooling Evolution**: Current best tools, emerging alternatives, community adoption
- **Security Standards**: Current security practices, vulnerability disclosures, compliance requirements
- **Performance Trends**: Current performance optimization techniques and benchmarks
- **Architecture Patterns**: Modern architectural approaches and anti-patterns to avoid

#### Ongoing Research Requirements
- **Periodic Reviews**: MUST conduct periodic research to stay current with technology evolution
- **Monitoring Changes**: MUST monitor for breaking changes, security updates, and major releases
- **Community Engagement**: MUST stay engaged with relevant communities for updates and insights
- **Technology Radar**: MUST maintain awareness of emerging technologies and trends
- **Knowledge Sharing**: MUST share research findings with team and update documentation

### Development Workflow Standards
All development work MUST follow comprehensive workflow standards for consistency and safety:

#### Task Management
- **TodoWrite Usage**: MUST use TodoWrite to track all work items and maintain visibility
- **Single Task Focus**: Only one task in progress at a time to maintain focus and quality
- **Immediate Completion**: MUST mark tasks complete immediately upon finishing
- **Subtask Breakdown**: MUST break complex work into manageable subtasks
- **Progress Tracking**: All progress MUST be visible through task management system

#### Code Change Management
- **Context Understanding**: MUST read before editing - understand context first
- **Pattern Preservation**: MUST preserve existing patterns and conventions
- **Pre-Commit Testing**: MUST test changes before committing
- **Decision Documentation**: MUST document non-obvious decisions
- **Incremental Validation**: MUST validate each change before proceeding

#### Communication Protocols
- **File-Based Outputs**: All worker results MUST be file-based outputs
- **Structured Formats**: MUST use structured formats (JSON/Markdown) for machine parsing
- **Naming Conventions**: MUST use clear naming with timestamps and task identifiers
- **Progress Monitoring**: MUST monitor progress through BashOutput, not direct stdout
- **Audit Trail**: All communications MUST be logged and traceable

#### Safety Guidelines - Command Execution
- **Interactive Confirmation**: MUST use interactive confirmation for deletions (rm -i instead of rm -rf)
- **No Force Operations**: MUST never force-push to git repositories
- **Pre-Execution Validation**: MUST validate operations before execution
- **Audit Logging**: MUST maintain audit logs of all operations
- **Rollback Capability**: MUST ensure operations can be reversed when possible

#### Safety Guidelines - File Operations
- **Existence Verification**: MUST check existence before creating directories
- **Path Validation**: MUST verify paths before operations
- **Reversible Operations**: MUST use safe file operations that can be reversed
- **Explicit Confirmation**: MUST never overwrite without explicit confirmation
- **Backup Strategy**: MUST maintain backups before critical file operations

#### System Resource Management
- **Resource Monitoring**: MUST monitor resource usage for parallel operations
- **Concurrency Limits**: MUST limit concurrent workers to 5-10 for system stability
- **Complexity-Based Reasoning**: MUST use appropriate reasoning levels for task complexity
- **Process Cleanup**: MUST clean up stuck processes promptly
- **Performance Monitoring**: MUST monitor system performance during operations

### Workflows & Planning Standards
All development work MUST follow comprehensive workflow and planning standards:

#### Testing Discipline - Manual Testing Checklist
Before pushing any changes, ALL items MUST be completed:
- **Build Success**: Run build command successfully without errors
- **Clean Build**: Verify no new build warnings or type errors
- **Feature Testing**: Test all affected pages and features thoroughly
- **Console Verification**: Check browser console for any errors
- **Mobile Testing**: Test mobile responsiveness if applicable
- **Interactive Verification**: Verify all interactive features work as expected

#### GitHub Workflow - Issue Creation Process
When starting new features or bug fixes, MUST follow this process:
```bash
# 1. Update main branch
git checkout main && git pull

# 2. Create detailed issue with structured format
gh issue create --title "feat: Descriptive title" --body "$(cat <<'ISSUE'
## Overview
Brief description of the feature/bug.

## Current State
What exists now.

## Proposed Solution
What should be implemented.

## Technical Details
- Components affected
- Implementation approach

## Acceptance Criteria
- [ ] Specific testable criteria
- [ ] Performance requirements
- [ ] UI/UX requirements
ISSUE
)"
```

#### GitHub Workflow - Standard Development Flow
All development MUST follow this exact flow:
```bash
# 1. Create feature branch from issue
git checkout -b feat/issue-number-description

# 2. Implement changes following constitution principles

# 3. Test thoroughly (use 'ttt' for full test suite)

# 4. Commit with structured message format
git add -A
git commit -m "feat: Brief description

- What: Specific changes made
- Why: Motivation for the changes
- Impact: What this affects

Closes #issue-number"

# 5. Push and create Pull Request
git push -u origin branch-name
gh pr create --title "Same as commit" --body "Fixes #issue_number"

# 6. ⚠️ CRITICAL: NEVER MERGE PRs YOURSELF
# - DO NOT use: gh pr merge
# - DO NOT use: Any merge commands
# - ONLY provide the PR link to the user
# - WAIT for explicit user instruction to merge
```

#### Planning Issue Structure Standards
All planning issues MUST include these structured sections:
- **Overview**: High-level summary of the work
- **Current State**: Description of existing situation
- **Proposed Solution**: Detailed implementation approach
- **Technical Details**: Components affected and implementation approach
- **Acceptance Criteria**: Specific, testable criteria with checkboxes

#### Implementation Execution Standards (gogogo)
When executing planned implementations:
1. **Find Implementation Issue**: Locate the most recent `plan:` issue
2. **Execute Implementation**: Follow plan step-by-step with constitutional compliance
3. **Test & Verify**: Run all relevant tests and verify implementation works
4. **Commit & Push**: Commit with descriptive message, push to feature branch, create/update PR
5. **Report Progress**: Provide clear status updates on implementation progress

#### Pull Request Management
- **No Self-Merging**: AI agents MUST NEVER merge their own pull requests
- **Review Process**: MUST wait for human review and explicit approval
- **Link Provision**: MUST provide PR link to user for review
- **Status Reporting**: MUST report implementation status and request next steps

### Operational Safety Standards
All operations MUST follow comprehensive safety standards to prevent irreversible damage:

#### Repository Usage Guidelines
- **Appropriate Repository Targeting**: ALWAYS work with the appropriate repository for your project
- **Upstream Repository Protection**: NEVER create issues/PRs on upstream repositories without permission
- **Repository Verification**: All GitHub operations MUST target the correct repository
- **Permission Validation**: MUST verify repository permissions before any operations

#### Command Usage Safety Standards
- **Force Flag Prohibition**: NEVER use -f or --force flags with any commands
- **Safe Command Options**: MUST always use safe, non-destructive command options
- **Interactive Confirmation Handling**: If commands require confirmation, handle appropriately without forcing
- **Verbose Operations**: MUST use verbose options to show what commands are doing
- **Command Prevalidation**: MUST validate commands before execution

#### Git Operations Safety Standards
- **No Force Pushing**: NEVER use git push --force or git push -f
- **No Force Checkout**: NEVER use git checkout -f
- **No Force Cleaning**: NEVER use git clean -f
- **History Preservation**: MUST always use safe git operations that preserve history
- **Branch Protection**: MUST protect main and production branches from force operations

#### ⚠️ CRITICAL Pull Request Management
- **No Self-Merging Policy**: NEVER MERGE PULL REQUESTS WITHOUT EXPLICIT USER PERMISSION
- **Prohibited Merge Commands**: NEVER use gh pr merge unless explicitly instructed by the user
- **Review Requirement**: MUST always wait for user review and approval before any merge
- **Link Provision**: MUST provide PR link to user for review and approval
- **Status Reporting**: MUST report implementation status and request merge instructions

#### File Operations Safety Standards
- **Interactive Deletion**: NEVER use rm -rf - MUST use rm -i for interactive confirmation
- **Pre-Deletion Confirmation**: MUST always confirm before deleting files
- **Reversible Operations**: MUST use safe file operations that can be reversed
- **Backup Requirements**: MUST maintain backups before critical file operations
- **Path Validation**: MUST verify file paths before operations

#### Package Manager Safety Standards
- **No Force Installation**: NEVER use [package-manager] install --force
- **Controlled Updates**: NEVER use [package-manager] update without specifying packages
- **Lockfile Review**: MUST review lockfile changes before committing
- **Dependency Verification**: MUST verify package dependencies before installation
- **Version Management**: MUST use explicit version specifications for critical dependencies

#### General Safety Guidelines
- **Safety Prioritization**: MUST prioritize safety and reversibility in all operations
- **Confirmation Requirements**: MUST ask for confirmation when performing potentially destructive actions
- **Command Explanation**: MUST explain the implications of commands before executing them
- **Operation Logging**: MUST maintain logs of all operations for audit purposes
- **Rollback Planning**: MUST have rollback plans for critical operations

### Visualization Standards
All documentation MUST incorporate visual elements to enhance clarity and understanding when requested by users:

#### Mermaid Diagrams Requirements
- **Workflow Diagrams**: All multi-step processes MUST be visualized using Mermaid flowcharts
- **Architecture Diagrams**: System components and interactions MUST use Mermaid graphs
- **Sequence Diagrams**: Inter-service communications and API flows MUST use Mermaid sequence diagrams
- **Timeline Diagrams**: Project phases and milestones MUST use Mermaid Gantt charts
- **Class Diagrams**: Data models and object relationships MUST use Mermaid class diagrams

#### Table Standards
- **Feature Comparisons**: MUST use structured Markdown tables with clear headers
- **Configuration Data**: MUST use tables for environment variables and settings
- **Test Results**: MUST use tables for test coverage and performance metrics
- **Technology Decisions**: MUST use comparison tables for technology evaluations

#### Chart and Graph Requirements
- **Performance Metrics**: MUST include visual representations of response times and throughput
- **Coverage Reports**: MUST include visual coverage indicators and trends
- **Progress Tracking**: MUST include visual burn-down charts and completion metrics
- **Quality Metrics**: MUST include visual quality gates and compliance indicators

#### Visualization Integration Rules
- **User-Triggered**: Visualizations MUST be provided when users explicitly request diagrams or explanations
- **Contextual**: Visualizations MUST be relevant to the specific concept being explained
- **Accessible**: All visualizations MUST include descriptive alt text and explanations
- **Consistent**: Visual styling MUST be consistent across all documentation
- **Maintained**: Visualizations MUST be updated when underlying data or processes change

#### Required Visualizations by Document Type
- **Specifications**: User journey flows, data model diagrams, feature comparison tables
- **Plans**: Architecture diagrams, timeline charts, dependency graphs, task breakdown tables
- **Tasks**: Workflow diagrams, progress tracking charts, test result tables
- **Constitution**: Principle relationship diagrams, compliance check matrices

### Demonstration & Simulation Standards
All complex implementations MUST include executable scripts for testing and demonstration:

#### Script Requirements & Standards
- **User-Requested Scripts**: MUST provide shell scripts when users explicitly request testing, demos, or simulations
- **Platform Compatibility**: Scripts MUST run on macOS (fish), Linux (bash), and Windows (WSL2 bash)
- **Executable Permissions**: All scripts MUST have proper execute permissions and shebang lines
- **Error Handling**: Scripts MUST include comprehensive error handling and validation
- **Self-Contained**: Scripts MUST be self-contained with clear dependencies and setup instructions

#### Script Categories & Use Cases
- **Test Scripts**: Validate functionality, test edge cases, verify system behavior under various conditions
- **Demo Scripts**: Demonstrate key features, showcase workflows, provide interactive examples
- **Simulation Scripts**: Simulate real-world scenarios, load testing, performance validation
- **Setup Scripts**: Bootstrap development environments, install dependencies, configure systems
- **Integration Scripts**: Test system integration, validate API endpoints, verify data flows

#### Script Structure & Documentation
- **Header Comments**: Each script MUST include purpose, usage instructions, and requirements
- **Parameter Validation**: Scripts MUST validate input parameters and provide usage help
- **Logging**: Scripts MUST include appropriate logging and progress indicators
- **Cleanup**: Scripts MUST cleanup temporary files and restore system state when appropriate
- **Exit Codes**: Scripts MUST use proper exit codes for success/failure scenarios

#### Script Storage & Organization
- **scripts/**: Directory for all demonstration, testing, and simulation scripts
- **scripts/test/**: Test scripts for validation and verification
- **scripts/demo/**: Demonstration scripts for showcasing features
- **scripts/simulate/**: Simulation scripts for testing scenarios
- **scripts/setup/**: Environment setup and bootstrap scripts

#### Script Distribution & Execution
- **Cross-Platform Support**: Provide both bash and fish versions when shell-specific features are beneficial
- **Dependency Management**: Scripts MUST document and optionally install required dependencies
- **Idempotent Operations**: Scripts MUST be safe to run multiple times without side effects
- **Rollback Capability**: Scripts MUST provide rollback mechanisms when making system changes
- **Execution Environment**: Scripts MUST specify required environment variables and configurations

## Governance

### Constitutional Supremacy
This constitution supersedes all other project practices and guidelines. When conflicts arise between this constitution and other project documentation, this constitution takes precedence. All project activities MUST comply with constitutional requirements.

### Amendment Process
All changes to this constitution must be proposed via a pull request targeting this file. Amendments require:
- **Documented Rationale**: MUST provide documented rationale for the change explaining why it's needed
- **Impact Assessment**: MUST include impact assessment on existing workflows and systems
- **Migration Plan**: MUST provide migration plan for affected components and processes
- **Explicit Approval**: MUST obtain explicit approval before implementation
- **Version Bump**: Changes must include version bump according to semantic versioning rules

### Versioning Policy
Constitution versions follow semantic versioning (MAJOR.MINOR.PATCH):
- MAJOR: Backward incompatible governance/principle removals or redefinitions
- MINOR: New principle/section added or materially expanded guidance
- PATCH: Clarifications, wording, typo fixes, non-semantic refinements

### Compliance Review
All specifications, plans, and tasks MUST be checked for constitutional compliance. AI agents must flag constitutional violations during planning and suggest alternatives. Human reviewers must verify constitutional compliance in pull requests.

### Enforcement Mechanisms
The constitution is enforced through:
- Automated checks in templates and commands
- AI agent validation during planning phases
- Human review gates in pull requests
- Template consistency validation
- Impact analysis for changes

**Version**: 2.4.0 | **Ratified**: 2025-10-02 | **Last Amended**: 2025-10-02