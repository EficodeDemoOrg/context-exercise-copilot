---
mode: Architect
description: "Generate initial architectural blueprint from project constitution"
tools: ['edit', 'runNotebooks', 'search', 'new', 'runCommands', 'runTasks', 'usages', 'vscodeAPI', 'problems', 'changes', 'testFailure', 'openSimpleBrowser', 'fetch', 'githubRepo', 'extensions', 'todos']
---
Create the foundational architecture for this project following this exact workflow:

⚠️ **MANDATORY TOOL**: You MUST use the #todo tool to track progress through all 4 phases. Update the todo list as you complete each step.

**Before starting, create your TODO list:**
```
#todo
- [ ] Phase 1: Read and analyze CONSTITUTION.md
- [ ] Phase 1: Extract technology constraints
- [ ] Phase 1: Identify conflicts/ambiguities
- [ ] Phase 2: Design component architecture
- [ ] Phase 2: Design state architecture
- [ ] Phase 2: Design data flow
- [ ] Phase 3: Structure 5 development epics
- [ ] Phase 4: Generate docs/ROADMAP.md
- [ ] Phase 4: Generate docs/ADR/INITIAL_ARCHITECTURE_ADR.md
- [ ] Verify all files created successfully
```

# PHASE 1: CONSTITUTION ANALYSIS
1. Read `CONSTITUTION.md` completely
2. Extract and list:
   - Technology constraints
   - Architectural patterns chosen
   - Development practices mandated
3. Identify any potential conflicts or ambiguities

# PHASE 2: ARCHITECTURAL DESIGN

## Component Architecture
Define the application's component hierarchy:
```
Example structure:
- AppRoot
  ├─ NavigationBar
  ├─ MainContent
  │  ├─ ContextPanel
  │  └─ VisualizationArea
  └─ StatusBar
```

## State Architecture
Map out the state model based on constitution's state management choice:
- Global state shape
- Local component state boundaries
- State update patterns
- Side effect handling

## Data Flow Design
Document how data moves through the system:
1. User interaction points
2. State mutations
3. Component re-render triggers
4. External API interactions (if any)

# PHASE 3: ROADMAP CREATION

Structure exactly 5 development epics in logical sequence:

1. **Foundation Epic**: Core infrastructure setup
2. **[Domain Epic 1]**: First major feature area
3. **[Domain Epic 2]**: Second major feature area
4. **[Integration Epic]**: System integration points
5. **[Polish Epic]**: Performance, UX refinement

Each epic must include:
- Objective (1 sentence)
- Key deliverables (3-5 items)
- Dependencies on previous epics

# PHASE 4: FILE GENERATION

## Generate docs/ROADMAP.md
```markdown
# Development Roadmap

## Epic 1: [Name]
**Objective**: [Clear goal]
**Deliverables**:
- [ ] [Specific deliverable]
- [ ] [Specific deliverable]
**Dependencies**: None / Epic X

[Continue for all 5 epics]

## Architecture Compliance
This roadmap aligns with CONSTITUTION.md by:
- [Specific alignment point]
- [Specific alignment point]
```

## Generate docs/ADR/INITIAL_ARCHITECTURE_ADR.md
```markdown
# Initial Architecture Decision Record

## Context
Based on CONSTITUTION.md established on [date], this ADR defines the foundational architecture.

## Decision

### Component Architecture
[Your design with justification]

### State Management Architecture
[Your design with justification]

### Data Flow Architecture
[Your design with justification]

## Consequences

### Positive
- [Specific benefit]
- [Specific benefit]

### Negative
- [Specific tradeoff]
- [Specific limitation]

## Alternatives Considered
- [Alternative]: Rejected because [reason]

## Compliance Verification
- Constitution requirement: [X] → Architecture implements: [Y]
- Constitution requirement: [X] → Architecture implements: [Y]
```

STOP after generating these two files. Do not proceed to implementation.