---
mode: Lead Developer
description: "Generate completion report for Architect review"
---
Generate completion report after all implementation tasks are done.

⚠️ **REQUIRED CONTEXT**: User must attach:
- The epic's ADR file  
- `docs/epic_<epic_name>/plans/IMPLEMENTATION_PLAN.md`
- `docs/epic_<epic_name>/MANIFEST.md`

⚠️ **MANDATORY TOOL**: You MUST use the #todo tool to track the report generation process.

**Before starting, create your TODO list:**
```
#todo
- [ ] Read all required context files
- [ ] Extract deliverables and metrics
- [ ] Verify ADR requirements met
- [ ] Generate COMPLETION_REPORT.md
- [ ] Present report to user
```

# OUTPUT GENERATION

**MANDATORY OUTPUT FILE**: `docs/epic_<epic_name>/COMPLETION_REPORT.md`

```markdown
# Epic Completion Report: [Epic Name]
**Date**: [Current date]
**Epic ADR**: docs/ADR/[EPIC]_ADR.md
**Status**: COMPLETE

## Executive Summary
**Planned**: [N] tasks across [M] files
**Executed**: [N] tasks successfully
**Result**: All ADR requirements implemented

## Deliverables
### New Files Created
- `path/to/file.ts` - [Purpose]

### Files Modified  
- `path/to/file.ts` - [Type of change]

## Requirements Verification
| ADR Requirement | Implementation | Task # | Status |
|-----------------|---------------|--------|--------|
| [Requirement from ADR] | [How implemented] | [Task that did it] | ✅ |

## Metrics
- Tasks Completed: [N]/[N]
- Files Created: [X]
- Files Modified: [Y]  
- Total Context Used: ~[Z]k tokens
- Average Context/Task: ~[A]k tokens

## Deviations from Plan
[None | Description of any changes]

## Technical Debt
[None | Items for future consideration]

## Lessons Learned
- [Observation]: [Impact on future epics]

## Architect Action Items
- [ ] Review implementation for architectural compliance
- [ ] Update ROADMAP.md to mark epic complete
- [ ] Consider follow-up epics for: [suggestions]

---
*Generated from implementation artifacts in docs/epic_[epic_name]/*
```

Also output to console:
```
=== EPIC COMPLETION SUMMARY ===
Epic: [Name]
Status: ✅ COMPLETE
Tasks: [N]/[N] completed
Deliverables: [X] new files, [Y] modified files
Report: docs/epic_[epic_name]/COMPLETION_REPORT.md
```