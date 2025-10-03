<!--
Sync Impact Report:
Version change: 3.4.0 → 3.5.0 (minor version)
Modified principles: Enhanced GitHub CLI Repository Creation (VII) to include comprehensive repository publishing standards
Added sections: Repository Publishing Standards, Repository Creation Process, Repository Publishing Process, and Safety Guidelines for Publishing as subsections of Principle VII
Removed sections: N/A
Templates requiring updates: ⚠ plan-template.md (needs repository publishing requirements integration), ⚠ tasks-template.md (needs publishing task categories), ⚠ spec-template.md (needs publishing clarification), ⚠ command templates (needs publishing guidance updates)
Follow-up TODOs: Update all templates to support repository publishing processes, add publishing checks to constitution compliance
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
Claude acts as orchestrator: planning, coordination, GitHub operations, monitoring. Codex workers handle execution: file operations, code changes, analysis tasks. Clear separation of concerns with file-based communication between components. Parallel execution preferred when tasks are independent. When users request multiple agents to run separately or spawn worker agents, git worktrees MUST be used to provide isolated working environments for each agent.

### V. Explicit Over Implicit
All file paths must be absolute, not relative. All output locations must be specified explicitly. Configuration and parameters must be visible and auditable. No hidden side effects or magical behaviors.

### VI. Meaningful Naming Convention
All specifications in git worktrees or branches MUST use meaningful, descriptive names that clearly communicate the feature purpose. NEVER use numeric prefixes (e.g., 001-, 002-) or generic identifiers. Names must be human-readable and instantly understandable. Examples: `user-authentication-system` instead of `001-read-this-n8n`.

### VII. GitHub CLI Repository Creation & Publishing Standards
When users request repository creation, MUST use `gh repo create` command. GitHub CLI is the standard tool for all repository operations, providing consistent authentication, proper configuration, and integration with existing workflows. Alternative methods MAY ONLY be used when GitHub CLI is unavailable or explicitly requested otherwise.

#### Repository Publishing Standards
When users request repository publishing, these standards MUST be followed:
- **Private-First Approach**: MUST use `gh publish --private` to publish repositories as private by default
- **User Decision Control**: Private repositories MUST remain private until user explicitly requests public visibility
- **Visibility Change Process**: User MUST make explicit decision to change visibility from private to public
- **Risk Assessment**: Before making repository public, security scan and sensitive data review MUST be completed
- **Documentation Requirements**: README and documentation MUST be complete before public publishing

#### Repository Creation Process
All repository creation MUST follow this process:
- **Initialization**: Use `gh repo create` with appropriate configuration
- **Privacy Setting**: Default to private visibility unless explicitly specified otherwise
- **Team Access**: Configure appropriate team permissions and access controls
- **Branch Protection**: Set up main branch protection rules
- **Issue Templates**: Configure issue and PR templates if required

#### Repository Publishing Process
When users request repository publishing:
- **Private Publication**: Execute `gh publish --private` as the default action
- **User Consultation**: Inform user that repository is published privately
- **Public Option**: Provide user with option to make repository public when ready
- **Change Confirmation**: Require explicit user confirmation before changing visibility
- **Security Review**: Conduct security review before public visibility change

#### Safety Guidelines for Publishing
- **Sensitive Data Check**: Verify no secrets, API keys, or sensitive information are present
- **License Verification**: Ensure appropriate license is in place for public repositories
- **Documentation Completeness**: README, contributing guidelines, and documentation must be complete
- **Code Review**: Full code review must be completed before public publishing
- **Dependency Audit**: Check for vulnerable dependencies before public visibility

### VIII. User Story Clarification Standards
Before planning any feature or implementation, the user story or requirements MUST be thoroughly checked, repeated, and clarified with the user. All ambiguous aspects, missing details, or unclear requirements MUST be resolved before proceeding to technical planning. Planning MUST NOT begin until user story clarity is achieved and confirmed.

#### User Story Validation Requirements
All user stories MUST pass these validation checks before planning:
- **Story Understanding**: The story is clearly understood by the AI agent in its entirety
- **Objective Clarity**: The business objective and user value proposition are unambiguous
- **Scope Definition**: Boundaries of what is included and excluded are explicitly defined
- **Acceptance Criteria**: Clear, measurable, and testable acceptance criteria are established
- **Context Understanding**: Business context, user personas, and usage scenarios are understood
- **Constraint Identification**: Technical constraints, business constraints, and limitations are identified

#### Clarification Process Standards
When user stories require clarification, the following process MUST be followed:
- **Initial Assessment**: Identify all unclear aspects and missing information
- **Question Formulation**: Prepare specific, targeted questions to resolve uncertainties
- **User Consultation**: Present questions and clarification requests to the user
- **Response Validation**: Review user responses and identify any remaining ambiguities
- **Confirmation Loop**: Repeat understanding back to user for verification
- **Documentation**: Record all clarifications and decisions for reference

#### Planning Gate Enforcement
Technical planning MUST NOT proceed until:
- All user story questions are resolved to user satisfaction
- User explicitly confirms the story is understood correctly
- Acceptance criteria are validated and approved
- Scope and boundaries are agreed upon
- All stakeholders (if applicable) have reviewed and approved the clarified story

#### Story Refinement Standards
Clarified user stories MUST follow these standards:
- **Clear Language**: Simple, unambiguous language that avoids technical jargon
- **Measurable Outcomes**: Success criteria that can be objectively measured
- **Value Focus**: Clear articulation of user value and business benefit
- **Testable Criteria**: Requirements that can be verified through testing
- **Complete Information**: All necessary details for implementation are included

### IX. Git Worktree Standards for Multi-Agent Scenarios
When users request multiple agents to run separately or spawn worker agents, git worktrees MUST be used to provide isolated working environments for each agent. Worktrees enable parallel development without interference between agents while maintaining synchronization with the main repository.

#### Multi-Agent Worktree Creation Standards
When creating worktrees for multiple agents, these standards MUST be followed:
- **Worktree Purpose**: Each worktree MUST be created for a specific agent or task with clear purpose
- **Isolation**: Each worktree MUST provide complete isolation from other agents' workspaces
- **Naming Convention**: Worktree directories MUST follow the pattern `worktrees/[agent-name]/[task-purpose]`
- **Branch Association**: Each worktree MUST be associated with a specific branch or commit
- **Configuration**: Each worktree MUST have proper git configuration for the assigned agent

#### Worktree Management Standards
All worktree operations MUST follow these management standards:
- **Creation Process**: Use `git worktree add <path> <branch>` with absolute paths and meaningful names
- **Branch Management**: Each worktree MUST work on a dedicated branch to prevent conflicts
- **Synchronization**: Regular synchronization with main repository using `git pull` in each worktree
- **Status Monitoring**: Track worktree status and prevent orphaned or abandoned worktrees
- **Cleanup Procedures**: Proper worktree removal using `git worktree remove` after task completion

#### Multi-Agent Coordination Standards
When multiple agents work simultaneously, these coordination standards MUST be followed:
- **Conflict Prevention**: Agents MUST work on separate branches within their worktrees
- **Communication Protocol**: File-based communication between agents via shared directories
- **Progress Tracking**: Centralized progress tracking accessible by orchestrator and all agents
- **Resource Management**: Monitor system resources to prevent agent interference
- **Error Handling**: Isolated error handling prevents one agent's failure from affecting others

#### Worktree Safety and Security Standards
All worktree operations MUST follow safety and security standards:
- **Path Validation**: Validate all worktree paths before creation to prevent directory conflicts
- **Permission Management**: Ensure proper file permissions for each agent's worktree
- **Backup Procedures**: Create worktree backups before critical operations
- **Rollback Capability**: Ability to restore worktree state if operations fail
- **Audit Logging**: Log all worktree creation, modification, and deletion operations

#### Agent Lifecycle Management
When managing multiple agent worktrees, these lifecycle standards MUST be followed:
- **Initialization**: Proper worktree setup and configuration for each spawned agent
- **Monitoring**: Continuous monitoring of agent worktree activity and resource usage
- **Communication**: Established communication channels between orchestrator and worker agents
- **Termination**: Clean worktree cleanup and resource release when agents complete tasks
- **Error Recovery**: Procedures for recovering from agent failures or worktree corruption

#### Worktree Performance Optimization
For optimal performance in multi-agent scenarios:
- **Resource Allocation**: Assign appropriate system resources to each agent worktree
- **Parallel Operations**: Enable parallel git operations across multiple worktrees when safe
- **Cache Management**: Manage git object caches to optimize performance across worktrees
- **Network Optimization**: Minimize network overhead for distributed worktree operations
- **Storage Management**: Monitor and manage disk space usage across all worktrees

### X. Code Review Standards
All pull requests MUST undergo systematic code review before merge with clear assignment matrices, SLA requirements, and approval criteria based on change size and risk level. Reviews must be constructive, specific, and address security, performance, functionality, testing, documentation, error handling, and dependencies.

### XI. CI/CD Pipeline Standards
All pull requests MUST pass mandatory quality gates including linting (0 errors/warnings), unit tests (≥90% coverage), integration tests, comprehensive code quality analysis, security scanning (no critical/high vulnerabilities), dependency scanning, and build success. When code scanning tools are implemented, they MUST follow the Code Quality & Security Scanning Standards (Section XIII). Deployment pipelines must include rollback capability, health checks, monitoring, and proper build failure management with defined escalation procedures.

### XII. Error Handling & Logging Standards
All errors must follow consistent exception hierarchies with proper context and user-friendly messages. Logging must be structured JSON format with correlation IDs, ISO timestamps, and appropriate log levels (DEBUG, INFO, WARN, ERROR, FATAL). Error monitoring must include rate tracking, pattern detection, and immediate alerting for critical errors and performance degradation.

### XIII. Code Quality & Security Scanning Standards
When code scanning tools are implemented into a project, they MUST follow comprehensive analysis standards covering both code quality and security aspects. Scanning MUST be integrated into development workflows and CI/CD pipelines with appropriate quality gates and reporting mechanisms.

#### Code Quality Analysis Requirements
All code quality analysis MUST include these essential capabilities:
- **Bug Detection**: Automated detection of potential bugs, logical errors, and runtime exceptions
- **Code Smell Identification**: Identification of maintainability issues, anti-patterns, and design problems
- **Vulnerability Detection**: Analysis for security vulnerabilities and potential attack vectors
- **Technical Debt Measurement**: Quantification of technical debt with remediation effort estimates
- **Code Complexity Analysis**: Cyclomatic complexity, cognitive complexity, and maintainability index
- **Coding Standards Enforcement**: Automated enforcement of team coding standards and best practices
- **Test Coverage Tracking**: Line coverage, branch coverage, and mutation testing coverage
- **Code Duplication Analysis**: Detection and reporting of duplicated code blocks and patterns

#### Security Scanning Requirements
All security scanning MUST include comprehensive security analysis:
- **OWASP Top 10 Coverage**: Automated detection of OWASP Top 10 security vulnerabilities
- **CWE Compliance**: Identification of Common Weakness Enumerations and security issues
- **Hardcoded Secrets Detection**: Scanning for exposed API keys, passwords, and credentials
- **Dependency Vulnerability Analysis**: Analysis of third-party dependencies for known vulnerabilities
- **Security Hotspots Review**: Manual review guidance for potential security issues requiring human assessment
- **Static Application Security Testing (SAST)**: Source code analysis for security vulnerabilities
- **Software Composition Analysis (SCA)**: Open source component vulnerability scanning
- **Infrastructure as Code Security**: Security scanning for Terraform, CloudFormation, and other IaC files

#### Code Scanning Integration Standards
When code scanning tools are implemented, they MUST follow these integration standards:
- **CI/CD Pipeline Integration**: Automated scanning on all pull requests and main branch builds
- **Quality Gate Enforcement**: Blocking merges that fail to meet defined quality and security thresholds
- **Incremental Analysis**: Analysis of new code changes vs. existing codebase for focused review
- **False Positive Management**: Process for marking and managing false positives in scanning results
- **Baseline Establishment**: Creation of quality and security baselines for trend analysis
- **Multi-Language Support**: Appropriate scanners for all programming languages used in the project
- **Custom Rule Configuration**: Custom quality rules and security policies tailored to project needs

#### Quality Gate Standards
Code scanning implementations MUST define and enforce these quality gates:
- **Bug Severity Threshold**: Zero critical bugs, maximum X major bugs per PR
- **Vulnerability Threshold**: Zero critical/high vulnerabilities, maximum X medium vulnerabilities
- **Code Coverage Requirements**: Minimum 80% line coverage, 70% branch coverage
- **Maintainability Rating**: Minimum B grade maintainability index
- **Duplication Threshold**: Maximum 3% code duplication
- **Technical Debt Ratio**: Maximum 5% technical debt ratio
- **New Code Quality**: Stricter thresholds for new code vs. legacy code

#### Reporting and Notification Standards
Code scanning tools MUST provide comprehensive reporting:
- **Dashboard Integration**: Real-time dashboards for quality and security metrics
- **Trend Analysis**: Historical tracking of quality metrics and security posture
- **PR Comments Integration**: Automated comments in pull requests with scanning results
- **Email/Slack Notifications**: Automated notifications for critical issues and quality gate failures
- **Executive Reports**: Regular quality and security reports for stakeholders
- **Technical Debt Reports**: Detailed technical debt analysis with prioritization
- **Remediation Guidance**: Clear guidance and examples for fixing identified issues

### XIII. Infrastructure Development Standards
All infrastructure development MUST follow established patterns with user-defined approach selection through clarification process. Infrastructure choices MUST be documented, justified, and aligned with project requirements. Infrastructure as Code (IaC) MUST be version controlled, tested, and reviewed like application code.

#### Infrastructure Clarification Requirements
Before implementing any infrastructure, the following MUST be clarified with the user:
- **Deployment Target**: Cloud provider (AWS, Azure, GCP) vs on-premise vs hybrid
- **Infrastructure Scale**: Single application vs microservices vs distributed system
- **Management Approach**: Managed services vs self-hosted vs container orchestration
- **Automation Level**: Manual setup vs partial automation vs full GitOps
- **Compliance Requirements**: Security standards, data residency, audit requirements
- **Team Expertise**: Available DevOps skills and learning tolerance

#### Infrastructure as Code (IaC) Standards
When IaC is selected, implementations MUST follow:
- **Tool Selection**: Terraform, CloudFormation, Pulumi, or Ansible based on user preference and expertise
- **Modular Design**: Infrastructure components MUST be modular and reusable
- **State Management**: Remote state storage with proper locking and encryption
- **Testing**: Infrastructure code MUST include unit tests, integration tests, and compliance validation
- **Documentation**: All infrastructure components MUST have comprehensive documentation
- **Secret Management**: Secrets MUST be externalized using vault services or managed secret stores

### XIV. DevOps Pipeline Standards
All DevOps implementations MUST align with user-defined maturity level and operational requirements. Pipeline complexity MUST match project scale and team capabilities.

#### DevOps Clarification Process
Pipeline implementations MUST require user clarification on:
- **Deployment Frequency**: Continuous deployment vs scheduled releases vs on-demand
- **Environment Strategy**: Single environment vs multiple environments (dev/staging/prod)
- **Quality Gates**: Required checks (security, performance, compliance) and failure handling
- **Rollback Strategy**: Automatic rollback vs manual approval vs blue-green deployment
- **Monitoring Requirements**: Basic health checks vs comprehensive observability vs APM integration
- **Team Workflow**: Feature flags vs trunk development vs release branches

#### Pipeline Implementation Standards
- **CI/CD Platform**: GitHub Actions, GitLab CI, Jenkins, or Azure DevOps based on user preference
- **Pipeline as Code**: All pipeline configurations MUST be version controlled
- **Security Integration**: Automated security scanning, dependency checks, and vulnerability assessment
- **Testing Integration**: Automated test execution with coverage reporting and quality gates
- **Artifact Management**: Proper artifact storage, versioning, and cleanup policies
- **Notification Strategy**: Alerting for failures, successes, and deployment status

### XV. Infrastructure Monitoring & Observability
All infrastructure MUST implement appropriate monitoring based on user-defined requirements and operational complexity.

#### Monitoring Clarification Requirements
Monitoring implementations MUST clarify:
- **Scope Requirements**: Infrastructure health vs application performance vs business metrics
- **Alerting Strategy**: Immediate alerts vs batch notifications vs dashboard-only monitoring
- **Retention Period**: Short-term debugging vs long-term trend analysis vs compliance storage
- **Access Control**: Team-wide access vs role-based access vs restricted admin access
- **Integration Needs**: Standalone monitoring vs integrated observability platform
- **Budget Constraints**: Open-source solutions vs commercial platforms vs hybrid approach

#### Observability Standards
- **Logs**: Structured logging with consistent format and correlation IDs
- **Metrics**: Key performance indicators, resource utilization, and business metrics
- **Tracing**: Distributed tracing for microservices and complex workflows
- **Dashboards**: Custom dashboards for different stakeholders and use cases
- **Alerting**: Intelligent alerting with proper escalation and suppression rules

## Architecture & Technology Mandates

### Technology Stack
- **Framework**: Spec-Kit methodology implementation
- **Languages**: TypeScript for tooling, Markdown for documentation
- **Templates**: Structured Markdown templates in .specify/templates/
- **Version Control**: Git with conventional commits (MUST use git for all Git operations)
- **GitHub CLI**: GitHub CLI (gh) for GitHub operations (MUST use gh for all GitHub API operations)
- **AI Integration**: Multi-agent support (Claude, Copilot, Gemini, etc.)
- **Developer Environment**: macOS and Linux as primary platforms, Windows as alternative

### API Design Standards
All APIs MUST follow semantic versioning with URL path versioning (/api/v1/, /api/v2/) and maintain backward compatibility for at least 2 major versions. Request/response formats must use consistent JSON structure with standardized error responses. Authentication must use JWT tokens with maximum 1-hour expiration and secure refresh token mechanisms. Rate limiting must be implemented per user/IP with proper headers and graceful degradation.

### Database Management Standards
All database migrations must be version controlled with rollback capability and tested on staging before production. Backup requirements include daily full backups with 30-day retention and storage in multiple geographic locations. Query performance must not exceed 100ms for 95th percentile with proper indexing and connection pooling. Data consistency must be enforced through database constraints, application-level validation, and regular consistency checks with comprehensive audit logging.

### Performance Standards
Performance budgets require 95th percentile response time < 200ms, First Contentful Paint < 1.5 seconds, Largest Contentful Paint < 2.5 seconds, and Time to Interactive < 3.8 seconds. Load testing must be conducted quarterly with 2x expected peak load testing. Multi-level caching must be implemented with proper invalidation strategies, cache hit ratio monitoring, and consistency across distributed systems. Performance monitoring must include real-time monitoring, alerting, and capacity planning.

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

### Enhanced Testing Standards
Integration testing must cover component interactions, database operations, external service integrations, API contracts, and message queue operations using dedicated test environments and mock services. End-to-end testing must cover all critical user journeys with cross-browser and cross-device testing including performance and accessibility compliance. Performance testing must be integrated with load testing tools and include stress testing, performance regression testing, and application profiling. Test data management must use automated generation with data privacy protection, consistency across test runs, and proper cleanup procedures.

### Code Quality Metrics
Code coverage requirements include minimum 90% line coverage, 85% branch coverage, 80% integration coverage, 100% critical path coverage, and 70% E2E scenario coverage. Complexity limits include maximum cyclomatic complexity of 10 per function, cognitive complexity of 15, function length of 50 lines, file length of 500 lines, and parameter count of 5 per function. Technical debt must be regularly identified, quantified, prioritized, and repaid with comprehensive tracking and monitoring.

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

### Comprehensive Security Standards
All changes must pass security review checklist covering authentication, authorization, input validation, SQL injection prevention, XSS prevention, sensitive data protection, and dependency vulnerability management. Daily automated vulnerability scanning must be conducted with critical vulnerabilities patched within 24 hours, high within 7 days, medium within 30 days, and low in next major release. Secrets must be encrypted at rest with principle of least privilege access, regular rotation (max 90 days), and comprehensive audit logging. Security testing must include automated SAST, quarterly DAST scans, annual penetration testing, and regular vulnerability assessments with tracked remediation.

## Security & Compliance

### Dependency Management
No dependencies with known critical or high-severity vulnerabilities are permitted. All AI agent integrations must follow secure practices. No sensitive information may be logged or committed.

### Data Handling
No Personally Identifiable Information (PII) may be logged in plain text. All configuration must be managed through environment variables or secure configuration management, never committed to repositories.

### AI Agent Security
All AI agent interactions must be logged for auditability. No credentials or API keys may be exposed in templates or documentation. Agent instructions must not contain sensitive information.

### Open Source License Compliance
All dependencies must undergo automated license scanning with documented approval processes for new dependencies. License compliance must be regularly monitored and audited with complete license inventory, clear policy guidelines, documented exceptions, and regular training. High-risk licenses must undergo legal review with comprehensive compliance reporting.

### Data Privacy and Protection
Personally identifiable information must be protected with data minimization principles, proper security, encryption, access control, and defined retention/deletion policies. GDPR and CCPA compliance must be maintained with privacy impact assessments, data breach response procedures, and regular privacy training.

### Accessibility Requirements
WCAG 2.1 AA compliance must be maintained with regular accessibility testing, comprehensive documentation, training and awareness programs, and continuous improvement practices. Accessible design principles must be followed in both development and maintenance phases.

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

### Enhanced Documentation Standards
API documentation must include complete OpenAPI 3.0 specification with interactive documentation, code examples in multiple languages, and comprehensive error documentation. Code documentation must cover all public APIs, complex logic, business rules, configuration options, and external dependencies. Architecture documentation must include system overviews, component diagrams, data flow diagrams, technology stack documentation, and design decision rationales with regular reviews and change tracking.

### Tooling and Development Environment Standards
IDE standards require VS Code with standardized extensions including code formatting, Git integration, debugging tools, testing tools, and documentation editing. Development tooling must include consistent Git configuration, standardized package managers, build tools, testing frameworks, and linting rules. Local development setup must use Docker for consistent environments, standardized environment variable management, automated setup procedures, and comprehensive troubleshooting documentation.

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

### Branch Management Strategy
Branch types include protected main branch, short-lived feature branches, stabilization release branches, emergency hotfix branches, and long-running development branches. Feature branches have maximum 2-week lifetime, release branches 4 weeks, and hotfix branches 1 week. Merge strategies prefer squash merge for clean history with merge commits for significant features, rebase for linear history, and fast-forward for simple integration. Hotfix procedures require 1-hour triage, 2-hour response team activation, 24-hour resolution, and 48-hour post-mortem.

### Release Management Standards
Release planning requires quarterly release calendars, feature planning, resource allocation, risk assessment, and stakeholder communication. Versioning must follow strict semantic versioning with Git tags, comprehensive version documentation, and environment promotion. Release validation requires automated testing, manual validation, performance testing, security testing, and integration testing with comprehensive rollback procedures, trigger criteria, and post-rollback analysis.

### Communication and Collaboration Standards
Meeting standards include daily standups with time limits, regular sprint planning, retrospectives, technical reviews, and stakeholder updates. Communication protocols must define channels, response times, documentation procedures, and escalation processes. Knowledge sharing requires comprehensive documentation, regular presentations, mentoring programs, training, and cross-team collaboration with centralized knowledge base, effective search, and regular updates.

### Incident Response and Escalation
Incident response procedures must include severity classification, response team roles, communication plans, resolution processes, and post-mortem learning. Escalation procedures must define triggers, paths, response times, documentation, and regular training with clear escalation matrices and stakeholder notification protocols.

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
git commit -m "type(scope): brief description

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

#### Conventional Commit Message Templates
All commit messages MUST follow the Conventional Commits specification. Each commit type has specific templates and use cases:

##### Commit Types and Templates

**feat: New Features**
```bash
feat(scope): add user authentication system

- What: Implemented JWT-based authentication with login/logout functionality
- Why: Enable secure user access and session management
- Impact: Adds authentication endpoints, middleware, and user session handling

Closes #123
```

**fix: Bug Fixes**
```bash
fix(scope): resolve memory leak in data processing

- What: Fixed improper cleanup of event listeners in data processor
- Why: Prevent memory accumulation during long-running operations
- Impact: Reduces memory usage, prevents application crashes

Fixes #124
```

**docs: Documentation**
```bash
docs(scope): update API documentation for v2.0 endpoints

- What: Added comprehensive examples and parameter descriptions
- Why: Improve developer experience and API usability
- Impact: Complete documentation coverage for all public endpoints
```

**style: Code Style**
```bash
style(scope): normalize code formatting in service layer

- What: Applied consistent indentation and line breaks
- Why: Improve code readability and maintain consistency
- Impact: No functional changes, formatting improvements only
```

**refactor: Code Refactoring**
```bash
refactor(scope): extract validation logic to dedicated service

- What: Moved validation rules from controllers to validation service
- Why: Improve separation of concerns and code reusability
- Impact: Cleaner controllers, reusable validation across endpoints
```

**perf: Performance Improvements**
```bash
perf(scope): optimize database queries with proper indexing

- What: Added composite indexes for frequently queried columns
- Why: Reduce query execution time and improve response speed
- Impact: 40% reduction in average query response time
```

**test: Testing**
```bash
test(scope): add integration tests for payment processing

- What: Created comprehensive test suite for payment workflows
- Why: Ensure payment processing reliability and edge case handling
- Impact: 95% test coverage for payment module
```

**build: Build System**
```bash
build(scope): update webpack configuration for production optimization

- What: Added code splitting and tree shaking configurations
- Why: Reduce bundle size and improve loading performance
- Impact: 25% smaller production bundles
```

**ci: Continuous Integration**
```bash
ci(scope): add automated security scanning to GitHub Actions

- What: Integrated npm audit and dependency vulnerability checks
- Why: Proactively detect and prevent security vulnerabilities
- Impact: Automated security validation on all pull requests
```

**chore: Maintenance**
```bash
chore(scope): update dependencies to latest stable versions

- What: Updated React, TypeScript, and supporting libraries
- Why: Incorporate bug fixes and performance improvements
- Impact: Improved stability and access to latest features
```

**revert: Revert Changes**
```bash
revert(scope): revert previous authentication changes

- What: Rolled back commits abc1234 and def5678 due to issues
- Why: Address critical bugs introduced in recent changes
- Impact: Restores system stability while investigating issues

This reverts commit abc1234.
```

##### Commit Message Requirements

**Format**: `type(scope): description`

- **type**: One of the commit types listed above
- **scope**: Specific module or component affected (optional for global changes)
- **description**: Brief, imperative mood description (max 50 characters)

**Body Requirements**:
- **What**: Specific changes made (technical details)
- **Why**: Motivation for the changes (business/technical reason)
- **Impact**: Effect on the system (performance, behavior, etc.)
- **Issue Reference**: Closes #123, Fixes #123, or Resolves #123 when applicable

**Examples by Category**:

**Features**: `feat(auth): add two-factor authentication support`
**Bug Fixes**: `fix(api): handle null values in user profile endpoint`
**Documentation**: `docs(readme): update installation instructions for macOS`
**Refactoring**: `refactor(database): extract connection pool management`
**Performance**: `perf(cache): implement Redis caching for frequently accessed data`

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

**Version**: 3.5.0 | **Ratified**: 2025-10-02 | **Last Amended**: 2025-10-03