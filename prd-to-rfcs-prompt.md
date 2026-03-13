You are an expert software architect and project manager tasked with breaking down the attached Product Requirements Document (PRD), features list, and project rules into manageable Request for Comments (RFC) documents for implementation.

Create a set of well-structured RFC documents that divide the project into logical, implementable units of work. Each RFC should represent a cohesive, reasonably-sized portion of the application that can be implemented as a unit. The RFCs MUST be organized in a clear implementation order that accounts for dependencies and logical build sequence. IMPORTANT: RFCs will be implemented strictly one by one in sequential order, so the ordering is critical.

If any critical information is missing or unclear in the provided documents that prevents thorough RFC creation, ask specific questions to gather the necessary details before proceeding.

Generate the RFCs files under RFCs folder including PROMPT CREATION md files by:

1. IMPLEMENTATION ORDER ANALYSIS:
   - Analyze the entire project to determine the optimal implementation sequence
   - Identify foundation components that must be built first
   - Create a directed graph of feature dependencies (described textually)
   - Determine critical path items that block other development
   - Group features into implementation phases based on dependencies
   - Assign sequential numbers to RFCs that reflect their strict implementation order (001, 002, 003, etc.)
   - CRITICAL: Each RFC will be implemented one at a time in numerical order, so the sequence must be logical and buildable
   - Each RFC must be fully implementable after all previous RFCs in the sequence have been completed
   - No parallel implementation will occur - RFC-002 will only begin after RFC-001 is complete
   - Map all dependencies between features to ensure the sequential order is feasible

2. FEATURE GROUPING:
   - Group related features that should be implemented together in a single RFC
   - Ensure each RFC represents a logical, cohesive unit of functionality
   - Balance RFC size - not too small (trivial) or too large (unmanageable)
   - Consider dependencies between features when grouping
   - Identify shared components or services that multiple features might depend on
   - Organize groups to align with the strict sequential implementation order
   - Ensure features that build upon each other are grouped in the correct sequence

3. RFC STRUCTURE:
   - Assign a unique identifier to each RFC that reflects implementation order (e.g., RFC-001-User-Authentication for the first component to be implemented)
   - Provide a clear title that describes the functionality
   - Include a summary of what the RFC covers
   - List all features/requirements addressed in the RFC
   - Detail technical approach and architecture considerations
   - Explicitly identify which previous RFCs this RFC builds upon
   - Specify which future RFCs will build upon this RFC
   - Estimate relative complexity (Low, Medium, High)
   - Include detailed acceptance criteria for each feature
   - Specify any API contracts or interfaces that will be exposed
   - Document data models and database schema changes required
   - Outline state management approach where applicable
   - Include specific implementation details such as:
     * Required file structure and organization
     * Key algorithms or business logic to implement
     * UI/UX specifications and design patterns to follow
     * State management approach
     * API integration details
     * Database interactions and data flow
     * Error handling requirements
     * Testing strategy with specific test cases
     * Performance considerations and optimization techniques

Propose a structure, following this sections template:
```
/<feature-rfc-name dir or file>/
  README.md
    - Entry overview for the specification
    - High-level summary of the proposed solution
    - List of features/requirements and use-cases addressed by this specification
    - Explicitly identify which previous features this feature builds upon
    - Specify which future features are expected to build on this feature
    - Key architectural decisions and rationale
    - Estimate relative complexity (Low, Medium, High) for features
    - Acceptance criteria / success criteria the implementation must satisfy
    - Links to all sections below

  /diagrams/
    - Extracted diagrams referenced by documentation
    - Diagrams must be clearly named and referenced from files
    *.mmd
    *.puml

  /01-architecture/
    - System-level architecture of the feature
    - Describes the high-level technical structure, system components and services involved in the feature
    - Overview of the interaction with existing systems and external services
    - Data flow/topology between parties or services

  /02-domain/
    - Domain data models and business logic
    - Domain entities, attributes, invariants and lifecycle behaviour
    - Business rules and validation rules
    - Persistence model related to the domain
    - data retention policies if applicable
    - domain invariants, validations and business constraints
    - Domain models' and their properties' lifecycle/state machines with states, transitions, guards, side effects, error states, etc.
    persistence.md
    <lifecycle>.md
    <state-machine>.md

  /03-behaviours-and-flows/
    - Application logic flows using the domain
    - Describes how requests, events or jobs move through the system
    - Covers synchronous and asynchronous behaviours
    - Focuses on functional behaviour from trigger to outcome
    <flow-name>.md
      - Each flow in a separate file, with diagrams and code references
      - Trigger
      - Preconditions
      - Step-by-step processing sequence
      - Error paths
      - Side effects and outputs
      - Dependencies on domain entities or interfaces

  /04-runtime-operations/
    - Runtime execution model of the feature in production
    - Describes how execution is initiated, coordinated, retried, constrained and recovered
    - Must not duplicate business/application flows
    - triggers logic entrypoints that activate feature execution, required data or conditions for execution to start
    orchestration.md
    - orchestration: coordination between services, processes or jobs, handoff between sync/async stages if applicable
    - scheduling logic: cron jobs, polling loops, delayed execution, recurring jobs
    - retry strategies, backoff, deduplication and idempotency guarantees
    - concurrency-control: locking, single-flight execution, race prevention, partition ownership
    - execution timeouts, throttling, backpressure, dependency limits
    - state reconciliation, replay or drift-correction behaviour if applicable

  /05-interfaces/
    - External and internal contracts exposed by the feature
    - Describes interfaces, not behavioural sequences
    - Defines APIs, message schemas, api gateway logic, scheduled/celery tasks supported interface etc

  /06-code-instructions/
    - Implementation guidance and mapping to repository structure
    - Helps developers or AI agents locate where logic should live
    - Should not duplicate repository-wide run/test instructions
    - entrypoints: controllers, handlers, consumers, schedulers
    - modules and their responsibilities
    - integration-points of services/components where feature logic must be integrated
    - code-map from spec sections to concrete code locations
    - code-specific testing instructions and instructions for mapping to test files and test cases

  /07-infrastructure/
    - Any cloud or server infrastructure relevant to the logic ot implement, shall be described here
    - for example terraform files, helm charts, service mesh/network config, ec2 instances configs, etc.

  /08-considerations/
    - Cross-cutting concerns, quality attributes and review topics
    - Covers what must be ensured, measured or accepted across the feature
    - expected performance characteristics,  bottlenecks, scaling expectations and optimization considerations
    - security risks and safeguards, authentication, authorization, secrets and sensitive data handling
    - regulatory, policy or audit requirements compliance, if any
    - observability: metrics, logs, tracing and alerting expectations
    - testing considerations: strategy, critical edge cases and failure scenarios, expected coverage focus and verification boundaries
    - known risks or limitations of the design
    - open/unresolved design questions
    - identified debt introduced or deferred
    - notable design tradeoffs and why they were accepted
    - release strategy, rollout stages, feature flag usage, rollback approach and migration considerations at a high level
```

Ensure:

- Each file ≤ 300 lines
- Cross-links between files
- If total length of feature's docs content/parts is <1000 lines and it doesn't have nested features and no long/extracted diagrams, it can be a single file, otherwise a dir
- If feature docs part's (like 01-architecture) content is less than a single file size threshold (300 lines) can be made a file instead of a dir, and vice versa.
- Points/dirs are created only when there is content to put in them, do not create empty dirs/files just for the structure
- Depending on complexity a nested parts of features, or nested features can be added, but all follow the same general and file structure rules


4. IMPLEMENTATION CONSIDERATIONS:
   - Highlight any technical challenges or considerations
   - Note any specific rules from RULES.md that particularly apply to this RFC
   - Identify potential edge cases or special handling requirements
   - Suggest testing approaches for the functionality
   - Specify performance expectations and optimization considerations
   - Address security concerns and required safeguards
   - Document any third-party dependencies or libraries needed
   - Outline error handling strategies and fallback mechanisms
   - Provide guidance on accessibility requirements
   - Include internationalization/localization considerations
   - Explain how this RFC fits into the overall sequential implementation plan
   - Describe how this RFC builds upon the functionality implemented in previous RFCs

5. IMPLEMENTATION PROMPT CREATION:
   - Create implementation prompts in strict numerical sequence (001, 002, 003, etc.)
   - For each RFC, create a corresponding implementation prompt file named "implementation-prompt-RFC-[ID].md"
   - IMPORTANT: You MUST copy the EXACT content from implementation-prompt-template.md as your starting point
   - First, read the entire implementation-prompt-template.md file to understand its structure and content
   - Make ONLY the following specific replacements in the template:
     * Replace all instances of "[ID]" with the RFC's identifier (e.g., "001")
     * Replace all instances of "[Title]" with the RFC's title (e.g., "User Authentication")
     * Replace all instances of "[brief description]" with a concise summary of the RFC's purpose
   - DO NOT modify, remove, or add any other content from the template
   - DO NOT change any section headings, formatting, or structure
   - DO NOT duplicate implementation details in the prompt that are already included in the RFC document
   - Verify that each implementation prompt maintains the exact same sections and instructions as the template
   - Double-check that all placeholders have been properly replaced before finalizing

6. RFCS.MD CREATION:
   - Create a master RFCS.md file that lists all RFCs in their strict numerical implementation order
   - Include a dependency graph or table showing relationships between RFCs
   - Provide a clear, sequential implementation roadmap
   - Group RFCs into implementation phases if appropriate
   - For each RFC, indicate which previous RFCs it builds upon
   - For each RFC, indicate which future RFCs will build upon it
   - Make it clear that implementation will proceed strictly in the numbered sequence

7. TECHNICAL SPECIFICATIONS:
   - For each RFC, provide detailed technical specifications including:
     * Component architecture diagrams (described textually)
     * Data flow diagrams (described textually)
     * API endpoints with request/response formats
     * Database schema changes with field definitions
     * State management patterns
     * Authentication and authorization requirements
     * Caching strategies where applicable
     * Specific algorithms or business logic pseudocode
     * Error codes and handling mechanisms
     * Logging and monitoring requirements
   - Explain how each technical specification builds upon or extends the implementations from previous RFCs
   - Ensure specifications account for the sequential implementation order

8. IMPLEMENTATION CONSTRAINTS:
   - Document any technical constraints that must be adhered to
   - Specify required coding standards and patterns
   - Note any performance budgets or requirements
   - List compatibility requirements (browsers, devices, etc.)
   - Identify any regulatory or compliance considerations
   - Highlight constraints that affect the sequential implementation order
   - Ensure constraints are addressed in the appropriate sequence

First, provide a brief overview of how you've approached breaking down the project, with special emphasis on the sequential implementation order you've determined. Then create the comprehensive set of RFC documents and implementation prompts following the structure above, organizing them in strict numerical implementation order.

Ensure each RFC is specific enough to guide implementation but flexible enough to allow for engineering decisions during development. Focus on creating RFCs that represent logical, cohesive units of functionality that can be reasonably implemented one after another.

The goal is to provide AI implementers with complete, unambiguous specifications that enable them to produce high-quality code without requiring additional clarification, while following a strict sequential implementation order. Each RFC must be fully implementable after all previous RFCs have been completed, with no parallel implementation. 