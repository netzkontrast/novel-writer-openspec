# Novel Writing Workflow Guidance

This document provides workflow guidance for AI assistants in novel writing, based on the OpenSpec methodology.

## Overview

This project uses the OpenSpec methodology for novel writing management. Core workflow:

```
Specify → Clarify → Plan → Write → Analyze
```

**OpenSpec Methodology Foundation**: Refer to `@/AGENTS.md` in the project root to understand how to use the OpenSpec framework (change proposals, spec management, etc.).

---

## 🎯 Clarify Specs (Clarification) - Parallel Path Display Mode

When there are ambiguous decision points or `[Need Clarification]` tags in the specs, use the following clarification process.

### Trigger Timing

- `[Need Clarification]` tag exists in spec files
- User explicitly requests clarification
- Key ambiguities detected (creative positioning, character design, narrative strategy, etc.)
- Before starting formal creative planning (plan)

### Core Design: Parallel Path Display

**DO NOT** predict a single path (avoid guiding users, leading to homogeneity)
**INSTEAD** display 2-3 parallel paths + explicitly encourage innovative mix-and-match

### 7 Major Categories of Clarification

Scan spec files to identify ambiguities in the following categories:

1. **Creative Positioning**: Target reader age group, work positioning (commercial/literary), expected scale
2. **Worldbuilding**: Era background, world rules, geographical scope
3. **Character Design**: Protagonist personality tone, growth curve, supporting character positioning
4. **Narrative Strategy**: Perspective choice, timeline structure, narrative pacing
5. **Plot Core**: Core conflict type, main storyline goal, ending tendency
6. **Style Tone**: Writing style choice, descriptive focus, emotional tone
7. **Creative Constraints**: Sensitive content handling, value orientation, update plan

### Path Generation Principles

Generate 2-3 parallel paths for each clarification task:

#### Path A: Classic Route

- Infer the most matching classic path based on clues in specs
- Choose combinations fully verified by the market
- Clearly mark as "Classic Route"
- Provide reference work examples

#### Path B: Differentiated Route

- Second choice contrasting with Path A
- Provide a different creative direction
- Mark as "Deep Route" or "Differentiated Route"
- Explain advantages and challenges

#### Path C: Innovative Mix-and-Match Route

- **Explicitly encourage breaking conventions**
- Provide counter-intuitive combination examples
- Mark as "Innovative Route"
- Emphasize "Any combination is possible to succeed"
- Do not provide fixed answer combinations (completely open)

### Question Design Principles

Each question (max 5) should include:

1. **Question Context** (💬): Explain why this question is asked
2. **Core Question**: Clear question statement
3. **Option Labels**:
   - **Path Label**: [Path A] [Path B] [Path C]
   - **Commonness Label**:
     - ⚠️ Most Common (Used by 80% of works)
     - 📊 Common (Around 50%)
     - ⭐ Innovative Point (<20% but interesting)
     - 🎨 Completely Innovative

Example Question Format:

```markdown
### Question 1: Target Reader Age Group?
💬 This is a core positioning question that will affect the overall style and narrative strategy.

| Option | Description | Path Label | Commonness |
|------|------|----------|--------|
| a | 18-25 years old (Student group) - Like hot-blooded, growth, idealism | [Path A] | ⚠️ Most Common |
| b | 26-35 years old (Professionals) - Focus on reality, strategy, human complexity | [Path B] | 📊 Common |
| c | 36-45 years old (Mature readers) - Pursue depth, literary quality, emotional resonance | | ⭐ Innovative Point |
| d | Cross-age (General) - Adjust narrative levels, diverse expression | [Path C] | 🎨 Innovative |
```

### Output Format Key Points

1. **Parallel Path Analysis** (Top)
   - Display 2-3 complete paths
   - Each path includes: Suitable crowd, core features, answer combination, advantages, disadvantages, reference works

2. **Detailed Question List**
   - Each question includes: Context explanation, options, path labels, commonness

3. **Innovative Examples**
   - Provide 3-5 unconventional combination examples
   - Explicitly state "Support all possible combinations"

4. **Multiple Answer Methods**
   - Path Shortcut: `Path A` or `A`
   - Concise Combination: `1 a 2 b 3 c`
   - Mixed Mode: `1 a 2 Path B 3 c`
   - Natural Language: Compatible mode

### Batch Clarification Mode (Key Feature)

**Output all questions at once**, user **answers at once**, significantly reducing interaction turns:

```
AI: Output 2-3 path analyses + 5 questions
User: Answer at once, e.g., "1 a 2 b 3 c 4 d 5 a" or "Path A"
AI: Parse answer, update specs, output report
```

### Answer Parsing Logic

Supported input formats:

- `Path A` / `A` / `path-a` → Apply answer combination of the entire path
- `1 a 2 b 3 c 4 d 5 a` → Custom per question
- `1a 2b 3c` → Compact format
- `1 a 2 Path B 3 c` → Mixed mode (Partial path + Partial custom)

### Spec Update

Add `## Clarification Record` section to spec file:

```markdown
## Clarification Record

### Clarification Session 2025-01-24

**Selected Path**: Innovative Mix-and-Match (Partial Path A + Partial Custom) ⭐

**Specific Answers**:
1. Target Reader: 18-25 years old (Student group) [Option a]
2. Story Type: Workplace Strategy Type [Option c] ⭐ Innovative Combination!
3. Protagonist Start: Loser Counterattack [Option a]
4. Growth System: Medium Complexity [Option b]
5. Mainline Rhythm: Moderate Tension [Option c]

**Innovation Explanation**:
Selected unconventional combination of "Student Reader + Workplace Strategy", can create a campus politics novel,
This is a rare but potential direction.

**Updates to Spec**:
- Update "Target Reader Persona" to 18-25 years old student group
- Update "Market Positioning" to Workplace Strategy Type (Campus Background)
- Update "Core Conflict" to combination of power game and growth
```

### Key Expressions Encouraging Innovation

During clarification, must include the following expressions encouraging innovation:

- "**We support all possible combinations!** Do not be limited by paths, innovation often comes from breaking rules."
- "Any unconventional combination has the potential to succeed!"
- "Uniqueness often comes from breaking rules, stick to your creativity!"
- Provide specific innovative combination examples (e.g., "Student + Strategy = Campus Politics Novel")

### CLI Command Usage

```bash
# Comprehensive Clarification
novelspec clarify

# Focus on specific domain (Future feature)
novelspec clarify characters    # Focus on character design only
novelspec clarify worldbuilding # Focus on worldbuilding only
```

---

## Important Principles

1. **Diversity Protection**: Avoid homogeneity caused by single prediction through parallel path display.
2. **Encourage Innovation**: Explicitly encourage unconventional combinations, mark innovative points.
3. **Batch Efficiency**: Output questions at once, collect answers at once, reduce token consumption.
4. **Flexible Format**: Support multiple answer input formats, lower user threshold.
5. **Complete Record**: All clarification decisions are recorded in spec files, traceable.

---

## Next Steps

After clarification is complete, it is recommended to:

- Run `novelspec validate` to verify spec integrity
- Enter creative planning stage (plan)
- Start specific chapter writing

---

## Resources

- **OpenSpec Methodology**: `@/AGENTS.md`
- **Project Conventions**: `@novelspec/project.md`
- **CLI Commands**: Run `novelspec --help` to view all commands
- **Slash Commands**: `/.claude/commands/clarify.md`
