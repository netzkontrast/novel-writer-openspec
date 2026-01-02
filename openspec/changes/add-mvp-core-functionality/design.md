# Design: MVP Core Functionality

## Context

Novel-Writer-OpenSpec is a new tool applying the OpenSpec methodology to novel writing. The core challenges are:
- Adapting the OpenSpec `specs/changes` structure to novel writing scenarios
- Providing a simple and easy-to-use CLI and AI assistant integration
- Ensuring the validator can accurately identify novel spec format errors

**Constraints**:
- Use `novelspec` namespace to avoid conflict with OpenSpec
- MVP phase focuses on format validation, semantic validation reserved for Phase 2
- Templates need to adapt to Chinese web novel writing habits (though the tool itself is international)

**Stakeholders**:
- AI-assisted web novel authors (Primary Users)
- Long-form novel authors needing to manage complex settings (Secondary Users)

## Goals / Non-Goals

**Goals**:
- ✅ Users can run `novelspec init my-novel` to create a novel project
- ✅ Users can run `novelspec validate <change>` to check for format errors
- ✅ AI can create proposals via `/novelspec-proposal`
- ✅ Templates include novel-specific spec examples (characters, worldbuilding, outline)
- ✅ README provides a quick start guide

**Non-Goals**:
- ❌ Semantic validation (character behavior consistency, setting conflict detection) - Phase 2
- ❌ Cross-chapter validation (timeline, foreshadowing tracking) - Phase 3
- ❌ Archive functionality - Phase 2
- ❌ VS Code extension or Web interface - Phase 4
- ❌ Automatic chapter generation (done by AI, tool only provides validation)

## Technical Decisions

### Decision 1: CLI Framework Selection

**Choice**: Use Commander.js

**Reason**:
- Lightweight and mature
- Supports subcommands, options, help generation
- Consistent with OpenSpec CLI

**Alternatives**:
- Yargs: More powerful but heavier
- Hand-written CLI: Flexible but requires more work

### Decision 2: File Parsing Strategy

**Choice**: Custom Markdown Parser (Regex + State Machine based)

**Reason**:
- Requirements + Scenarios format is specific, general Markdown parsers are overly complex
- Need to precisely identify `### Requirement:` and `#### Scenario:` structures
- Lightweight, no external dependencies

**Implementation**:
```typescript
interface Spec {
  purpose: string;
  requirements: Requirement[];
}

interface Requirement {
  name: string;
  level: 'SHALL' | 'MUST' | 'MAY';
  scenarios: Scenario[];
}

interface Scenario {
  name: string;
  conditions: string[];  // WHEN/THEN lines
}
```

**Alternatives**:
- unified + remark: Heavyweight, but more robust (consider if complex Markdown features are needed)

### Decision 3: Template Variable Replacement

**Choice**: Simple string replacement (`{{VARIABLE}}`)

**Reason**:
- Templates are simple, no complex logic needed
- User-friendly, easy to understand

**Implementation**:
```typescript
function applyTemplate(template: string, vars: Record<string, string>): string {
  return template.replace(/\{\{(\w+)\}\}/g, (_, key) => vars[key] || '');
}
```

**Alternatives**:
- Handlebars/Mustache: Powerful but over-engineered

### Decision 4: Validation Error Report Format

**Choice**: Clear text output + Optional JSON format

**Text Format**:
```
Format Verification:
✓ proposal.md contains Why/What/Impact
✗ tasks.md missing task list format
  → Must use - [ ] or - [x]

Verification Result: 1 error
```

**JSON Format** (`--json` option):
```json
{
  "valid": false,
  "errors": [
    {
      "file": "tasks.md",
      "type": "format",
      "message": "Missing task list format"
    }
  ]
}
```

**Reason**:
- Text output is human-friendly
- JSON output supports CI/CD integration

### Decision 5: Directory Structure Specification

**Choice**: Strictly follow OpenSpec structure, only adjust namespace

```
my-novel/
├── novelspec/              # Core spec directory
│   ├── project.md          # Project conventions (including creative principles)
│   ├── AGENTS.md           # AI assistant instructions
│   ├── specs/              # Established specs
│   │   ├── characters/
│   │   ├── worldbuilding/
│   │   └── outline/
│   └── changes/            # Change proposals
│       └── archive/
├── chapters/               # Chapter content (generated artifacts)
└── docs/                   # Project documentation
```

**Reason**:
- Consistent with OpenSpec, reducing learning cost
- `novelspec/` namespace clearly identifies purpose
- `chapters/` separates content from specs

### Decision 6: AI Assistant Integration Method

**Choice**: Provide `novelspec/AGENTS.md` instruction file + example slash command configuration

**AGENTS.md Content**:
- When to create proposals (new chapters, extending settings)
- How to create proposal/tasks/specs structure
- How to run validate
- Requirements + Scenarios format specification

**Slash Command Example** (`.cursor/commands/novelspec-proposal.md`):
```yaml
name: /novelspec-proposal
description: Create novel spec proposal
steps:
  1. Ask user for creative intent
  2. Create changes/<id>/ structure
  3. Generate proposal.md, tasks.md, specs/
  4. Run novelspec validate
```

**Reason**:
- Tool-agnostic (supports Claude, Cursor, Windsurf, etc.)
- Clear workflow guidance

## Data Model

### Core Data Structures

```typescript
// Spec File
interface SpecFile {
  path: string;              // File path
  purpose: string;           // ## Purpose content
  requirements: Requirement[];
}

// Requirement
interface Requirement {
  name: string;              // Requirement name
  level: 'SHALL' | 'MUST' | 'MAY';
  description: string;       // Requirement description
  scenarios: Scenario[];
}

// Scenario
interface Scenario {
  name: string;              // Scenario name
  conditions: {
    type: 'WHEN' | 'THEN';
    text: string;
  }[];
}

// Change Proposal
interface Change {
  id: string;                // Change ID
  proposalPath: string;      // proposal.md path
  tasksPath: string;         // tasks.md path
  designPath?: string;       // design.md path (optional)
  deltaSpecs: DeltaSpec[];   // Spec deltas
}

// Spec Delta
interface DeltaSpec {
  capability: string;        // Capability name (e.g., 'characters/protagonist')
  operations: {
    type: 'ADDED' | 'MODIFIED' | 'REMOVED' | 'RENAMED';
    requirements: Requirement[];
  }[];
}

// Validation Result
interface ValidationResult {
  valid: boolean;
  errors: ValidationError[];
  warnings: ValidationWarning[];
}

interface ValidationError {
  file: string;
  line?: number;
  type: 'format' | 'semantic' | 'cross-chapter';
  message: string;
  suggestion?: string;
}
```

## Risks / Trade-offs

### Risk 1: Custom Parser Fragility

**Risk**: Regex parsing may not handle edge cases

**Mitigation**:
- Strict format requirements, reducing variability
- Extensive test fixtures covering common and edge cases
- Clear error messages to help users correct

**Trade-off**: Simplicity vs Robustness (Prioritize simplicity in MVP phase)

### Risk 2: Templates Not Adapting to User Needs

**Risk**: Default templates may not fit all novel types

**Mitigation**:
- Provide multiple example templates (Fantasy, Wuxia, Urban, Sci-Fi)
- Users can customize project.md and spec.md templates
- Documentation explaining how to adjust templates

**Trade-off**: Universality vs Specialization (MVP focuses on Fantasy type)

### Risk 3: Validation False Positives

**Risk**: Overly strict validation may flag legal content

**Mitigation**:
- Provide `--strict` and non-strict modes
- Clear documentation on format requirements
- Collect user feedback for continuous optimization

**Trade-off**: Strictness vs Flexibility (Default non-strict, optional strict)

## Migration Plan

No migration needed (New projects)

## Testing Strategy

### Unit Tests
- Parser: Test Requirements/Scenarios parsing
- Validator: Test format validation rules
- Template Manager: Test variable replacement

### Integration Tests
- CLI Commands: Test `init` and `validate` end-to-end
- Real Fixtures: Test with complete novel spec files

### Manual Testing
- Use AI assistant to create proposals
- Verify error message clarity
- Check generated project structure

## Open Questions

1. **Q**: Need to support multiple languages (English, Chinese)?
   **A**: MVP focuses on Chinese (as per original context), but code design considers internationalization. (Note: Translating documentation to English as part of this task).

2. **Q**: Need configuration file (`.novelspecrc`)?
   **A**: Not needed in MVP, use `novelspec/project.md` as configuration.

3. **Q**: Does validator need plugin extension support?
   **A**: Not needed in Phase 1, consider in Phase 3.
