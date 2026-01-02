# CLI Validate Capability

## Purpose
Provide `novelspec validate` command to check if change proposals conform to Requirements + Scenarios specifications.

## ADDED Requirements

### Requirement: Format Validation Command
The system MUST provide `novelspec validate` command to validate change proposal formats.

#### Scenario: Validate single change
- **WHEN** user runs `novelspec validate add-chapter-1-10`
- **THEN** check `novelspec/changes/add-chapter-1-10/` directory exists
- **THEN** check `proposal.md` format (contains Why/What/Impact)
- **THEN** check `tasks.md` format (uses task list format)
- **THEN** check `specs/` spec.md format (Requirements + Scenarios)
- **THEN** output validation results

#### Scenario: Validate all active changes
- **WHEN** user runs `novelspec validate` (no arguments)
- **THEN** list all active changes
- **THEN** validate each change sequentially
- **THEN** output comprehensive validation results

#### Scenario: Strict validation mode
- **WHEN** user runs `novelspec validate add-chapter-1-10 --strict`
- **THEN** execute all format checks
- **THEN** extra check: each Requirement has at least one Scenario
- **THEN** extra check: Scenario uses `#### Scenario:` format (4 hashes)
- **THEN** extra check: use SHALL/MUST/MAY keywords
- **THEN** extra check: delta spec uses ADDED/MODIFIED/REMOVED tags

### Requirement: proposal.md Format Validation
The system MUST validate that proposal.md contains required sections.

#### Scenario: Validate Why section
- **WHEN** validating proposal.md
- **THEN** check existence of `## Why` section
- **THEN** check Why section has at least 1 sentence

#### Scenario: Validate What Changes section
- **WHEN** validating proposal.md
- **THEN** check existence of `## What Changes` section
- **THEN** check What Changes uses list format

#### Scenario: Validate Impact section
- **WHEN** validating proposal.md
- **THEN** check existence of `## Impact` section
- **THEN** check Impact marks affected specs

#### Scenario: Missing required section error
- **WHEN** proposal.md misses `## Why` section
- **THEN** output error: "proposal.md missing ## Why section"
- **THEN** validation fails

### Requirement: tasks.md Format Validation
The system MUST validate that tasks.md uses task list format.

#### Scenario: Validate task list format
- **WHEN** validating tasks.md
- **THEN** check at least one `- [ ]` or `- [x]` line
- **THEN** check task description is clear (non-empty)

#### Scenario: Task list format error
- **WHEN** tasks.md does not contain task list
- **THEN** output error: "tasks.md must use task list format (- [ ] or - [x])"
- **THEN** validation fails

### Requirement: spec.md Format Validation
The system MUST validate that spec.md uses Requirements + Scenarios format.

#### Scenario: Validate Requirements format
- **WHEN** validating spec.md
- **THEN** check existence of `### Requirement:` header
- **THEN** check each Requirement has description text

#### Scenario: Validate Scenarios format
- **WHEN** validating spec.md
- **THEN** check each Requirement has at least one `#### Scenario:` (4 hashes)
- **THEN** check Scenario contains WHEN/THEN conditions

#### Scenario: Scenario format error
- **WHEN** Scenario uses `### Scenario:` (3 hashes) instead of 4 hashes
- **THEN** output error: "Scenario must use #### Scenario: format (4 hashes)"
- **THEN** validation fails

#### Scenario: Missing Scenario error
- **WHEN** Requirement has no Scenario
- **THEN** output error: "Requirement '[name]' missing Scenario"
- **THEN** validation fails

### Requirement: Delta Spec Format Validation
The system MUST validate that delta spec uses ADDED/MODIFIED/REMOVED tags.

#### Scenario: Validate ADDED Requirements
- **WHEN** validating changes/.../specs/[capability]/spec.md
- **THEN** check existence of `## ADDED Requirements` section
- **THEN** check Requirements format under ADDED is correct

#### Scenario: Validate MODIFIED Requirements
- **WHEN** delta spec contains `## MODIFIED Requirements`
- **THEN** check Requirements under MODIFIED are complete (including all Scenarios)

#### Scenario: Missing operation tag error
- **WHEN** delta spec has no ADDED/MODIFIED/REMOVED tags
- **THEN** output error: "Delta spec must use ADDED/MODIFIED/REMOVED tags"
- **THEN** validation fails

### Requirement: Validation Result Output
The system SHALL output clear validation results.

#### Scenario: Text format output
- **WHEN** validation completes (default mode)
- **THEN** output format validation checklist (✓ Passed, ✗ Failed)
- **THEN** output error details and fix suggestions
- **THEN** output validation result summary (X errors, Y warnings)

#### Scenario: JSON format output
- **WHEN** user runs `novelspec validate <change> --json`
- **THEN** output JSON format validation results
- **THEN** include `valid`, `errors`, `warnings` fields
- **THEN** each error includes `file`, `type`, `message`, `suggestion` fields
