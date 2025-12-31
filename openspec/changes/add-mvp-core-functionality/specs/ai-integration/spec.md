# AI Integration Capability

## Purpose
Provide AI assistant integration instructions and workflow guidance, enabling AI to efficiently use the novelspec tool to assist in novel writing.

## ADDED Requirements

### Requirement: AGENTS.md Instruction File
The system MUST provide a `novelspec/AGENTS.md` file to guide AI assistants.

#### Scenario: Include workflow guidelines
- **WHEN** AI assistant reads `novelspec/AGENTS.md`
- **THEN** include five-stage workflow explanation (Create Proposal -> Validate -> Execute -> Continuous Verification -> Archive)
- **THEN** each stage includes specific steps and commands

#### Scenario: Include command instructions
- **WHEN** AI assistant reads `novelspec/AGENTS.md`
- **THEN** include `/novelspec-proposal` command instruction
- **THEN** include `/novelspec-apply` command instruction
- **THEN** include `/novelspec-archive` command instruction

#### Scenario: Include format specifications
- **WHEN** AI assistant reads `novelspec/AGENTS.md`
- **THEN** include Requirements + Scenarios format specifications
- **THEN** include ADDED/MODIFIED/REMOVED usage instructions
- **THEN** include common errors and correction examples

### Requirement: /novelspec-proposal Command Definition
The system SHALL define `/novelspec-proposal` AI command behavior.

#### Scenario: Create proposal process
- **WHEN** AI executes `/novelspec-proposal`
- **THEN** ask user for creative intent (Create Chapter X-Y/Extend setting)
- **THEN** create `changes/<change-id>/` directory structure
- **THEN** generate `proposal.md` (Why/What/Impact)
- **THEN** generate `tasks.md` (Task list)
- **THEN** generate `specs/` deltas (ADDED/MODIFIED Requirements)
- **THEN** run `novelspec validate <change-id>` check
- **THEN** output validation results and modification suggestions

#### Scenario: Read context
- **WHEN** AI executes `/novelspec-proposal`
- **THEN** read `novelspec/project.md` (Creative principles)
- **THEN** read `novelspec/specs/` (Current specs)
- **THEN** generate deltas based on existing specs

#### Scenario: Generate proposal.md
- **WHEN** AI generates proposal.md
- **THEN** Why section explains creative goal
- **THEN** What Changes lists spec changes
- **THEN** Impact marks affected specs and new chapters

### Requirement: /novelspec-apply Command Definition
The system SHALL define `/novelspec-apply` AI command behavior.

#### Scenario: Execute writing process
- **WHEN** AI executes `/novelspec-apply`
- **THEN** read `proposal.md` (Understand intent)
- **THEN** read `design.md` (if exists, understand technical plan)
- **THEN** read `tasks.md` (Get task list)
- **THEN** execute tasks sequentially
- **THEN** generate chapter content to `chapters/`
- **THEN** run `novelspec validate` after completing each chapter
- **THEN** mark completed tasks as `[x]`

#### Scenario: Continuous verification
- **WHEN** AI writes chapters
- **THEN** run format verification after completing each chapter
- **THEN** check content conforms to specs (Protagonist behavior, magic usage, plot)
- **THEN** fix immediately if there are errors

### Requirement: /novelspec-archive Command Definition
The system SHALL define `/novelspec-archive` AI command behavior (MVP phase only explains, does not implement).

#### Scenario: Archive prompt
- **WHEN** AI executes `/novelspec-archive`
- **THEN** prompt user that archive function is implemented in Phase 2
- **THEN** explain archive process (Merge delta to specs/, move to archive/)

### Requirement: Format Specification Documentation
`AGENTS.md` MUST include clear format specifications.

#### Scenario: Requirements format specification
- **WHEN** AI reads format specification
- **THEN** explain using `### Requirement:` format (3 hashes)
- **THEN** explain using SHALL/MUST/MAY keywords
- **THEN** provide correct and incorrect example comparisons

#### Scenario: Scenarios format specification
- **WHEN** AI reads format specification
- **THEN** emphasize using `#### Scenario:` format (4 hashes)
- **THEN** explain using WHEN/THEN conditions
- **THEN** provide correct and incorrect example comparisons

#### Scenario: Delta operation specification
- **WHEN** AI reads format specification
- **THEN** explain ADDED (New content)
- **THEN** explain MODIFIED (Modify existing content, need to copy completely)
- **THEN** explain REMOVED (Delete content, mark reason)
- **THEN** explain RENAMED (Rename only)

### Requirement: Examples and Best Practices
`AGENTS.md` SHALL include practical examples.

#### Scenario: Complete proposal example
- **WHEN** AI reads AGENTS.md
- **THEN** include complete proposal example for writing chapters 11-20
- **THEN** include full content of proposal.md, tasks.md, specs/
- **THEN** include validation success and failure examples

#### Scenario: Common errors and fixes
- **WHEN** AI reads AGENTS.md
- **THEN** include common format error examples (Scenario using 3 hashes, missing WHEN/THEN)
- **THEN** include corresponding correction methods
- **THEN** include debugging commands (`novelspec validate --strict`)
