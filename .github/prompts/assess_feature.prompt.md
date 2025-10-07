---
mode: Architect
description: "Assess new feature impact on existing architecture and update roadmap"
---
Execute this feature assessment workflow precisely:

⚠️ **MANDATORY TOOL**: You MUST use the #todo tool to track progress through the assessment workflow. Update the todo list as you complete each phase.

**Before starting, create your TODO list:**
```
#todo
- [ ] Phase 1: Read CONSTITUTION.md
- [ ] Phase 1: Read INITIAL_ARCHITECTURE_ADR.md
- [ ] Phase 1: Read ROADMAP.md
- [ ] Phase 1: Read all other ADRs
- [ ] Phase 2: Request feature details from user
- [ ] Phase 3: Analyze architectural impact
- [ ] Phase 3: Identify required changes
- [ ] Phase 4: Determine epic placement
- [ ] Phase 5: Generate new ADR
- [ ] Phase 5: Update ROADMAP.md
- [ ] Verify all changes complete
```

# PHASE 1: CONTEXT GATHERING

1. Read these files in order:
   - `CONSTITUTION.md` (foundational rules)
   - `docs/ADR/INITIAL_ARCHITECTURE_ADR.md` (current architecture)
   - `docs/ROADMAP.md` (development plan)
   - All other ADRs in `docs/ADR/` (past decisions)

2. Create mental model of:
   - Current architectural state
   - Planned evolution
   - Decision history

# PHASE 2: FEATURE REQUEST

Ask the user:
> "What feature would you like me to assess? Please describe:
> 1. The feature's purpose
> 2. Expected user interaction
> 3. Any specific requirements or constraints"

Wait for complete response before proceeding.

# PHASE 3: IMPACT ANALYSIS

Analyze the feature across these dimensions:

## Architectural Fit Assessment
- **Component Impact**: Which existing components need modification?
- **New Components**: What new components are required?
- **State Model Changes**: How does this affect the state architecture?
- **Data Flow Changes**: New data paths or modifications needed?

## Risk Assessment
- **Breaking Changes**: Could this break existing functionality?
- **Performance Impact**: Will this degrade performance?
- **Complexity Cost**: How much architectural complexity does this add?
- **Technical Debt**: What shortcuts might be tempting but dangerous?

## Dependency Analysis
- **Prerequisite Epics**: Which roadmap items must complete first?
- **Parallel Work**: What can be developed simultaneously?
- **Future Conflicts**: What planned features might this complicate?

# PHASE 4: RECOMMENDATION

Based on analysis, provide one of these verdicts:

## ✅ GREEN LIGHT
"This feature aligns well with current architecture. Minimal structural changes required."

## ⚠️ YELLOW LIGHT  
"This feature is feasible but requires careful implementation to avoid architectural degradation."

## 🛑 RED LIGHT
"This feature conflicts with architectural principles or would require major restructuring."

# PHASE 5: DOCUMENTATION UPDATES

## Update docs/ROADMAP.md

If GREEN or YELLOW:
- Insert new epic in appropriate sequence
- Adjust dependencies of subsequent epics
- Add note: `"[Added on DATE]: [Feature] based on architectural assessment"`

If RED:
- Add to new section "Deferred Features" with explanation

## Create docs/ADR/[FEATURE]_ADR.md

Use this template:
```markdown
# [Feature Name] Architecture Decision Record

## Date
[Current date]

## Status
Accepted / Rejected / Deferred

## Context
User requested: [Original request summary]

## Architectural Analysis

### Component Changes
[Detailed list]

### State Model Impact
[Detailed analysis]

### Data Flow Modifications
[Detailed changes]

## Decision
[What we're doing and why]

## Consequences

### Positive
- [Benefit]

### Negative  
- [Tradeoff]

### Risks
- [Risk]: Mitigation: [Strategy]

## Implementation Notes
[Key considerations for developers]

## Alternatives Considered
- [Alternative]: Rejected because [reason]

## Constitution Alignment Check
✓/✗ [Constitution principle]: [How this aligns or conflicts]
```

# PHASE 6: SUMMARY

Present to user:
> "Feature assessment complete. I've:
> 1. [Updated/Did not update] ROADMAP.md [with reason]
> 2. Created ADR documenting the architectural impact
> 3. Recommendation: [GREEN/YELLOW/RED with one-line summary]
> 
> Would you like me to explain any specific aspect of this assessment?"