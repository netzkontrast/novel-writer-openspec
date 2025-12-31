# Novel-Writer-OpenSpec Product Requirement Document (PRD)

> Version: 1.0
> Date: 2025-01-22
> Status: Draft

## Documentation Overview

This document defines the core requirements and technical specifications for the **Novel-Writer-OpenSpec** product. This product draws on the OpenSpec methodology, applying the dual-track structure of specs/ (truth) + changes/ (proposals) to the field of novel writing, enhancing the efficiency and quality of AI-assisted creation through structured management and automated validation.

---

## I. Product Overview

### 1.1 Product Positioning

**Novel-Writer-OpenSpec** is a novel writing management tool based on the core concepts of the OpenSpec methodology. Through the separated management of `specs/` (established truth) and `changes/` (change proposals), it provides clear context and strict verification mechanisms for AI-assisted novel creation.

**Relationship with OpenSpec**:
- **Concept Adoption**: Dual-track structure of specs/ (truth) + changes/ (proposals)
- **Independent Tool**: Uses `novelspec` command, independent namespace, avoids conflict with OpenSpec
- **Customization**: Optimized spec format, validation rules, and workflow for novel writing

### 1.2 Core Value Proposition

Utilizing the three major advantages of the OpenSpec methodology to solve core pain points in AI-assisted novel creation:

#### 1. Clear Context Management

**Problem**: AI easily confuses "existing settings" with "planned settings"

**Solution**:
- `novelspec/specs/` stores established settings (characters, worldbuilding, outline)
- `novelspec/changes/` manages chapters to be written and setting changes
- AI clearly knows "current truth" and "work tasks"

**Effect**: AI understanding cost reduced by 50%, fewer deviations from specs

#### 2. Strict Spec Format

**Problem**: AI-generated content easily deviates from specs, hard to verify

**Solution**:
- Uses Requirements + Scenarios format to make specs verifiable
- SHALL/MUST keywords clarify constraint strength
- ADDED/MODIFIED/REMOVED clearly manage setting evolution

**Effect**: Specs can be automatically parsed and validated, reducing character inconsistencies and setting conflicts

#### 3. Automated Validation Mechanism

**Problem**: Consistency checks rely on manual or subjective AI judgment

**Solution**:
- `novelspec validate` automatically checks consistency
- Instant feedback prevents error accumulation
- Structured validation covers dimensions like characters, worldbuilding, plot, etc.

**Effect**: Validation efficiency increased by 10x, quality more stable

### 1.3 Target Users

- **Primary Users**: Web novel authors using AI assistance
- **Secondary Users**: Long-form novel authors needing to manage complex settings
- **Potential Users**: Creative teams valuing consistency and quality control

### 1.4 Core Problems & Solutions

| Creative Pain Point | Novel-Writer-OpenSpec Solution |
|---------|-------------------------------|
| AI confuses existing vs. planned settings | `specs/` (truth) vs `changes/` (task) separation |
| AI generated content deviates from specs | Requirements + Scenarios strict constraints |
| Hard to trace "why changed like this" | `proposal.md` clarifies change intent |
| Consistency check relies on manual work | `novelspec validate` automated validation |
| Setting evolution hard to manage | ADDED/MODIFIED/REMOVED incremental management |
| Multi-version outline chaos | specs/ single truth, archive/ retains history |

---

## II. System Architecture

### 2.1 Directory Structure Design

```
my-novel/
├── novelspec/                  # Novel spec management directory (Core)
│   ├── project.md              # Project conventions (Novel info, creative principles, style guide)
│   ├── AGENTS.md               # AI assistant work instructions
│   │
│   ├── specs/                  # Established novel specs (Single Source of Truth)
│   │   ├── characters/         # Character specs
│   │   │   ├── protagonist/
│   │   │   │   └── spec.md    # Protagonist complete spec
│   │   │   ├── heroine/
│   │   │   │   └── spec.md    # Heroine complete spec
│   │   │   └── supporting/
│   │   │       ├── mentor/spec.md
│   │   │       └── villain/spec.md
│   │   │
│   │   ├── worldbuilding/      # Worldbuilding specs
│   │   │   ├── magic-system/
│   │   │   │   └── spec.md    # Magic system spec
│   │   │   ├── geography/
│   │   │   │   └── spec.md    # Geography setting spec
│   │   │   ├── factions/
│   │   │   │   └── spec.md    # Faction organization spec
│   │   │   └── history/
│   │   │       └── spec.md    # Historical background spec
│   │   │
│   │   └── outline/            # Story outline spec
│   │       └── spec.md        # Established chapter outlines
│   │
│   └── changes/                # Changes to be written (Proposals)
│       ├── add-chapter-1-10/   # Proposal for writing chapters 1-10
│       │   ├── proposal.md     # Why write these 10 chapters
│       │   ├── design.md       # Technical plan (POV, pacing, foreshadowing)
│       │   ├── tasks.md        # Creation task list
│       │   └── specs/          # Spec deltas
│       │       ├── outline/spec.md              # Outline delta
│       │       ├── characters/protagonist/spec.md  # Protagonist development
│       │       └── worldbuilding/magic-system/spec.md
│       │
│       ├── add-chapter-11-20/  # Proposal for writing chapters 11-20
│       │   ├── proposal.md
│       │   ├── design.md
│       │   ├── tasks.md
│       │   └── specs/
│       │       └── outline/spec.md
│       │
│       ├── expand-magic-advanced/  # Magic expansion proposal
│       │   ├── proposal.md
│       │   ├── design.md
│       │   ├── tasks.md
│       │   └── specs/
│       │       └── worldbuilding/magic-system/spec.md
│       │
│       └── archive/            # Completed changes archive
│           ├── 2025-01-20-add-chapter-1-10/
│           └── 2025-01-21-expand-magic-basic/
│
├── chapters/                   # Actual chapter content (Generated artifacts)
│   ├── volume-1/
│   │   ├── chapter-001.md
│   │   ├── chapter-002.md
│   │   └── ...
│   └── volume-2/
│       ├── chapter-011.md
│       └── ...
│
└── docs/                       # Project documentation
    ├── PRD.md                  # This document
    └── workflow-guide.md       # Workflow guide
```

**Key Design Points**:

1. **Independent Namespace**: Use `novelspec/` instead of `openspec/` to avoid conflict
2. **No Constitution**: Creative principles integrated into `project.md` instead of a separate spec (OpenSpec has no constitution concept)
3. **Clear Separation**: `specs/` (truth) and `changes/` (proposals) strictly separated
4. **Structured Archiving**: `archive/` retains full history and change intent

### 2.2 Spec File Format

#### Project (Project Conventions)

```markdown
# novelspec/project.md

## Project Info
- Novel Name: "Star Dream"
- Genre: Fantasy Cultivation
- Target Word Count: 1 million words
- Estimated Volumes: 4 volumes

## Creative Principles

This project follows these core creative principles (AI must strictly adhere):

1. **Logical Consistency**: World settings once established must remain consistent, cannot be arbitrarily modified
2. **Character Consistency**: Character behavior must fit personality settings and growth trajectory
3. **Plot Reasonableness**: Plot development needs causal logic, no forced conflicts
4. **Unified Style**: Maintain unified narrative style and language characteristics

## Style Guide

- **Narrative Perspective**: Third-person limited perspective (mainly protagonist POV)
- **Language Style**: Modern vernacular, concise and brisk, avoid classical Chinese and internet slang
- **Chapter Length**: 3000-4000 words/chapter
- **Update Frequency**: Daily update, 1 chapter per day

## Quality Standards

- Each chapter must advance the plot or deepen character
- Dialogue fits character identity and personality
- Descriptions should be visual, avoiding mere listing
- Foreshadowing must be recorded and resolved

## Taboos

- ❌ No modern internet slang
- ❌ No arbitrary changes to magic system rules
- ❌ No character OOC (Out of Character)
- ❌ No undefined settings (characters, locations, skills, etc.)
```

**Note**:
- `project.md` carries creative principles and style guide, equivalent to novel-writer's constitution
- But this is not an independent spec, but a project-level convention
- AI reads this file as the highest constraint when working

#### Character (Character Spec)

```markdown
# novelspec/specs/characters/protagonist/spec.md

## Purpose
Complete spec definition for protagonist Chen Fan, basis for AI generating dialogue and behavior.

## Requirements

### Requirement: Basic Setting
Protagonist SHALL have a clear and consistent identity background.

#### Scenario: Identity Information
- **WHEN** Protagonist appears or is mentioned
- **THEN** Name: Chen Fan
- **THEN** Age: 25 years old
- **THEN** Profession: Programmer (Before crossing over)
- **THEN** Personality: Rational, introverted, kind but not a "Saint"
- **THEN** Traits: Strong logical thinking, not good at socializing, keen observation

### Requirement: Capability Growth
Protagonist MUST undergo verifiable growth trajectory.

#### Scenario: Volume 1 Growth (Chapters 1-30)
- **WHEN** Volume 1 completes
- **THEN** Cultivation Level: From ordinary person to Qi Refining Level 5
- **THEN** Personality Change: From timid to confident but still cautious
- **THEN** Relationship Change: From stranger to friend with heroine
- **THEN** Mastered Skills: Xuan Yuan Art, Wind Thunder Step

### Requirement: Behavior Pattern
Protagonist SHALL exhibit consistent behavior patterns in different situations.

#### Scenario: Facing Danger
- **WHEN** Encountering life threat
- **THEN** Remain calm, rationally analyze situation
- **THEN** Prioritize finding escape route
- **THEN** Do not easily fight hard against strong enemies
- **THEN** If with companions, prioritize protecting the weak

#### Scenario: Facing Temptation
- **WHEN** Someone offers powerful technique or treasure
- **THEN** Analyze risks and costs first
- **THEN** Ask about source and attached conditions
- **THEN** Cautiously judge whether to accept
- **THEN** Do not covet things falling from the sky

#### Scenario: Facing Conflict
- **WHEN** Conflict with others
- **THEN** Prioritize communication to solve
- **THEN** Avoid meaningless fights
- **THEN** Act decisively when necessary
- **THEN** Do not kill innocents indiscriminately

### Requirement: Dialogue Style
Protagonist's dialogue SHALL fit their identity and personality.

#### Scenario: Daily Dialogue
- **WHEN** Talking with peers or juniors
- **THEN** Peaceful tone, concise wording
- **THEN** No nonsense, substantive speech
- **THEN** Occasionally show programmer-style logical thinking

#### Scenario: Talking to Stronger
- **WHEN** Talking with seniors or strong people
- **THEN** Respectful but not subservient
- **THEN** Cautious wording, avoid offense
- **THEN** Do not retreat when adhering to principles
```

#### Worldbuilding (Worldview Spec)

```markdown
# novelspec/specs/worldbuilding/magic-system/spec.md

## Purpose
Define cultivation system and magic rules of this world, basis for AI describing relevant scenes.

## Requirements

### Requirement: Cultivation Level System
Cultivation system MUST be clear and consistent.

#### Scenario: Level Division
- **WHEN** Mentioning cultivation levels
- **THEN** Use the following system:
  - Qi Refining Stage (Levels 1-9)
  - Foundation Establishment Stage (Early, Mid, Late)
  - Golden Core Stage (Early, Mid, Late)
  - Nascent Soul Stage (Early, Mid, Late)
  - Spirit Severing Stage (Early, Mid, Late)

### Requirement: Level Gap Combat Power
Combat power gap between different levels SHALL be reasonable.

#### Scenario: Cross-level Combat Limit
- **WHEN** Character fights across levels
- **THEN** At most cross 2 small levels (e.g., Qi Refining 3 vs 5)
- **THEN** Need special conditions (Technique, Treasure, Environment advantage)
- **THEN** Crossing major realms (e.g., Qi Refining vs Foundation Establishment) almost impossible

### Requirement: Sign-in System Rules
Protagonist's sign-in system MUST follow fixed rules.

#### Scenario: Sign-in Mechanism
- **WHEN** Protagonist signs in
- **THEN** Only once per day
- **THEN** Different locations have different rewards
- **THEN** Special locations have better rewards (Sect forbidden area, ruins, etc.)
- **THEN** Reward range: Techniques, Pills, Treasures, Spirit Stones

#### Scenario: Sign-in Reward Balance
- **WHEN** Obtaining sign-in reward
- **THEN** Must not be too overpowered (e.g., directly breaking through major realm)
- **THEN** Need protagonist subsequent cultivation to digest
- **THEN** Maintain reasonable growth curve
```

#### Outline (Outline Spec)

```markdown
# novelspec/specs/outline/spec.md

## Purpose
Established part of story outline, basis for AI advancing plot.

## Requirements

### Requirement: Chapter 1 - Awakening
Chapter 1 SHALL establish worldview and protagonist settings.

#### Scenario: Opening Setting
- **WHEN** Chapter 1 starts
- **THEN** Protagonist Chen Fan travels to fantasy world
- **THEN** Discovers obtaining sign-in system
- **THEN** Initially understand cultivation system
- **THEN** Plant foreshadowing: System origin mysterious, will be revealed in future

#### Scenario: Worldview Display
- **WHEN** Chapter 1 in progress
- **THEN** Introduce protagonist location: Qingyun Sect Outer Gate
- **THEN** Show sect basic structure
- **THEN** Hint at cruelty of cultivation world

### Requirement: Chapter 2 - Exploring System
Chapter 2 SHALL demonstrate system capabilities.

#### Scenario: First Sign-in
- **WHEN** Protagonist uses system for first time
- **THEN** Sign-in location: Sect Square
- **THEN** Obtain reward: Basic technique "Xuan Yuan Art"
- **THEN** Understand sign-in rules (Once daily)
- **THEN** Start cultivation

#### Scenario: First Cultivation
- **WHEN** Protagonist cultivates Xuan Yuan Art
- **THEN** Show cultivation process
- **THEN** Breakthrough to Qi Refining Level 1
- **THEN** Feel strength improvement

### Requirement: Chapter 3 - First Try
Chapter 3 SHALL initially demonstrate protagonist strength.

#### Scenario: Encounter Trouble
- **WHEN** Chapter 3
- **THEN** Protagonist encounters bullying outer sect senior brother
- **THEN** Forced to fight
- **THEN** Use Xuan Yuan Art to repel opponent
- **THEN** Attract attention, plant foreshadowing for subsequent plot
```

#### Change Delta (Change Increment)

```markdown
# novelspec/changes/add-chapter-11-20/specs/outline/spec.md

## ADDED Requirements

### Requirement: Chapter 11 - Sect Competition
Chapter 11 SHALL open the Sect Competition arc.

#### Scenario: Competition Opening
- **WHEN** Chapter 11 starts
- **THEN** Sect announces triennial competition
- **THEN** Introduce reward: Top 3 enter Scripture Pavilion
- **THEN** Protagonist decides to participate
- **THEN** Introduce opponent: Outer sect genius Li Jian

### Requirement: Chapter 12 - First Victory
Chapter 12 SHALL demonstrate protagonist strength growth.

#### Scenario: First Round Match
- **WHEN** Protagonist participates in first round
- **THEN** Opponent is Qi Refining Level 6 outer sect disciple
- **THEN** Protagonist hides strength (Only use 70%)
- **THEN** Narrow victory but do not expose sign-in system ability
- **THEN** Attract some attention

### Requirement: Chapter 13 - Mysterious Mentor
Chapter 13 SHALL introduce important supporting character.

#### Scenario: Meeting Elder Yun
- **WHEN** Protagonist cultivates alone after match
- **THEN** Mysterious Elder Yun appears
- **THEN** Elder Yun sees protagonist is extraordinary
- **THEN** Propose to guide protagonist
- **THEN** Plant foreshadowing: Elder Yun identity mysterious

## MODIFIED Requirements

### Requirement: Protagonist Strength Level
Protagonist MUST reach Qi Refining Level 9 in Chapters 11-20.

#### Scenario: Status at end of Chapter 20
- **WHEN** Chapter 20 ends
- **THEN** Cultivation Level: Qi Refining Level 9 (Close to Foundation Establishment)
- **THEN** Mastered Skills: Xuan Yuan Art (Great Success), Wind Thunder Step (Proficient), Cloud Breaking Hand (Beginner)
- **THEN** Combat Power: Can fight 2 levels higher
- **THEN** Reputation: Somewhat famous in outer sect

#### Scenario: Growth Trajectory
- **WHEN** During Chapters 11-20
- **THEN** Chapter 11: Qi Refining Level 7
- **THEN** Chapter 15: Breakthrough to Qi Refining Level 8
- **THEN** Chapter 19: Breakthrough to Qi Refining Level 9
- **THEN** Each breakthrough has reasonable opportunity (Sign-in reward + Own effort)
```

**ADDED/MODIFIED Usage Instructions**:

- **ADDED**: New content, previously not existing in specs/
- **MODIFIED**: Modify existing content, need to copy original Requirement completely and modify
- **REMOVED**: Delete content (Mark reason and migration plan)
- **RENAMED**: Rename only (Mark FROM/TO)

### 2.3 Workflow Design

Novel-Writer-OpenSpec adopts **Five-Stage Workflow**, borrowing from OpenSpec's Three-Stage Cycle:

```
┌─────────────────────────────────────┐
│  Stage 1: Create Change Proposal       │
│  - Define creative goal (Chap X-Y)     │
│  - Generate proposal/design/tasks      │
│  - Write spec deltas (ADDED/MODIFIED)  │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│  Stage 2: Validate Proposal            │
│  - novelspec validate --strict         │
│  - Check format, semantics, consistency│
│  - AI fixes errors                     │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│  Stage 3: Execute Writing              │
│  - AI reads specs/ (truth)             │
│  - AI reads change delta (increment)   │
│  - Generate chapters per tasks.md      │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│  Stage 4: Continuous Verification      │
│  - Run validate after each chapter     │
│  - AI receives instant feedback        │
│  - Fix errors then continue            │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│  Stage 5: Archive Change               │
│  - novelspec archive <change-id>       │
│  - Merge delta to specs/               │
│  - Move to archive/                    │
│  - specs/ becomes new truth            │
└─────────────────────────────────────┘
         │
         └──> Return to Stage 1 (Next batch of chapters)
```

#### Stage 1: Create Change Proposal (Detailed Example)

**Scenario**: Writing Chapters 11-20

```bash
# Human creates proposal via AI assistant
# Use command: /novelspec-proposal

# AI creates directory structure
mkdir -p novelspec/changes/add-chapter-11-20/specs/{outline,characters}
```

**File 1: `proposal.md`** (Change Intent)

```markdown
## Why
Chapters 1-10 completed protagonist introduction and basic cultivation. Chapters 11-20 need to:
- Demonstrate protagonist strength and growth via Sect Competition
- Advance main plot (Obtain advanced techniques and resources)
- Establish relationships with core supporting characters (Li Jian, Elder Yun)
- Plant foreshadowing for Volume 2

## What Changes
- Add outline specs for chapters 11-20
- Protagonist level from Qi Refining Level 7 → Qi Refining Level 9
- Add supporting character specs: Genius disciple Li Jian, Mysterious mentor Elder Yun
- Extend magic system: Add advanced skill description (Cloud Breaking Hand)

## Impact
- **Impacted Specs**:
  - `specs/outline/spec.md` (Add 10 chapters)
  - `specs/characters/protagonist/spec.md` (Level and skill update)
  - `specs/characters/li-jian/spec.md` (Added)
  - `specs/characters/yun-elder/spec.md` (Added)
  - `specs/worldbuilding/magic-system/spec.md` (Added skill)
- **Impacted Chapters**: Add `chapters/volume-2/chapter-011.md` to `chapter-020.md`
- **Estimated Word Count**: Approx 35,000 words (10 chapters × 3,500 words/chapter)
```

**File 2: `design.md`** (Technical Plan)

```markdown
## Context
Chapters 11-20 are the climax of Volume 1, need to balance pacing and "cool points" (Shuangdian).

## Goals / Non-Goals

**Goals**:
- Demonstrate combination of protagonist talent and effort
- Establish reader expectation for protagonist strength
- Plant important foreshadowing for Volume 2
- Introduce key supporting characters to enrich story

**Non-Goals**:
- Do not overly expose sign-in system secrets
- Do not introduce too many new settings adding complexity
- Do not let protagonist strength improve too fast losing reasonableness

## Technical Decisions

### POV (Perspective) Design
- **Chapters 11-15**: Mainly protagonist third-person limited POV
- **Chapters 16-18**: Interspersed with opponent POV (Li Jian), adding suspense and contrast
- **Chapters 19-20**: Return to protagonist POV, showing climax and turning point

### Pacing Control
- **Chapter 11**: Buildup (Slow pace), introduce competition rules and opponents
- **Chapters 12-18**: Matches (Fast pace), one chapter per fight or multiple fights per chapter
- **Chapters 19-20**: Turning point (Medium pace), unexpected situation and wrap-up

### Foreshadowing Arrangement
- **Chapter 13**: Plant foreshadowing for Elder Yun's true identity (Revealed in Volume 2)
- **Chapter 17**: Hint at internal sect conflicts (Main plot of Volume 2)
- **Chapter 20**: Lead to larger worldview (Other sects, evil cultivator organizations)

### "Cool Points" Design
- Chapter 12: First win, show strength
- Chapter 15: Breakthrough to Qi Refining Level 8
- Chapter 18: Desperate counter-kill strong enemy
- Chapter 19: Breakthrough to Qi Refining Level 9
- Chapter 20: Obtain precious reward

## Risks / Trade-offs

**Risks**:
- Pace too fast may cause reader fatigue
- Too many new characters may distract attention

**Mitigation**:
- Arrange a soothing chapter every 2-3 chapters (Daily life, emotional line)
- New characters focus on 2 core supporting characters

## Migration Plan
No migration needed, pure new content.
```

**File 3: `tasks.md`** (Task List)

```markdown
## 1. Spec Updates

- [ ] 1.1 Update protagonist spec (`specs/characters/protagonist/spec.md`)
  - Level: Qi Refining 7 → Qi Refining 9
  - New Skill: Cloud Breaking Hand
  - Update combat power description
  
- [ ] 1.2 Create Li Jian character spec (`specs/characters/li-jian/spec.md`)
  - Basic setting: Outer sect genius, Qi Refining 8
  - Personality: Proud but not stupid, has own persistence
  - Behavior pattern: Facing challenge, facing failure
  
- [ ] 1.3 Create Elder Yun character spec (`specs/characters/yun-elder/spec.md`)
  - Basic setting: Mysterious strong person, cultivation level unknown
  - Personality: Indifferent, wise, cherishes talent
  - Behavior pattern: Guiding protagonist, observing protagonist
  
- [ ] 1.4 Extend magic system (`specs/worldbuilding/magic-system/spec.md`)
  - New Skill: Cloud Breaking Hand (Late Qi Refining skill)
  - Skill effect, cultivation condition, power description

## 2. Chapter Writing

- [ ] 2.1 Chapter 11: Sect Competition Opening
  - Introduce competition rules and rewards
  - Protagonist decides to participate
  - Introduce opponent Li Jian
  
- [ ] 2.2 Chapter 12: First Round Match
  - Protagonist vs ordinary outer sect disciple
  - Easy win but not expose full strength
  - Attract some attention
  
- [ ] 2.3 Chapter 13: Meeting Elder Yun
  - Cultivate alone after match
  - Elder Yun appears and sees protagonist is extraordinary
  - Propose guidance, plant identity foreshadowing
  
- [ ] 2.4 Chapter 14: Special Training Begins
  - Elder Yun guides cultivation essentials
  - Protagonist cultivates Cloud Breaking Hand
  - Strength steadily improves
  
- [ ] 2.5 Chapter 15: Second Round Match
  - Protagonist vs Qi Refining 7 opponent
  - Use newly learned skill
  - Breakthrough to Qi Refining 8 during battle
  
- [ ] 2.6 Chapter 16: Opponent POV (Li Jian)
  - Switch to Li Jian POV
  - Show Li Jian's strength and inner thoughts
  - Interested in protagonist
  
- [ ] 2.7 Chapter 17: Semi-final
  - Protagonist vs strong enemy
  - Fall into hard fight
  - Hint someone in sect targets protagonist
  
- [ ] 2.8 Chapter 18: Dangerous Breakthrough
  - Comprehend Cloud Breaking Hand essence in desperate situation
  - Turn defeat into victory
  - Gain audience recognition
  
- [ ] 2.9 Chapter 19: Final Begins
  - Protagonist vs Li Jian
  - Fierce battle
  - Breakthrough to Qi Refining 9 during match
  
- [ ] 2.10 Chapter 20: Sect Competition Ends
  - Protagonist wins or narrowly loses (According to subsequent plan)
  - Obtain reward (Enter Scripture Pavilion)
  - Lead to larger worldview

## 3. Validation

- [ ] 3.1 Consistency Check
  - Character behavior fits setting
  - Magic usage fits rules
  - Timeline no conflict
  
- [ ] 3.2 Foreshadowing Record
  - Record Elder Yun identity foreshadowing
  - Record sect conflict foreshadowing
  - Record Volume 2 lead-in
```

**File 4: `specs/outline/spec.md`** (Outline Delta)

```markdown
## ADDED Requirements

### Requirement: Chapter 11 - Sect Competition Opening
[Complete spec, see previous example]

### Requirement: Chapter 12 - First Victory
[Complete spec, see previous example]

... (Specs for Chapters 13-20)
```

**File 5: `specs/characters/li-jian/spec.md`** (New Character Spec)

```markdown
## Purpose
Complete spec definition for outer sect genius Li Jian.

## Requirements

### Requirement: Basic Setting
Li Jian SHALL be the recognized genius of the outer sect.

#### Scenario: Identity Information
- **WHEN** Li Jian appears or is mentioned
- **THEN** Name: Li Jian
- **THEN** Age: 22 years old
- **THEN** Cultivation: Qi Refining Level 8
- **THEN** Personality: Proud but not stupid, principled
- **THEN** Status: Outer sect number one genius

### Requirement: Behavior Pattern
Li Jian SHALL exhibit consistent behavior patterns.

#### Scenario: Facing Challenge
- **WHEN** Someone challenges Li Jian
- **THEN** Accept challenge but do not underestimate enemy
- **THEN** Go all out
- **THEN** Not arrogant in victory, not discouraged in defeat

#### Scenario: Facing Failure
- **WHEN** Li Jian fails (e.g., defeated by protagonist)
- **THEN** Acknowledge opponent strength
- **THEN** Reflect on own shortcomings
- **THEN** Do not hold grudge, instead respect opponent
```

#### Stage 2: Validate Proposal

```bash
# Run validation command
novelspec validate add-chapter-11-20 --strict

# System checks
Checks:
✓ proposal.md format correct, contains Why/What/Impact three parts
✓ design.md contains Context/Goals/Technical Decisions
✓ tasks.md uses task list format, contains spec updates, chapter writing, validation
✓ specs/outline/spec.md uses ADDED format to add new chapters
✓ specs/characters/li-jian/spec.md format correct
✓ All Requirements contain at least one Scenario
✓ All Scenarios use `#### Scenario:` format (4 hashes)
✓ Use SHALL/MUST keywords to clarify constraint strength
✗ specs/characters/li-jian/spec.md missing "Dialogue Style" Requirement

# AI adds after feedback
→ AI adds "Dialogue Style" Requirement
→ Re-validate
✓ All checks passed
```

#### Stage 3: Execute Writing

```bash
# AI executes writing via /novelspec-apply command

# AI reads context (by priority)
1. novelspec/project.md (Highest constraint: creative principles, style guide)
2. novelspec/specs/characters/protagonist/spec.md (Protagonist setting)
3. novelspec/specs/characters/heroine/spec.md (Heroine setting, if relevant)
4. novelspec/specs/worldbuilding/magic-system/spec.md (Magic system)
5. novelspec/specs/outline/spec.md (Existing outline)
6. novelspec/changes/add-chapter-11-20/ (Current task)
   - proposal.md (Understand intent)
   - design.md (Technical plan)
   - tasks.md (Execution list)
   - specs/ (Delta specs)

# AI executes tasks.md
Task 1.1: Update protagonist spec
→ In changes/add-chapter-11-20/specs/characters/protagonist/spec.md
  Use MODIFIED Requirements format
  Copy original Requirement completely and modify level and skill

Task 2.1: Write Chapter 11
→ Generate chapters/volume-2/chapter-011.md based on all specs
→ Content includes:
  - Adhere to project.md style guide (3000-4000 words, modern vernacular)
  - Protagonist behavior fits protagonist/spec.md
  - Magic usage fits magic-system/spec.md
  - Plot fits outline/spec.md Chapter 11 Requirement
→ Automatically run novelspec validate add-chapter-11-20
→ If error, fix then continue

Task 2.2-2.10: Sequentially write Chapters 12-20
→ Validate once after completing each chapter
→ Ensure continuity
```

**AI Generated Chapter 11 Example**:

```markdown
# Chapter 11 Sect Competition Opening

Crowds surged on the Qingyun Sect Outer Gate Square.

Chen Fan stood at the back of the crowd, his gaze sweeping over the inner sect elders on the high platform. The triennial Sect Competition finally kicked off today.

"For this competition, the top three can enter the Scripture Pavilion to choose a technique." The presiding elder's voice clearly spread throughout the venue.

Scripture Pavilion. Chen Fan's eyes narrowed.

Precious techniques and secret manuals of the sect were collected there, which outer sect disciples could not approach normally. If he could enter, perhaps he could find matching skills more suitable for the Xuan Yuan Art.

"Junior Brother Chen also participating?"

A familiar voice came from beside him. Chen Fan turned his head and saw fellow senior brother Zhang Yun.

"En, want to try." Chen Fan answered calmly.

Zhang Yun smiled bitterly: "I'll pass, Qi Refining Level 3 participating is just feeding kills. But Junior Brother Chen you are Qi Refining Level 7, actually have some chance."

Qi Refining Level 7. This was the cultivation level Chen Fan declared to the outside. In fact, after this period of signing in and cultivation, he had stabilized at the peak of Qi Refining Level 7, likely to breakthrough anytime.

But he wouldn't say it.

"Li Jian also signed up." Zhang Yun lowered his voice, "Outer sect number one genius, Qi Refining Level 8, almost no one is his opponent."

Chen Fan followed Zhang Yun's gaze.

In front of the crowd, a young man in green stood alone, no one dared to approach around him. The young man had a handsome face, gaze sharp like a sword, faintly revealing a fierce aura.

Li Jian.

Chen Fan silently noted this name. Qi Refining Level 8, indeed very strong. But if only so, it was not that he had no power to fight.

"All participating disciples, group by cultivation level..."

As the elder's voice sounded, the Sect Competition officially began.
```

**validate automatic check**:

```bash
✓ Word count: Approx 3200 words, fits project.md 3000-4000 words requirement
✓ Language style: Modern vernacular, concise and brisk, no internet slang
✓ Protagonist behavior: Calm observation, cautiously hide strength, fits protagonist/spec.md
✓ Dialogue style: Concise and substantive, fits setting
✓ Plot: Fits outline/spec.md Chapter 11 Requirement
✓ No undefined settings (Li Jian defined in specs)
```

#### Stage 4: Continuous Verification

```bash
# AI automatically validates after completing each chapter
novelspec validate add-chapter-11-20

# Validation dimension example (Chapter 12)
Checks:
✓ Chapter 12 protagonist behavior fits specs/characters/protagonist/spec.md
  - Remain calm facing danger ✓
  - Do not easily expose full strength ✓
  
✓ Chapter 12 magic description fits specs/worldbuilding/magic-system/spec.md
  - Use Xuan Yuan Art ✓
  - Use Wind Thunder Step ✓
  
✓ Chapter 12 plot fits changes/.../specs/outline/spec.md Chapter 12 spec
  - Opponent is Qi Refining 6 outer sect disciple ✓
  - Protagonist hides strength ✓
  - Narrow victory ✓
  
✗ Chapter 12 appeared undefined "Void Breaking Sword Art"
  → Rule violation: No such skill in specs/worldbuilding/magic-system/spec.md
  → AI receives feedback, chooses:
    a) Modify Chapter 12, use defined skill (Xuan Yuan Art or Wind Thunder Step)
    b) Update magic-system/spec.md add "Void Breaking Sword Art" definition
    
# AI chooses plan a, modifies Chapter 12
→ Re-validate
✓ All passed
```

#### Stage 5: Archive Change

```bash
# Archive after all tasks completed
novelspec archive add-chapter-11-20

# System automatically executes merge operation

# 1. Merge outline delta
Merge changes/add-chapter-11-20/specs/outline/spec.md
  → specs/outline/spec.md
  
Operations:
- Append ADDED Requirements (Chapters 11-20) to specs/outline/spec.md
- If MODIFIED Requirements exist, replace corresponding content
- If REMOVED Requirements exist, delete corresponding content

# 2. Merge protagonist spec update
Merge changes/add-chapter-11-20/specs/characters/protagonist/spec.md
  → specs/characters/protagonist/spec.md
  
Operations:
- Find MODIFIED Requirement (e.g., "Capability Growth")
- Replace original Requirement completely

# 3. Add new character specs
Add specs/characters/li-jian/spec.md
Add specs/characters/yun-elder/spec.md

Operations:
- Copy from changes/.../specs/characters/ to specs/characters/
- Remove ADDED tag, become formal spec

# 4. Update magic system (if any)
Update specs/worldbuilding/magic-system/spec.md

Operations:
- Merge added skill definitions

# 5. Move to archive
Move changes/add-chapter-11-20/
  → changes/archive/2025-01-22-add-chapter-11-20/

Operations:
- Retain proposal.md, design.md, tasks.md completely
- Retain specs/ delta completely (as historical record)
- Add archive date prefix

# Result
After archiving:
✓ specs/ becomes new Single Source of Truth, containing full outline for Chapters 1-20
✓ specs/characters/ contains latest specs for all appeared characters
✓ archive/ retains full change history and intent (proposal.md)
✓ AI reads latest specs/ as context when writing Chapter 21 next time
```

**Archived `specs/outline/spec.md`** (Partial):

```markdown
# novelspec/specs/outline/spec.md

## Purpose
Established part of story outline, basis for AI advancing plot.

## Requirements

### Requirement: Chapter 1 - Awakening
[Original Content]

### Requirement: Chapter 2 - Exploring System
[Original Content]

...

### Requirement: Chapter 10 - Outer Sect Trial
[Original Content]

### Requirement: Chapter 11 - Sect Competition Opening
Chapter 11 SHALL open the Sect Competition arc.

#### Scenario: Competition Opening
- **WHEN** Chapter 11 starts
- **THEN** Sect announces triennial competition
- **THEN** Introduce reward (Enter Scripture Pavilion)
- **THEN** Protagonist decides to participate
- **THEN** Introduce opponent Li Jian

### Requirement: Chapter 12 - First Victory
[Complete Spec]

...

### Requirement: Chapter 20 - Sect Competition Ends
[Complete Spec]
```

---

## III. Functional Requirements

### 3.1 CLI Commands

Novel-Writer-OpenSpec uses independent `novelspec` command, avoiding conflict with OpenSpec:

```bash
# Project Management
novelspec init <project-name>        # Initialize novel project
novelspec init <project-name> --here # Initialize in current directory

# Change Management
novelspec list                       # List active changes (chapters to be written)
novelspec list --archive             # List archived changes
novelspec show <change-id>           # View change details
novelspec validate <change-id>       # Validate change consistency
novelspec validate <change-id> --strict  # Strict validation
novelspec archive <change-id>        # Archive completed change

# Spec Management
novelspec list --specs               # List established specs
novelspec show <spec-id> --type spec # View spec details

# Auxiliary Functions
novelspec check                      # Check project configuration
novelspec version                    # View version info
novelspec help                       # View help
```

**Differences from OpenSpec**:

| Feature | OpenSpec | Novel-Writer-OpenSpec |
|------|----------|----------------------|
| Command Prefix | `openspec` | `novelspec` |
| Directory Name | `openspec/` | `novelspec/` |
| Init | `openspec init` | `novelspec init <project-name>` |
| Validate | `openspec validate <change>` | `novelspec validate <change>` |

### 3.2 AI Assistant Integration

Support slash commands for mainstream AI tools:

| AI Tool | Command Format | Config Location |
|---------|---------|---------|
| **Claude Code** | `/novelspec-proposal`, `/novelspec-apply`, `/novelspec-archive` | `.claude/commands/` |
| **Cursor** | `/novelspec-proposal`, `/novelspec-apply`, `/novelspec-archive` | `.cursor/commands/` |
| **Windsurf** | `/novelspec-proposal`, `/novelspec-apply`, `/novelspec-archive` | `.windsurf/workflows/` |
| **Gemini CLI** | `/novel/proposal`, `/novel/apply`, `/novel/archive` | `.gemini/commands/*.toml` |
| **Others** | Refer to `novelspec/AGENTS.md` instructions | `novelspec/AGENTS.md` |

**AI Assistant Command Description**:

#### `/novelspec-proposal` (Create Proposal)
```
Usage Scenario: Human wants to write new chapters or extend settings

AI Execution:
1. Create changes/<change-id>/ directory
2. Generate proposal.md (Ask human intent)
3. Generate design.md (Technical plan)
4. Generate tasks.md (Task list)
5. Generate specs/ deltas (ADDED/MODIFIED)
6. Run novelspec validate check

Output:
- Complete change proposal structure
- Validation results and modification suggestions
```

#### `/novelspec-apply` (Execute Writing)
```
Usage Scenario: Proposal validation passed, start executing writing

AI Execution:
1. Read novelspec/project.md (Creative principles)
2. Read novelspec/specs/ (Current truth)
3. Read changes/<change-id>/ (Current task)
4. Execute in tasks.md order
5. Generate chapter content to chapters/
6. Run validate after each chapter
7. Mark completed tasks as [x]

Output:
- Chapter content files
- Continuous verification feedback
- Completion progress update
```

#### `/novelspec-archive` (Archive Change)
```
Usage Scenario: All tasks completed, archive change

AI Execution:
1. Check if tasks.md are all completed
2. Run final validate
3. Call novelspec archive <change-id>
4. System automatically merges delta to specs/
5. Move to archive/

Output:
- Archive success confirmation
- specs/ update summary
- Next step suggestions
```

### 3.3 Validation Rules

`novelspec validate` executes three-level validation:

#### 3.3.1 Format Validation

Check file structure and syntax:

```yaml
proposal.md:
  - Must contain: Why, What Changes, Impact
  - Why: At least 1 sentence explaining reason
  - What Changes: Use list format
  - Impact: Mark impacted specs

design.md:
  - Optional file
  - If exists, must contain: Context, Goals, Technical Decisions
  
tasks.md:
  - Must use task list format: - [ ] or - [x]
  - Task description clear
  - At least contain: Spec updates, Chapter writing

spec.md:
  - Must use Requirements + Scenarios format
  - Each Requirement at least one Scenario
  - Scenario must use #### Scenario: format (4 hashes)
  - Must use SHALL/MUST/MAY keywords

delta spec.md:
  - Must use ADDED/MODIFIED/REMOVED tags
  - MODIFIED must contain complete Requirement content
```

#### 3.3.2 Semantic Validation

Check content reasonableness:

```yaml
Character Consistency:
  - Character behavior fits specs/characters/<name>/spec.md definition
  - Dialogue style fits character setting
  - Cultivation level change reasonable (Cannot breakthrough jumping levels)

Worldview Consistency:
  - Magic usage fits specs/worldbuilding/magic-system/spec.md
  - Geography description fits specs/worldbuilding/geography/spec.md
  - Faction relationship fits specs/worldbuilding/factions/spec.md

Plot Consistency:
  - Chapter content fits specs/outline/spec.md definition
  - Plot development has causal logic
  - No undefined characters, locations, skills

Reference Integrity:
  - Mentioned characters defined in specs/characters/
  - Used skills defined in specs/worldbuilding/magic-system/
  - Mentioned locations defined in specs/worldbuilding/geography/
```

#### 3.3.3 Cross-Chapter Validation

Check continuity:

```yaml
Timeline Consistency:
  - Chapter chronological order reasonable
  - No time jump contradictions
  - Character age growth fits timeline

Character Status Consistency:
  - Cultivation level change traceable
  - Injury recovery logical
  - Relationship development has process

Foreshadowing Management:
  - Record planted foreshadowing
  - Check foreshadowing resolution
  - Warn about long-unresolved foreshadowing
```

**Validation Output Example**:

```bash
$ novelspec validate add-chapter-11-20 --strict

Format Verification:
✓ proposal.md contains Why/What/Impact
✓ design.md contains Context/Goals/Technical Decisions
✓ tasks.md uses task list format
✓ specs/outline/spec.md uses ADDED format
✓ specs/characters/li-jian/spec.md format correct
✓ All Scenarios use #### Scenario: format
✓ Use SHALL/MUST keywords

Semantic Verification:
✓ Chapter 11 protagonist behavior fits protagonist/spec.md
✓ Chapter 12 magic usage fits magic-system/spec.md
✗ Chapter 13 undefined character "Elder Yun"
  → Need to create specs/characters/yun-elder/spec.md
✓ Chapters 14-20 plot fits outline spec

Cross-Chapter Verification:
✓ Timeline consistent (Chapters 11-20 span approx 15 days)
✓ Protagonist cultivation change reasonable (7->9 levels, with breakthrough opportunity)
⚠ Chapter 13 planted Elder Yun identity foreshadowing, unresolved
  → Suggest noting resolution plan in design.md

Verification Result: 1 error, 1 warning
Please fix errors and re-validate.
```

### 3.4 Template System

Provide novel-specific templates during project initialization:

```
novelspec-templates/
├── project.md.template           # Project convention template
├── AGENTS.md.template            # AI assistant instruction template
│
├── characters/
│   └── _template/
│       └── spec.md.template     # Character spec template
│
├── worldbuilding/
│   ├── magic-system/
│   │   └── spec.md.template     # Magic system template
│   ├── geography/
│   │   └── spec.md.template     # Geography setting template
│   └── factions/
│       └── spec.md.template     # Faction organization template
│
└── outline/
    └── spec.md.template         # Outline template
```

**`project.md.template`**:

```markdown
# novelspec/project.md

## Project Info
- Novel Name: {{NOVEL_NAME}}
- Genre: {{GENRE}} (Fantasy/Wuxia/Urban/Sci-Fi/Other)
- Target Word Count: {{TARGET_WORDS}} million words
- Estimated Volumes: {{VOLUMES}} volumes

## Creative Principles

This project follows these core creative principles (AI must strictly adhere):

1. **Logical Consistency**: World settings once established must remain consistent
2. **Character Consistency**: Character behavior must fit personality settings and growth trajectory
3. **Plot Reasonableness**: Plot development needs causal logic
4. **Unified Style**: Maintain unified narrative style

## Style Guide

- **Narrative Perspective**: {{POV}} (First person/Third person limited/Omniscient)
- **Language Style**: {{LANGUAGE_STYLE}}
- **Chapter Length**: {{CHAPTER_LENGTH}} words/chapter
- **Update Frequency**: {{UPDATE_FREQUENCY}}

## Quality Standards

- Each chapter must advance the plot or deepen character
- Dialogue fits character identity and personality
- Descriptions should be visual

## Taboos

- ❌ No arbitrary changes to core settings
- ❌ No character OOC
- ❌ No undefined settings
```

**`characters/_template/spec.md.template`**:

```markdown
# novelspec/specs/characters/{{CHARACTER_ID}}/spec.md

## Purpose
Complete spec definition for {{CHARACTER_NAME}}.

## Requirements

### Requirement: Basic Setting
{{CHARACTER_NAME}} SHALL have clear identity background.

#### Scenario: Identity Information
- **WHEN** {{CHARACTER_NAME}} appears or is mentioned
- **THEN** Name: {{CHARACTER_NAME}}
- **THEN** Age: {{AGE}}
- **THEN** Personality: {{PERSONALITY}}
- **THEN** Traits: {{TRAITS}}

### Requirement: Behavior Pattern
{{CHARACTER_NAME}} SHALL exhibit consistent behavior patterns in different situations.

#### Scenario: Facing Danger
- **WHEN** Encountering threat
- **THEN** {{BEHAVIOR_PATTERN}}

### Requirement: Dialogue Style
{{CHARACTER_NAME}}'s dialogue SHALL fit their identity.

#### Scenario: Daily Dialogue
- **WHEN** Daily communication
- **THEN** {{DIALOGUE_STYLE}}
```

---

## IV. Technical Implementation

### 4.1 Technical Architecture

```
┌─────────────────────────────────────────────┐
│           User Interface (CLI + AI Assistant)   │
├─────────────────────────────────────────────┤
│              Command Layer (Commands)          │
│  ┌──────────┬──────────┬──────────┐        │
│  │  init    │ validate │ archive  │        │
│  └──────────┴──────────┴──────────┘        │
├─────────────────────────────────────────────┤
│              Core Layer (Core)                 │
│  ┌──────────┬──────────┬──────────┐        │
│  │ Parser   │Validator │ Archiver │        │
│  └──────────┴──────────┴──────────┘        │
├─────────────────────────────────────────────┤
│            Utils Layer (Utils)                 │
│  ┌──────────┬──────────┬──────────┐        │
│  │ FileOps  │  Logger  │ Template │        │
│  └──────────┴──────────┴──────────┘        │
└─────────────────────────────────────────────┘
```

### 4.2 Core Module Design

#### 4.2.1 Parser

```typescript
/**
 * Parse spec files
 */
class SpecParser {
  /**
   * Parse spec.md file, extract Requirements and Scenarios
   */
  parseSpec(filePath: string): Spec {
    // Read file content
    // Extract Requirements (### Requirement:)
    // Extract Scenarios (#### Scenario:)
    // Extract keywords (SHALL/MUST/MAY)
    // Return structured object
  }

  /**
   * Parse delta spec
   */
  parseDelta(filePath: string): Delta {
    // Identify ADDED/MODIFIED/REMOVED
    // Extract corresponding Requirements
    // Return delta object
  }

  /**
   * Parse proposal.md
   */
  parseProposal(filePath: string): Proposal {
    // Extract Why/What/Impact
    // Return proposal object
  }
}
```

#### 4.2.2 Validator

```typescript
/**
 * Validate specs and changes
 */
class NovelValidator {
  /**
   * Format validation
   */
  validateFormat(change: Change): ValidationResult {
    // Check proposal.md format
    // Check tasks.md format
    // Check spec.md Requirements + Scenarios format
    // Check SHALL/MUST keyword usage
  }

  /**
   * Semantic validation (Novel specific)
   */
  validateSemantics(change: Change, specs: Specs): ValidationResult {
    // Check character behavior consistency
    // Check worldview setting consistency
    // Check plot logic
    // Check reference integrity (No undefined roles/skills/locations)
  }

  /**
   * Cross-chapter validation
   */
  validateCrossChapter(chapters: Chapter[]): ValidationResult {
    // Check timeline consistency
    // Check character status change reasonableness
    // Check foreshadowing management
  }

  /**
   * Strict validation (All checks)
   */
  validateStrict(change: Change, specs: Specs): ValidationResult {
    // Execute all validations
    // Return comprehensive result
  }
}
```

#### 4.2.3 Archiver

```typescript
/**
 * Archive change, merge to specs/
 */
class ChangeArchiver {
  /**
   * Archive change
   */
  archive(changeId: string): ArchiveResult {
    // 1. Read change delta
    // 2. Apply to specs/
    //    - ADDED: Append new Requirements
    //    - MODIFIED: Replace corresponding Requirements
    //    - REMOVED: Delete corresponding Requirements
    // 3. Move change to archive/
    // 4. Add date prefix
  }

  /**
   * Merge delta to spec
   */
  private mergeDelta(delta: Delta, spec: Spec): Spec {
    // Process ADDED Requirements
    // Process MODIFIED Requirements (Complete replacement)
    // Process REMOVED Requirements
    // Return updated spec
  }
}
```

### 4.3 File Operations

```typescript
/**
 * File and directory operation utils
 */
class FileOperations {
  /**
   * Read spec file
   */
  readSpec(path: string): string {
    // Read file content
  }

  /**
   * Write spec file
   */
  writeSpec(path: string, content: string): void {
    // Write file
  }

  /**
   * Move directory (Archive)
   */
  moveDirectory(from: string, to: string): void {
    // Move directory
  }

  /**
   * Copy template
   */
  copyTemplate(template: string, dest: string, vars: object): void {
    // Copy template and replace variables
  }
}
```

### 4.4 AI Efficiency Mechanism Summary

| Mechanism | Technical Implementation | AI Efficiency Effect |
|------|---------|-----------|
| **Context Isolation** | `specs/` (truth) vs `changes/` (task) separation | AI clearly knows "existing" vs "to-do", understanding cost reduced by 50% |
| **Intent Clarity** | `proposal.md` explains change reason | AI understands "why", reducing deviation from specs |
| **Strict Format** | Requirements + Scenarios fixed format | AI can automatically parse and validate, accuracy improved |
| **Incremental Management** | ADDED/MODIFIED/REMOVED explicitly marked | AI precisely understands change scope, avoiding omission or overwriting |
| **Auto Validation** | `novelspec validate` instant feedback | AI corrects errors immediately, validation efficiency increased by 10x |
| **Truth Update** | `specs/` unique accurate after archive | AI next time based on accurate state, reducing error accumulation |

---

## V. Implementation Roadmap

### Phase 1: MVP (Minimum Viable Product)

**Goal**: Validate core concepts, complete basic functions

**Feature List**:
- [ ] `novelspec init` command (Project initialization)
- [ ] Novel project templates (project.md, basic specs/ structure)
- [ ] `novelspec validate` command (Format validation)
- [ ] AI assistant instructions (AGENTS.md)
- [ ] Basic documentation (README, workflow-guide)

**Success Criteria**:
- Can initialize a novel project
- Can validate proposal and spec format
- AI can use `/novelspec-proposal` to create proposal

**Estimated Time**: 2-3 weeks

### Phase 2: Core Functions

**Goal**: Perfect validation and archiving functions

**Feature List**:
- [ ] Semantic validator (Character, Worldview, Plot consistency)
- [ ] `novelspec archive` command (Change archiving)
- [ ] Perfect templates (character, worldbuilding, outline)
- [ ] `/novelspec-apply` and `/novelspec-archive` AI commands
- [ ] Detailed documentation and examples

**Success Criteria**:
- validate can catch common errors (OOC, setting conflicts)
- archive can correctly merge delta to specs/
- Can write 100k words novel with complete workflow

**Estimated Time**: 3-4 weeks

### Phase 3: Enhanced Functions

**Goal**: Improve user experience and functional completeness

**Feature List**:
- [ ] Cross-chapter validation (Timeline, foreshadowing tracking)
- [ ] `novelspec list --stats` Statistics info
- [ ] `novelspec check` Health check
- [ ] Export function (Generate EPUB/PDF)
- [ ] Error prompt optimization

**Success Criteria**:
- Can track foreshadowing and timeline
- Smooth user experience, friendly error prompts
- Support exporting to ebook formats

**Estimated Time**: 2-3 weeks

### Phase 4: Ecosystem Construction

**Goal**: Expand toolchain and community

**Feature List**:
- [ ] VS Code extension (Syntax highlighting, real-time validation)
- [ ] Web interface (Visual management of specs and changes)
- [ ] Community template library (Different types of novel templates)
- [ ] Best practice documentation

**Success Criteria**:
- VS Code extension available
- Community contributed templates available
- Success cases and best practices available

**Estimated Time**: Ongoing

---

## VI. Success Criteria

### 6.1 Functional Completeness

- [x] **Project Initialization**
  - `novelspec init <project-name>` can create complete project structure
  - Contains project.md, AGENTS.md, basic specs/ templates
  
- [ ] **Change Management**
  - AI can create structured proposal (proposal, design, tasks, specs)
  - `novelspec validate` can catch format and semantic errors
  - `novelspec archive` can correctly merge and archive
  
- [ ] **AI Integration**
  - Support slash commands for mainstream AI tools
  - AI can efficiently use complete workflow

### 6.2 Quality Standards

- [ ] **Validation Accuracy**
  - Format validation: 100% accurately identify format errors
  - Semantic validation: Catch ≥80% common errors (OOC, setting conflicts)
  - False positive rate: ≤5%
  
- [ ] **Data Consistency**
  - `specs/` is always the unique accurate truth
  - `archive/` retains full history and intent
  - No data loss or corruption
  
- [ ] **Documentation Quality**
  - README clear and complete
  - Workflow guide has detailed examples
  - API documentation accurate

### 6.3 Usability

- [ ] **Ease of Use**
  - New user completes first proposal creation within 15 minutes
  - Commands concise and intuitive, no need to memorize complex parameters
  - Error prompts friendly, provide solutions
  
- [ ] **Performance**
  - `validate` command completes within < 5 seconds
  - `archive` command completes within < 3 seconds
  - Support 1 million words project without performance issues
  
- [ ] **Compatibility**
  - Support macOS/Linux/Windows
  - Support Node.js ≥ 18.0.0
  - Support mainstream AI tools (Claude, Cursor, Windsurf, Gemini)

### 6.4 Actual Verification

**Verification Method**: Create a 100k words novel using Novel-Writer-OpenSpec

**Verification Metrics**:
- [ ] AI understanding accuracy: ≥ 90% (Generated content fits specs)
- [ ] Consistency error rate: ≤ 5% (OOC, setting conflicts)
- [ ] Creation speed: Improved by ≥ 30% compared to traditional methods
- [ ] Validation efficiency: Improved by ≥ 10x compared to manual check
- [ ] User satisfaction: ≥ 4/5 stars

---

## VII. Risks and Challenges

### 7.1 Technical Risks

| Risk | Impact | Mitigation |
|------|------|---------|
| High validator false positive rate | Poor user experience, distrust tool | Continuously optimize validation rules, provide false positive feedback mechanism |
| Archive merge error | Data corruption, user loss | Backup before archive, provide rollback function |
| Performance issues | Lag in large projects | Incremental parsing, caching mechanism |

### 7.2 User Risks

| Risk | Impact | Mitigation |
|------|------|---------|
| Steep learning curve | Users give up using | Provide detailed documentation, video tutorials, example projects |
| Unfamiliar with Requirements format | Write wrong format, validation fail | Provide templates, AI assisted generation |
| Do not understand specs/changes concepts | Use wrong directory, confuse truth and proposal | Clear documentation explanation, tool automated check |

### 7.3 Methodology Risks

| Risk | Impact | Mitigation |
|------|------|---------|
| Too strict restrictions on creative freedom | Users feel constrained | Emphasize methodology is tool not shackle, can be flexibly adjusted |
| OpenSpec methodology not suitable for novels | Core assumption error | Adjust through actual verification, improve methodology if necessary |
| AI does not understand specs format | Efficiency improvement failure | Optimize prompt, provide AI training data |

---

## VIII. Appendix

### 8.1 Glossary

| Term | Description |
|------|------|
| **novelspec** | Command prefix and directory name of this tool |
| **specs/** | Established novel specs (Single Source of Truth) |
| **changes/** | Change proposals to be written |
| **Requirement** | Requirement item in specs, expressed using SHALL/MUST |
| **Scenario** | Verifiable scenario of requirement, using WHEN/THEN format |
| **Delta** | Change increment, marked using ADDED/MODIFIED/REMOVED |
| **Proposal** | Change proposal, explaining Why/What/Impact |
| **Archive** | Archive of completed changes |

### 8.2 Example Project

Complete example project structure ("Star Dream" Fantasy Novel):

```
star-dream-novel/
├── novelspec/
│   ├── project.md
│   ├── AGENTS.md
│   ├── specs/
│   │   ├── characters/
│   │   │   ├── protagonist/spec.md      # Chen Fan
│   │   │   ├── heroine/spec.md          # Lin Xi
│   │   │   └── supporting/
│   │   │       ├── mentor/spec.md       # Elder Yun
│   │   │       └── villain/spec.md      # Li Jian
│   │   ├── worldbuilding/
│   │   │   ├── magic-system/spec.md     # Cultivation System
│   │   │   ├── geography/spec.md        # Qingyun Sect Geography
│   │   │   └── factions/spec.md         # Sect Factions
│   │   └── outline/spec.md              # Outline for Chapters 1-20
│   └── changes/
│       ├── add-chapter-21-30/           # Active change
│       └── archive/
│           ├── 2025-01-20-add-chapter-1-10/
│           └── 2025-01-22-add-chapter-11-20/
├── chapters/
│   ├── volume-1/
│   │   ├── chapter-001.md (3,200 words)
│   │   ├── chapter-002.md (3,500 words)
│   │   └── ... (to chapter-020.md)
│   └── volume-2/
│       └── chapter-021.md (In progress)
└── docs/
    ├── PRD.md
    └── workflow-guide.md
```

### 8.3 References

- **OpenSpec Official Documentation**: https://github.com/Fission-AI/OpenSpec
- **Novel-Writer Project**: github.com/wordflowlab/novel-writer (Reference comparison)
- **Spec-Kit Methodology**: Predecessor of OpenSpec, similar concept

### 8.4 Changelog

| Version | Date | Content |
|------|------|---------|
| 1.0 | 2025-01-22 | Initial version, defining core functions and architecture |

---

**End of Document**
