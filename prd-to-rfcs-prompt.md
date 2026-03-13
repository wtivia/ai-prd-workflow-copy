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
    - docs overview file, if the feature is a dir not a single file
    - Include a summary of what this feature docs covers
    - List all features/requirements addressed in the docs
    - Explicitly identify which previous features this feature builds upon
    - Specify which future features were build upon this feature
    - Estimate relative complexity (Low, Medium, High)
    - If provided, document detailed acceptance criteria for each feature that the implementation satisfied
  /diagrams/ 
    - all big/extracted diagrams go here, named clearly
    *.mmd
    *.puml
  /01-architecture/ - contains detailed technical approach and architecture considerations, overview/explanation, like services-catalog, data flow diagrams between parties/services
  /02-domain/ 
    - data models, states, and theirs' or their properties' core state behaviours/processing/lifecycle logic (core business logic) description if any. 
    - Documented data models and database schemas/their changes
    state-machines.md or lifecycle.md 
    - data models and their properties lifecycle/state machines
    db.md
  /03-behaviours-and-flows/
    - usecases, complex behaviours and flows of the investigated logic (mainly application logic that uses business logic and domain), like request/response flows, async flows, batch/scheduled jobs flows, webhooks flows, etc. 
    - Documented with diagrams and code instruction references if needed.
    <flow-name>.md - each flow in a separate file, with diagrams and code references
    state-machine.md - if there is a state machine related to the application logic, it can be described in a separate file or included in the flow files if not too big
  /04-operating-logic/ 
    - Execution Mechanics of what operations this logic can run and how, not the same as business/application logic flows, similar to operating details of the application logic. Should describe not how the logic works, but what, how, when it (and its result) is triggered/processed and side effects.
    - how feature's logic parts are configured, operated/managed, maintained, triggered, what are the entrypoints, what data is required for the trigger, what are the side effects of the trigger, how the processing of the logic result is orchestrated
    - orchestration, scheduled tasks', tracking/monitoring/alerting's configs and logic, if any
    - short description of used testing strategy with specific/complex test cases to implement, aimed type and quality of the coverage
  /05-interface/ 
    - description of any exposed external or internal (between parts of the system) contracts/interfaces/entrypoints
    - Documents api, message schemas, api gateway logic, scheduled/celery tasks supported interface etc.
    api.md
    message-schemas.md
  /06-code-instructions/ - any code-related map/references or other info to document. Should not include details on how to run and test this code, that should be covered by the repository's docs.
    code-map.md
  /07-infrastructure/
    - if identified any cloud or server infrastructure related to the investigated logic, it shall be described here
    - for example terraform files, helm charts, service mesh config, ec2 instances configs, etc.
  /08-considerations/
    - Performance considerations and optimization techniques of the implementation
    - Security concerns and required safeguards of the implementation
    - Compliance and regulatory considerations
    - risks, cross-cutting logic, hidden logic that could not be put in any of previous dirs
    - key/critical findings, unresolved questions regarding the implementation, open questions, etc
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