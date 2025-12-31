# Proposal: Add MVP Core Functionality

## Why

Novel-Writer-OpenSpec is a new project that needs to implement Phase 1 MVP core functionality to validate the feasibility of the OpenSpec methodology in the field of novel writing.

Current State: Project only has PRD documentation, no actual code.

Goal: Implement Minimum Viable Product, including project initialization, basic validation, and AI assistant integration, enabling users to:
1. Initialize a novel project
2. Create and validate spec proposals
3. Use `/novelspec-proposal` command via AI assistant

## What Changes

- **CLI Basic Framework**: Implement `novelspec` CLI tool, supporting `init` and `validate` commands
- **Project Initialization**: Implement `novelspec init <project-name>` to create novel project structure
- **Template System**: Provide novel-specific templates (project.md, AGENTS.md, character/worldbuilding/outline spec.md templates)
- **Format Validator**: Implement format validation (check formats of proposal.md, tasks.md, spec.md)
- **AI Assistant Instructions**: Create AGENTS.md, defining `/novelspec-proposal` and other commands
- **Basic Documentation**: README and workflow-guide

**Excludes** (Phase 2 and later):
- Semantic validation (character consistency, world consistency)
- Cross-chapter validation (timeline, foreshadowing tracking)
- `novelspec archive` command
- Web interface or VS Code extension

## Impact

### Affected Specs
Added the following capability specs:
- `specs/cli-init/spec.md` - Project initialization function
- `specs/cli-validate/spec.md` - Format validation function
- `specs/template-system/spec.md` - Template system
- `specs/ai-integration/spec.md` - AI assistant integration

### Affected Code
Added the following files and directories:
- `src/` - Source code directory
  - `cli.ts` - CLI entry
  - `commands/init.ts` - init command
  - `commands/validate.ts` - validate command
  - `core/parser.ts` - Markdown parser
  - `core/validator.ts` - Format validator
  - `core/template-manager.ts` - Template manager
  - `utils/file-ops.ts` - File operation utils
- `templates/` - Template file directory
  - `project.md.template`
  - `AGENTS.md.template`
  - `characters/_template/spec.md.template`
  - `worldbuilding/magic-system/spec.md.template`
  - `outline/spec.md.template`
- `package.json` - Project configuration and dependencies
- `tsconfig.json` - TypeScript configuration
- `README.md` - User documentation
- `docs/workflow-guide.md` - Workflow guide

### Breaking Changes
None (New project)

### Migration
No migration needed (New project)
