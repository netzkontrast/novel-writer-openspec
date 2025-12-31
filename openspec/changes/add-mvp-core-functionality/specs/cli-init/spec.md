# CLI Init Capability

## Purpose
Provide `novelspec init` command, enabling users to quickly initialize a novel project, including complete `novelspec/` directory structure and template files.

## ADDED Requirements

### Requirement: Project Initialization Command
The system MUST provide `novelspec init` command to create novel project structure.

#### Scenario: Basic project initialization
- **WHEN** user runs `novelspec init my-novel`
- **THEN** create `my-novel/` directory
- **THEN** create `my-novel/novelspec/` directory structure
- **THEN** copy `project.md` template to `my-novel/novelspec/project.md`
- **THEN** copy `AGENTS.md` template to `my-novel/novelspec/AGENTS.md`
- **THEN** create `novelspec/specs/` directory
- **THEN** create `novelspec/changes/` and `novelspec/changes/archive/` directories
- **THEN** create `chapters/` directory
- **THEN** create `docs/` directory
- **THEN** output success message and next steps

#### Scenario: Initialize in current directory
- **WHEN** user runs `novelspec init my-novel --here` in existing directory
- **THEN** create `novelspec/` structure in current directory
- **THEN** do not create new project directory
- **THEN** output success message

#### Scenario: Directory already exists error
- **WHEN** user runs `novelspec init my-novel`
- **THEN** if `my-novel/` directory already exists
- **THEN** output error message: "Directory 'my-novel' already exists"
- **THEN** exit code is 1

### Requirement: Template Variable Replacement
The system SHALL prompt user for project info during initialization and replace template variables.

#### Scenario: Collect project info
- **WHEN** user runs `novelspec init my-novel`
- **THEN** prompt user for novel name (default: my-novel)
- **THEN** prompt user for genre (Fantasy/Wuxia/Urban/Sci-Fi/Other)
- **THEN** prompt user for target word count (default: 1 million words)
- **THEN** prompt user for estimated volume count (default: 4 volumes)

#### Scenario: Apply template variables
- **WHEN** user provides project info
- **THEN** replace `{{NOVEL_NAME}}` in `project.md`
- **THEN** replace `{{GENRE}}` in `project.md`
- **THEN** replace `{{TARGET_WORDS}}` in `project.md`
- **THEN** replace `{{VOLUMES}}` in `project.md`

### Requirement: Success Message and Guidance
The system SHALL provide clear next steps after successful initialization.

#### Scenario: Output next steps
- **WHEN** project initialization successful
- **THEN** output: "✓ Project 'my-novel' initialized successfully!"
- **THEN** output: "Next steps:"
- **THEN** output: "1. cd my-novel"
- **THEN** output: "2. Edit novelspec/project.md to set creative principles"
- **THEN** output: "3. Use AI assistant /novelspec-proposal to create first proposal"
