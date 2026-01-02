# Template System Capability

## Purpose
Provide novel-specific template files and a variable replacement mechanism, enabling users to quickly start writing different types of novels.

## ADDED Requirements

### Requirement: Template File Management
The system MUST provide novel-specific template files.

#### Scenario: Provide project.md template
- **WHEN** user initializes project
- **THEN** copy `templates/project.md.template` to project
- **THEN** template includes sections for project info, creative principles, style guide, quality standards, taboos
- **THEN** use `{{NOVEL_NAME}}`, `{{GENRE}}`, `{{TARGET_WORDS}}`, `{{VOLUMES}}` variables

#### Scenario: Provide AGENTS.md template
- **WHEN** user initializes project
- **THEN** copy `templates/AGENTS.md.template` to project
- **THEN** template includes AI assistant workflow instructions
- **THEN** include explanation for `/novelspec-proposal`, `/novelspec-apply`, `/novelspec-archive` commands

#### Scenario: Provide character spec template
- **WHEN** user needs to create character spec
- **THEN** provide `templates/characters/_template/spec.md.template`
- **THEN** template includes Purpose, Requirements (Basic setting, behavior pattern, dialogue style)
- **THEN** use `{{CHARACTER_NAME}}`, `{{AGE}}`, `{{PERSONALITY}}`, `{{TRAITS}}` variables

#### Scenario: Provide worldbuilding spec template
- **WHEN** user needs to create worldbuilding spec
- **THEN** provide `templates/worldbuilding/magic-system/spec.md.template`
- **THEN** template includes Purpose, Requirements (Cultivation levels, combat power gaps, special rules)
- **THEN** use `{{SYSTEM_NAME}}`, `{{LEVELS}}` etc. variables

#### Scenario: Provide outline spec template
- **WHEN** user needs to create outline spec
- **THEN** provide `templates/outline/spec.md.template`
- **THEN** template includes Purpose, Requirements (Chapter spec examples)
- **THEN** include example Requirements + Scenarios for Chapters 1-3

### Requirement: Variable Replacement Mechanism
The system MUST support template variable replacement.

#### Scenario: Identify template variables
- **WHEN** processing template files
- **THEN** identify variables in `{{VARIABLE}}` format
- **THEN** support alphanumeric and underscore variable names

#### Scenario: Replace variables
- **WHEN** applying template variables
- **THEN** replace `{{NOVEL_NAME}}` with user-input novel name
- **THEN** replace `{{GENRE}}` with user-selected genre
- **THEN** keep unmatched variables as is

#### Scenario: Handle missing variables
- **WHEN** variable value is not provided
- **THEN** use default value or empty string
- **THEN** do not output error (optional variables)

### Requirement: Template Content Specification
Template files SHALL include clear examples and instructions.

#### Scenario: project.md template content
- **WHEN** viewing project.md template
- **THEN** include complete creative principles example (logical consistency, character consistency, plot reasonableness, unified style)
- **THEN** include style guide example (narrative perspective, language style, chapter length)
- **THEN** include quality standards example
- **THEN** include taboos example

#### Scenario: Character spec template content
- **WHEN** viewing character spec template
- **THEN** include basic setting Requirement example
- **THEN** include behavior pattern Requirement example (when facing danger, when facing temptation)
- **THEN** include dialogue style Requirement example
- **THEN** each Requirement includes complete Scenarios

#### Scenario: Worldbuilding spec template content
- **WHEN** viewing worldbuilding spec template
- **THEN** include cultivation level system Requirement example
- **THEN** include combat power gap Requirement example
- **THEN** include special rules Requirement example (e.g., Sign-in System)
- **THEN** each Requirement includes verifiable Scenarios

### Requirement: Template Extensibility
The system SHALL allow users to customize templates.

#### Scenario: User customizes template
- **WHEN** user modifies `novelspec/project.md`
- **THEN** keep user modified content
- **THEN** do not overwrite with subsequent commands

#### Scenario: User adds new template
- **WHEN** user adds new template file in `templates/`
- **THEN** system recognizes and can use the new template
- **THEN** support same variable replacement mechanism
