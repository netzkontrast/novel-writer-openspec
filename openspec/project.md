# Project Context

## Purpose
Novel-Writer-OpenSpec is a novel writing management tool based on the OpenSpec methodology. Through the separated management of `specs/` (established truth) and `changes/` (change proposals), it provides clear context and strict verification mechanisms for AI-assisted novel creation.

## Tech Stack
- **Language**: TypeScript
- **Runtime**: Node.js ≥ 18.0.0
- **Package Manager**: npm/pnpm
- **CLI Framework**: Commander.js or similar
- **Validation**: Custom Markdown Parser + Requirements/Scenarios Validation

## Project Conventions

### Code Style
- Use TypeScript strict mode
- Prettier formatting, 2-space indentation
- ESLint code quality checks
- JSDoc comments for functions and classes

### Architecture Patterns
- **Command Pattern**: CLI commands implemented independently (`commands/init.ts`, `commands/validate.ts`, etc.)
- **Core Layer Separation**: Parser, Validator, Archiver as independent modules
- **File Conventions**: All spec files use Markdown format, following Requirements + Scenarios structure

### Testing Strategy
- Unit tests cover core modules (Parser, Validator, Archiver)
- Integration tests cover CLI commands
- Use real novel spec files as test fixtures

### Git Workflow
- Main branch: `main`
- Feature branch: `feature/[description]`
- Commit format: Conventional Commits (`feat:`, `fix:`, `docs:`, etc.)

## Domain Context

### Novel Writing Terminology
- **Character Spec**: Defines character identity, personality, behavior patterns, dialogue style
- **Worldbuilding Spec**: Defines magic systems, geography, factions/organizations, historical background
- **Outline Spec**: Defines chapter outlines and plot development
- **Change Proposal**: Proposal to write new chapters or extend settings

### OpenSpec Methodology Application
- **specs/**: Established novel specifications (characters, worldbuilding, outline)
- **changes/**: Chapters to be written and setting changes
- **Requirements**: Use SHALL/MUST to express spec requirements
- **Scenarios**: Verifiable scenarios using WHEN/THEN format

## Important Constraints

1. **Namespace Independence**: Use `novelspec` command and `novelspec/` directory to avoid conflict with OpenSpec
2. **No Constitution**: Creative principles integrated into `project.md` instead of a separate spec
3. **Strict Formatting**: Must use `#### Scenario:` format (4 hashes), each Requirement must have at least one Scenario
4. **Incremental Tagging**: Changes must explicitly use ADDED/MODIFIED/REMOVED tags

## External Dependencies

- No external API dependencies
- Local file system operations
- Optional: Git integration (future)

## Novelspec-Specific Conventions

### Project Structure
Novel projects use the following structure:
```
my-novel/
├── novelspec/              # Spec management directory
│   ├── project.md          # Project conventions
│   ├── AGENTS.md           # AI assistant instructions
│   ├── specs/              # Established specs
│   └── changes/            # Change proposals
└── chapters/               # Chapter content
```

### Validation Rules
- Format Verification: Check file structure and syntax
- Semantic Verification: Check character consistency, world consistency, plot consistency
- Cross-Chapter Verification: Check timeline, character status, foreshadowing management
