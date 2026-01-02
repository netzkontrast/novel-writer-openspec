# Novel-Writer-OpenSpec

> A novel writing management tool based on the OpenSpec methodology

[![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)](https://github.com/wordflowlab/novel-writer-openspec)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](./LICENSE)

## 📖 Introduction

**Novel-Writer-OpenSpec** is a tool that applies the OpenSpec methodology to novel writing. By separating `specs/` (established specifications) from `changes/` (change proposals), it provides clear context and strict verification mechanisms for AI-assisted novel creation.

### Core Advantages

- ✅ **Clear Context Management**: AI clearly knows "existing settings" vs. "planned settings"
- ✅ **Strict Spec Format**: Requirements + Scenarios verifiable format
- ✅ **Automated Verification**: Automated format verification reduces character inconsistencies and setting conflicts
- ✅ **Structured Evolution**: Clearly manage setting evolution with ADDED/MODIFIED/REMOVED
- ✅ **AI Friendly**: Provides AI assistant integration instructions to improve writing efficiency

## 🚀 Quick Start

### Installation

```bash
npm install -g novelspec
```

Or local development:

```bash
git clone https://github.com/wordflowlab/novel-writer-openspec.git
cd novel-writer-openspec
npm install
npm link
```

### Create Your First Novel Project

```bash
# Initialize project
novelspec init my-novel

# Enter project directory
cd my-novel

# View project structure
tree -L 2 novelspec/
```

Output:
```
novelspec/
├── project.md       # Project conventions (creative principles, style guide)
├── AGENTS.md        # AI assistant work instructions
├── specs/           # Established specifications (Single Source of Truth)
│   ├── characters/
│   ├── worldbuilding/
│   └── outline/
└── changes/         # Change proposals
    └── archive/
```

### Create Proposal Using AI Assistant

Use slash commands in AI tools like Cursor/Claude/Windsurf:

```
/novelspec-proposal
```

AI will guide you to create the first change proposal (e.g., creating chapters 1-10).

### Validate Proposal

```bash
novelspec validate add-chapter-1-10
```

Output:
```
Change: add-chapter-1-10
──────────────────────────────────────────────────
Format Verification:
✓ proposal.md contains Why/What/Impact
✓ tasks.md uses task list format
✓ specs/outline/spec.md format is correct
✓ All Requirements have at least one Scenario

Verification Result: Passed
```

## 📚 Core Concepts

### specs/ - Established Specifications (Single Source of Truth)

Stores confirmed novel specifications:
- **characters/** - Character specs (protagonist, supporting characters, villains)
- **worldbuilding/** - Worldview specs (magic system, geography, factions)
- **outline/** - Story outline specs (completed chapter outlines)

### changes/ - Change Proposals

Manages chapters to be written and setting changes:
- Each change includes: `proposal.md`, `tasks.md`, `specs/` delta
- Start writing after verification passes
- Archive to `archive/` after completion

### Requirements + Scenarios Format

All specs use a verifiable format:

```markdown
### Requirement: Character Basic Setting
The protagonist SHALL have a clear identity background.

#### Scenario: Identity Information
- **WHEN** Protagonist appears or is mentioned
- **THEN** Name: Chen Fan
- **THEN** Age: 25 years old
- **THEN** Personality: Rational, introverted, kind but not a "Saint"
```

## 🛠️ CLI Commands

### `novelspec init <project-name>`

Initialize a new novel project.

```bash
novelspec init my-novel           # Create new project
novelspec init my-novel --here    # Initialize in current directory
```

### `novelspec list`

List changes or specs.

```bash
novelspec list                    # List active changes
novelspec list --archive          # List archived changes
novelspec list --specs            # List all specs
novelspec list --json             # JSON output
```

### `novelspec show <item-id>`

Show details of a change or spec.

```bash
novelspec show add-chapter-1-10                      # Show change details
novelspec show characters/protagonist --type spec    # Show spec details
novelspec show add-chapter-1-10 --json               # JSON output
```

### `novelspec validate [change-id]`

Validate the format of a change proposal.

```bash
novelspec validate                    # Validate all active changes
novelspec validate add-chapter-1-10   # Validate a single change
novelspec validate --strict           # Strict validation mode
novelspec validate --json             # JSON output
```

### `novelspec archive <change-id>`

Archive a completed change.

```bash
novelspec archive add-chapter-1-10    # Archive change
novelspec archive add-chapter-1-10 -y # Archive (skip confirmation)
```

### `novelspec --help`

View help information.

```bash
novelspec --help
novelspec init --help
novelspec validate --help
novelspec list --help
novelspec show --help
novelspec archive --help
```

## 🤖 AI Assistant Integration

Novel-Writer-OpenSpec automatically creates AI assistant integration instructions when initializing a project:

### Automatically Created Files

After running `novelspec init my-novel`, the following are created in the project:

- **`.cursor/commands/`** - Cursor slash command configuration
  - `novelspec-proposal.md` - Create proposal command
  - `novelspec-apply.md` - Execute writing command
  - `novelspec-archive.md` - Archive change command
- **`novelspec/AGENTS.md`** - Complete AI assistant work instructions

### Supported AI Tools

- **Cursor** - Automatically creates `.cursor/commands/`
- **Claude** - Refer to `novelspec/AGENTS.md`
- **Windsurf** - Refer to `novelspec/AGENTS.md`
- **Others** - Refer to `novelspec/AGENTS.md`

### AI Assistant Commands

#### `/novelspec-proposal` - Create Change Proposal

AI guides you to create a structured proposal:
1. Ask for creative intent (Chapter X-Y/Extend setting)
2. Generate `proposal.md`, `tasks.md`, `specs/`
3. Automatically run `novelspec validate`
4. Output verification results

#### `/novelspec-apply` - Execute Writing

AI writes chapters according to the proposal and task list:
1. Read `proposal.md`, `design.md`, `tasks.md`
2. Write based on the truth in `specs/`
3. Continuously verify each chapter
4. Mark tasks as completed

#### `/novelspec-archive` - Archive Change

(To be implemented in Phase 2)

## 📖 Workflow Example

### Complete Process of Writing Chapters 1-10

#### 1. Create Proposal

Use AI assistant:
```
/novelspec-proposal
```

AI asks:
```
Which chapter do you want to write? or what setting to extend?
```

Answer:
```
Write chapters 1-10, protagonist travels to a fantasy world, obtains a sign-in system, completes introductory cultivation
```

AI generates:
- `novelspec/changes/add-chapter-1-10/proposal.md`
- `novelspec/changes/add-chapter-1-10/tasks.md`
- `novelspec/changes/add-chapter-1-10/specs/outline/spec.md`
- `novelspec/changes/add-chapter-1-10/specs/characters/protagonist/spec.md`

#### 2. Validate Proposal

```bash
novelspec validate add-chapter-1-10 --strict
```

#### 3. Execute Writing

Use AI assistant:
```
/novelspec-apply
```

AI automatically:
- Reads all relevant specs
- Writes chapters in order of `tasks.md`
- Generates `chapters/volume-1/chapter-001.md` to `chapter-010.md`
- Continuously verifies each chapter

#### 4. Archive Change

(Will be supported in Phase 2)

```bash
novelspec archive add-chapter-1-10
```

## 🗂️ Project Structure

```
my-novel/
├── novelspec/                  # Spec management directory
│   ├── project.md              # Project conventions
│   ├── AGENTS.md               # AI assistant instructions
│   ├── specs/                  # Established specs (Single Source of Truth)
│   │   ├── characters/
│   │   │   ├── protagonist/spec.md
│   │   │   ├── heroine/spec.md
│   │   │   └── supporting/
│   │   ├── worldbuilding/
│   │   │   ├── magic-system/spec.md
│   │   │   ├── geography/spec.md
│   │   │   └── factions/spec.md
│   │   └── outline/spec.md
│   └── changes/                # Change proposals
│       ├── add-chapter-1-10/
│       │   ├── proposal.md
│       │   ├── tasks.md
│       │   └── specs/
│       └── archive/
├── chapters/                   # Chapter content (Generated artifacts)
│   ├── volume-1/
│   │   ├── chapter-001.md
│   │   ├── chapter-002.md
│   │   └── ...
│   └── volume-2/
└── docs/                       # Project documentation
    └── workflow-guide.md
```

## 📝 Spec Example

### Character Spec

```markdown
# novelspec/specs/characters/protagonist/spec.md

## Purpose
Complete spec definition for protagonist Chen Fan.

## Requirements

### Requirement: Basic Setting
The protagonist SHALL have a clear and consistent identity background.

#### Scenario: Identity Information
- **WHEN** Protagonist appears or is mentioned
- **THEN** Name: Chen Fan
- **THEN** Age: 25 years old
- **THEN** Personality: Rational, introverted, kind but not a "Saint"

### Requirement: Behavior Pattern
The protagonist SHALL exhibit consistent behavior patterns in different situations.

#### Scenario: Facing Danger
- **WHEN** Encountering life threat
- **THEN** Remain calm, rationally analyze the situation
- **THEN** Prioritize finding an escape route
```

### Change Proposal Example

```markdown
# novelspec/changes/add-chapter-11-20/proposal.md

## Why
Chapters 1-10 completed the protagonist's introduction and basic cultivation. Chapters 11-20 need to demonstrate the protagonist's strength and growth through the Sect Competition.

## What Changes
- Add outline specs for chapters 11-20
- Protagonist level from Qi Refining Level 7 → Qi Refining Level 9
- Add supporting character specs: Genius disciple Li Jian, Mysterious mentor Elder Yun

## Impact
- **Impacted Specs**:
  - `specs/outline/spec.md` (Add 10 chapters)
  - `specs/characters/protagonist/spec.md` (Level update)
  - `specs/characters/li-jian/spec.md` (Added)
```

## 🔧 Development

### Local Development

```bash
# Clone repository
git clone https://github.com/wordflowlab/novel-writer-openspec.git
cd novel-writer-openspec

# Install dependencies
npm install

# Build
npm run build

# Link locally
npm link

# Test
novelspec --version
```

### Directory Structure

```
novel-writer-openspec/
├── src/                    # Source code
│   ├── cli.ts              # CLI entry
│   ├── commands/           # CLI commands
│   │   ├── init.ts
│   │   └── validate.ts
│   ├── core/               # Core modules
│   │   ├── parser.ts
│   │   ├── validator.ts
│   │   └── template-manager.ts
│   └── utils/              # Utility functions
│       └── file-ops.ts
├── templates/              # Template files
│   ├── project.md.template
│   ├── AGENTS.md.template
│   ├── characters/
│   ├── worldbuilding/
│   └── outline/
├── docs/                   # Documentation
│   ├── PRD.md
│   └── workflow-guide.md
├── openspec/               # OpenSpec specs (Project itself)
│   ├── project.md
│   ├── specs/
│   └── changes/
├── package.json
├── tsconfig.json
└── README.md
```

## 📚 Documentation

- [PRD - Product Requirement Document](./docs/PRD.md)
- [Workflow Guide](./docs/workflow-guide.md)
- [AI Assistant Instructions Example](./templates/AGENTS.md.template)

## 🤝 Contribution

Contributions are welcome! Please check [CONTRIBUTING.md](./CONTRIBUTING.md).

## 📄 License

MIT License - See [LICENSE](./LICENSE)

## 🔗 Related Projects

- [OpenSpec](https://github.com/Fission-AI/OpenSpec) - Original OpenSpec methodology
- [Novel-Writer](https://github.com/wordflowlab/novel-writer) - Novel writing tool based on Spec-Kit

## 📮 Contact

- Issues: [GitHub Issues](https://github.com/wordflowlab/novel-writer-openspec/issues)
- Email: [your-email@example.com](mailto:your-email@example.com)

---

**Happy Writing! 📝✨**


## 🏗️ Project Analysis & Critique

### Functionality Summary

**Novel-Writer-OpenSpec** adapts the **OpenSpec methodology**—traditionally used for software engineering—to the domain of **novel writing**.
- **Core Concept**: Separates the "Truth" (Specifications in `specs/`) from "Proposals" (Changes in `changes/`).
- **Workflow**: Writers create a "Change Proposal" (e.g., "Add Chapter 10"), which includes a rationale (`proposal.md`), tasks (`tasks.md`), and updates to world/character specs.
- **Validation**: Strict enforcement of a `Requirement` + `Scenario` format ensures consistency and helps prevent "plot holes."
- **AI-First**: Designed as a backend for AI writing assistants, providing clear context and verification steps to minimize hallucinations.

### Critical Evaluation

#### Strengths
*   **Structured Creativity**: applying CI/CD concepts to storytelling is a powerful innovation for managing complex narratives.
*   **AI Integration**: The inclusion of `AGENTS.md` and structured JSON outputs makes it an excellent tool for AI agents.
*   **Clean Architecture**: The separation of Parser (`src/core/parser.ts`), Validator (`src/core/validator.ts`), and CLI logic is clean and maintainable.

#### Weaknesses (Critical)
*   **Fragile Parsing**: The regex-based parser (`src/core/parser.ts`) relies on exact string matching (e.g., specific whitespace). It is brittle and likely to break with minor user formatting errors.
*   **Zero Test Coverage**: The repository currently lacks a test suite. `npm test` fails. This is a significant risk for a tool that claims to provide "strict validation."
*   **Shallow Validation**: Validation checks syntax (e.g., headers exist) but lacks semantic depth (e.g., checking if a removed character is referenced in a new chapter).

### Relevance Assessment

*   **High Relevance (Core)**:
    *   `src/core/parser.ts`: The heart of the system. Needs refactoring to be more robust.
    *   `src/core/validator.ts`: The brain. Currently too simple; needs to incorporate "Best Practices."
    *   `openspec/AGENTS.md`: The "Constitution." Contains logic that should be extracted into code.
*   **Low Relevance (Peripheral)**:
    *   `src/utils/`: Generic helpers.
    *   `novelspec/`: Example content (useful mainly for testing).

### Refactor Strategy: Extracting "Best Ideas"

The "Best Ideas" for this project are currently trapped in text form within **`openspec/AGENTS.md`** under the "Best Practices" section. The goal of a refactor should be to **codify these text rules into software logic**.

1.  **Extract "Simplicity" Rules**:
    *   *Source*: `AGENTS.md` advises "Default to <100 lines of new code".
    *   *Refactor*: Update `validator.ts` to warn if a `spec.md` file exceeds a certain complexity or length.

2.  **Extract "Atomic Changes" Rules**:
    *   *Source*: `AGENTS.md` states "Change must have at least one delta".
    *   *Refactor*: Ensure `validator.ts` strictly fails if the `specs/` folder in a change is empty.

3.  **Extract "Strict Formatting" Rules**:
    *   *Source*: `AGENTS.md` details strict `#### Scenario:` usage.
    *   *Refactor*: Move the fragile regex logic from `parser.ts` into a dedicated **Grammar Definition** or AST parser to make these rules robust and reusable.
