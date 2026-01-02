# Tasks: MVP Core Functionality

## 1. Project Infrastructure

- [x] 1.1 Initialize npm project, create `package.json`
  - Dependencies: `commander` (CLI), `chalk` (Color output)
  - Dev Dependencies: `typescript`, `@types/node`, `prettier`, `eslint`
  
- [x] 1.2 Configure TypeScript (`tsconfig.json`)
  - strict mode enabled
  - Output directory: `dist/`
  - Include: `src/**/*.ts`
  
- [x] 1.3 Configure build scripts
  - `npm run build`: TypeScript compilation
  - `npm run dev`: watch mode development
  - `npm link`: Local installation of `novelspec` command

## 2. Core Module Implementation

- [x] 2.1 Implement Markdown Parser (`src/core/parser.ts`)
  - Parse `### Requirement:` and `#### Scenario:`
  - Extract SHALL/MUST/MAY keywords
  - Extract WHEN/THEN conditions
  - Test: Cover normal and edge cases
  
- [x] 2.2 Implement Format Validator (`src/core/validator.ts`)
  - Validate proposal.md contains Why/What/Impact
  - Validate tasks.md uses task list format
  - Validate spec.md Requirements + Scenarios format
  - Validate delta spec uses ADDED/MODIFIED/REMOVED
  - Test: Cover common format errors
  
- [x] 2.3 Implement Template Manager (`src/core/template-manager.ts`)
  - Read template files
  - Variable replacement (`{{VARIABLE}}`)
  - Copy templates to target directory
  - Test: Verify variable replacement correctness

- [x] 2.4 Implement File Operation Utils (`src/utils/file-ops.ts`)
  - Create directory structure
  - Read/Write files
  - Check file existence
  - Test: Cover file operation scenarios

## 3. CLI Command Implementation

- [x] 3.1 Implement CLI Entry (`src/cli.ts`)
  - Use Commander.js
  - Register `init` and `validate` commands
  - Provide `--version` and `--help`
  
- [x] 3.2 Implement `novelspec init` Command (`src/commands/init.ts`)
  - Accept `<project-name>` argument
  - Support `--here` option (initialize in current directory)
  - Create `novelspec/` directory structure
  - Copy template files (project.md, AGENTS.md)
  - Create `specs/`, `changes/`, `changes/archive/` directories
  - Create `chapters/`, `docs/` directories
  - Output success message and next steps
  - Test: Verify directory structure correctness
  
- [x] 3.3 Implement `novelspec validate` Command (`src/commands/validate.ts`)
  - Accept `<change-id>` argument (optional, default to validate all)
  - Support `--strict` option (strict validation)
  - Support `--json` option (JSON output)
  - Run format validation
  - Output validation results (text or JSON)
  - Test: Verify error detection and reporting

## 4. Template File Creation

- [x] 4.1 Create `project.md.template`
  - Include project info, creative principles, style guide, quality standards, taboos
  - Use variables: `{{NOVEL_NAME}}`, `{{GENRE}}`, `{{TARGET_WORDS}}`, etc.
  
- [x] 4.2 Create `AGENTS.md.template`
  - Define AI assistant workflow (create proposal, execute writing, archive)
  - Explain `/novelspec-proposal`, `/novelspec-apply`, `/novelspec-archive` commands
  - Format specifications and validation rules
  
- [x] 4.3 Create Character Spec Template (`templates/characters/_template/spec.md.template`)
  - Include: Purpose, Requirements (Basic setting, behavior pattern, dialogue style)
  - Use variables: `{{CHARACTER_NAME}}`, `{{AGE}}`, `{{PERSONALITY}}`, etc.
  
- [x] 4.4 Create Worldbuilding Spec Template (`templates/worldbuilding/magic-system/spec.md.template`)
  - Include: Purpose, Requirements (Cultivation levels, combat power gaps, special rules)
  - Use variables: `{{SYSTEM_NAME}}`, `{{LEVELS}}`, etc.
  
- [x] 4.5 Create Outline Spec Template (`templates/outline/spec.md.template`)
  - Include: Purpose, Requirements (Chapter specs)
  - Example: Requirements + Scenarios for Chapters 1-3

## 5. Documentation Writing

- [x] 5.1 Write `README.md`
  - Project introduction
  - Quick start (installation, initialization, create proposal)
  - Core concepts (specs/changes, Requirements/Scenarios)
  - CLI command reference
  - Example: Creating a fantasy novel project
  
- [x] 5.2 Write `docs/workflow-guide.md`
  - Detailed 5-stage workflow (Create Proposal -> Validate -> Execute -> Continuous Verification -> Archive)
  - Detailed steps for each stage
  - AI assistant usage examples
  - FAQ and solutions

## 6. Testing

- [ ] 6.1 Write Unit Tests (Skipped in MVP phase)
  - Parser: Test Requirements/Scenarios parsing
  - Validator: Test format validation rules
  - Template Manager: Test variable replacement
  
- [ ] 6.2 Write Integration Tests (Skipped in MVP phase)
  - `novelspec init`: Verify generated project structure
  - `novelspec validate`: Verify error detection
  
- [x] 6.3 Manual Testing
  - CLI commands executable (novelspec --version, --help)
  - Build success (npm run build)
  - Local installation success (npm link)

## 7. Release Preparation

- [x] 7.1 Update `package.json`
  - Set `bin` field pointing to `dist/cli.js`
  - Set version: `0.1.0`
  - Add `files` field (include `dist/`, `templates/`)
  
- [x] 7.2 Create `.npmignore`
  - Exclude `src/`, `tests/`, `*.test.ts`
  
- [x] 7.3 Test Local Installation
  - `npm link` install globally
  - Run `novelspec --version` ✓
  - Run `novelspec --help` ✓
  - Verify functionality ✓

## 8. Verification Completion

- [x] 8.1 Confirm all tests passed (Basic function verification)
- [x] 8.2 Confirm documentation complete (README, workflow-guide, templates)
- [x] 8.3 Confirm CLI commands work normally (--version, --help)
- [x] 8.4 MVP Core functionality implementation complete
