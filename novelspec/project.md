# novel-writer-openspec Project Conventions

## Project Overview

A novel writing management tool based on the OpenSpec methodology, providing structured spec management and creative workflow.

## Core Philosophy

1. **Spec-Driven Creation**: Define specs first, then create.
2. **Progressive Clarification**: From vague to clear, gradually clarifying creative direction.
3. **Diversity Protection**: Avoid homogeneity, encourage innovative combinations.
4. **Version Management**: Manage spec changes using OpenSpec methodology.

## Directory Structure

```
novelspec/
├── AGENTS.md           # Novel creation workflow guide (AI Assistant specific)
├── project.md          # This file: Project conventions
├── specs/              # Confirmed novel specs
│   ├── characters/     # Character specs
│   │   ├── protagonist/
│   │   │   └── spec.md
│   │   └── supporting/
│   │       └── spec.md
│   ├── worldbuilding/  # Worldbuilding specs
│   │   ├── magic-system/
│   │   │   └── spec.md
│   │   └── geography/
│   │       └── spec.md
│   ├── outline/        # Outline specs
│   │   └── chapter-plan/
│   │       └── spec.md
│   └── knowledge/      # Knowledge base
│       ├── character-profiles/
│       └── world-settings/
├── changes/            # Pending change proposals
│   ├── add-character-arc/
│   │   ├── proposal.md
│   │   ├── tasks.md
│   │   └── specs/
│   │       └── characters/protagonist/spec.md
│   └── archive/        # Archived changes
└── tracking/           # Creation progress tracking (JSON format)
    ├── plot-tracker.json
    ├── timeline.json
    └── relationships.json
```

## File Naming Conventions

### Spec Files (specs/)

- **Directory Name**: kebab-case, e.g., `character-protagonist`, `magic-system`
- **File Name**: Unified as `spec.md`
- **Path Example**: `specs/characters/protagonist/spec.md`

### Change ID (changes/)

- **Format**: Verb-led, kebab-case
- **Verb Choices**:
  - `add-` - Add feature or content
  - `update-` - Modify existing content
  - `remove-` - Remove content
  - `refactor-` - Refactor structure
  - `fix-` - Fix error
- **Examples**:
  - `add-character-arc`
  - `update-worldbuilding-system`
  - `refactor-outline-structure`

### Knowledge Base Files (knowledge/)

- **Character Profiles**: `character-profiles/{name}.md`
- **World Settings**: `world-settings/{topic}.md`
- **Naming Rule**: kebab-case, Pinyin or English

### Tracking Files (tracking/)

- **Format**: JSON
- **Naming**: kebab-case, e.g., `plot-tracker.json`
- **Update Frequency**: Update after each chapter creation

## Spec Format Conventions

### Requirements + Scenarios Format

All spec files use OpenSpec's Requirements + Scenarios format:

```markdown
## Requirements

### Requirement: Protagonist Basic Setting
The protagonist SHALL have clear background, personality traits, and core motivation.

#### Scenario: Protagonist Background Setting
- **WHEN** Creating protagonist spec
- **THEN** MUST specify protagonist's age, profession, family background
- **AND** Personality traits should include at least 3 core features
- **AND** Core motivation should be clear and reasonable

### Requirement: Protagonist Growth Trajectory
The protagonist SHALL have a clear growth trajectory, from initial state to final state.

#### Scenario: Growth Stage Division
- **WHEN** Planning protagonist growth
- **THEN** Should be divided into at least 3 growth stages
- **AND** Each stage should have clear trigger events
- **AND** Growth should be reflected in changes of ability, mindset, or values
```

### Change Proposal Format

Refer to OpenSpec standard:

- `proposal.md` - Change proposal (Why, What, Impact)
- `tasks.md` - Implementation task list (Checklist)
- `specs/{capability}/spec.md` - Spec delta (ADDED/MODIFIED/REMOVED)

## Creative Workflow

### Standard Workflow

1. **Specify**
   - Create initial specs using templates
   - Support Level 1-4 progressive specs

2. **Clarify**
   - Use `novelspec clarify` command
   - Batch clarification mode (Parallel path display)
   - Complete all decisions at once

3. **Plan**
   - Formulate chapter outline
   - Assign writing tasks

4. **Write**
   - Create content according to specs
   - Use tracking system to record progress

5. **Analyze**
   - Verify conformity to specs
   - Check consistency

### Change Management Workflow

Refer to OpenSpec standard three-stage workflow:

1. **Creating Changes** - Create change proposal
2. **Implementing Changes** - Implement change
3. **Archiving Changes** - Archive change

## Template Library

### Available Templates

1. **Character Templates**:
   - `character-protagonist` - Protagonist spec template
   - `character-supporting` - Supporting character spec template
   - `character-villain` - Villain spec template

2. **Worldbuilding Templates**:
   - `worldbuilding-xuanhuan` - Fantasy worldview template
   - `worldbuilding-wuxia` - Wuxia worldview template
   - `worldbuilding-urban` - Urban worldview template

3. **Outline Templates**:
   - `outline-chapter` - Chapter outline template
   - `outline-complete` - Complete outline template

4. **Knowledge Templates**:
   - `knowledge-world-setting` - World setting template
   - `knowledge-character-profile` - Character profile template

5. **Tracking Templates**:
   - `tracking-plot-tracker` - Plot tracker template
   - `tracking-timeline` - Timeline template
   - `tracking-relationships` - Relationship network template

### Using Templates

```bash
# CLI command (Future feature)
novelspec create character --template protagonist

# Or manually copy template
# Template location: src/core/templates/novel-templates/
```

## Validation Rules

### Spec Validation

```bash
# Validate single change
novelspec validate add-character-arc

# Validate all changes
novelspec validate

# Strict validation
novelspec validate --strict
```

### Common Validation Failures

1. **Missing Scenario**: Each Requirement needs at least one Scenario
2. **Format Error**: Scenario must use `WHEN/THEN/AND` format
3. **Missing Descriptive Text**: Requirement must have descriptive text below

## Best Practices

### Spec Writing

1. **Start Small**: Use Level 1-2 progressive specs, expand gradually
2. **Keep Concise**: Requirement should focus on single concern
3. **Verifiable**: Scenario should be testable and verifiable
4. **Avoid Premature Detail**: Do not over-detail in initial specs

### Clarification Decisions

1. **Use Batch Mode**: Answer all questions at once, reduce interaction
2. **Encourage Innovation**: Do not be bound by common paths
3. **Record Reasoning**: Clarification records should include decision reasoning

### Version Management

1. **Small Steps**: Frequent small changes are better than large-scale refactoring
2. **Clear Naming**: Change ID should clearly express intent
3. **Archive Promptly**: Archive immediately after completion to keep changes/ directory clean

## Tool Support

### CLI Commands

```bash
novelspec init <project-name>    # Initialize project
novelspec clarify                 # Clarify spec
novelspec validate                # Validate spec
novelspec list                    # List changes
novelspec list --specs            # List specs
novelspec show <item-id>          # Show details
novelspec archive <change-id>     # Archive change
```

### AI Assistant Guidance

- **AGENTS.md** - Complete AI workflow guidance
- **Claude Code Slash Command** - `.claude/commands/clarify.md`

## Resources

- **OpenSpec Documentation**: https://github.com/Fission-AI/OpenSpec
- **Project README**: `@/README.md`
- **AI Workflow Guidance**: `@novelspec/AGENTS.md`
