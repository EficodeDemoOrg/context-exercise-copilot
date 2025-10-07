---
mode: Lead Developer
description: "Conduct comprehensive technical research for epic implementation"
---
Execute this research workflow to eliminate all unknowns before planning.

⚠️ **REQUIRED CONTEXT**: User must attach:
- `CONSTITUTION.md`
- `docs/ADR/INITIAL_ARCHITECTURE_ADR.md`
- The specific epic's ADR file
- Any relevant existing code files

⚠️ **MANDATORY TOOL**: You MUST use the #todo tool to track progress through the research workflow. Update the todo list as you complete each category.

**Before starting, create your TODO list:**
```
#todo
- [ ] Phase 1: Identify epic name from ADR
- [ ] Phase 1: Create directory structure
- [ ] Phase 2: Research codebase patterns
- [ ] Phase 2: Research dependencies
- [ ] Phase 2: Research integration points
- [ ] Phase 2: Research state management
- [ ] Phase 2: Research testing approach
- [ ] Phase 2: Research error handling
- [ ] Phase 3: Identify implementation risks
- [ ] Phase 4: Generate RESEARCH.md
- [ ] Verify research document complete
```

# PHASE 1: CONTEXT ANALYSIS

1. Identify the epic name from the provided ADR
2. Create directory structure:
   ```bash
   mkdir -p docs/epic_<epic_name>/research
   mkdir -p docs/epic_<epic_name>/plans
   mkdir -p docs/epic_<epic_name>/tasks
   ```

# PHASE 2: RESEARCH EXECUTION

Investigate these categories systematically:

## Code Location Research
- Map ALL files that need modification
- Find exact line numbers for insertions/changes
- Identify import paths and dependencies
- Document existing patterns in those files

## Implementation Pattern Research
- Find similar implementations in codebase
- Document conventions used (naming, structure, patterns)
- Identify reusable components/utilities

## Technical Specification Research
- List exact APIs/methods needed
- Document function signatures
- Find performance considerations
- Identify error handling patterns

## Integration Research
- Map component connections
- Document state management touchpoints
- Trace data flow paths
- Find event handlers and listeners

# PHASE 3: OUTPUT GENERATION

**MANDATORY OUTPUT FILE**: `docs/epic_<epic_name>/research/RESEARCH.md`

Use this exact format:

```markdown
# Research Report: [Epic Name]
Generated: [Date]
Epic ADR: docs/ADR/[EPIC_NAME]_ADR.md

## Executive Summary
[2-3 sentences summarizing key findings and approach]

## File Mapping

### Files Requiring Modification
| File Path | Lines | Operation | Purpose |
|-----------|-------|-----------|---------|
| `src/components/App.tsx` | 45-67 | Modify | Add new route handler |
| `src/store/index.ts` | 12-15 | Modify | Register new reducer |

### New Files Required
| File Path | Purpose | Template Source |
|-----------|---------|-----------------|
| `src/features/[epic]/index.ts` | Feature entry point | `src/features/example/index.ts` |

## Code Insertion Points

### File: `src/components/App.tsx`
**Current State (Lines 45-50):**
```typescript
const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About }
];
```
**Insertion Point**: After line 47
**Pattern to Follow**: Existing route structure

### File: `src/store/index.ts`
[Continue for each file...]

## Technical Specifications

### Required APIs
| Method | Source | Purpose | Signature |
|--------|--------|---------|-----------|
| `useSelector` | `react-redux` | Access state | `<T>(selector: (state: RootState) => T): T` |

### State Shape Additions
```typescript
// To be added to RootState
interface NewFeatureState {
  data: DataType[];
  loading: boolean;
  error: string | null;
}
```

## Implementation Patterns Found

### Pattern: Async Action Creators
**Location**: `src/features/users/actions.ts:23-45`
**Usage**: All async operations use this pattern
```typescript
export const fetchData = createAsyncThunk(
  'feature/fetchData',
  async (params: Params) => {
    const response = await api.fetch(params);
    return response.data;
  }
);
```

## Integration Points

### Component Tree Integration
```
App
└── MainLayout
    └── FeatureContainer (NEW)
        ├── FeatureList (NEW)
        └── FeatureDetail (NEW)
```

### State Flow
1. User action in `FeatureContainer`
2. Dispatch action via `dispatch(featureAction())`
3. Reducer updates state in `features/[epic]/slice.ts`
4. Components re-render via `useSelector`

## Dependencies Required
| Package | Version | Purpose | Already Installed |
|---------|---------|---------|-------------------|
| `react-redux` | ^8.0.0 | State management | ✅ Yes |
| `@reduxjs/toolkit` | ^1.9.0 | Redux utilities | ✅ Yes |

## Risk Assessment
| Risk | Severity | Mitigation |
|------|----------|------------|
| State shape conflicts | Low | Use namespaced keys |
| Performance impact | Medium | Implement memoization |

## Implementation Sequence
1. **Create feature directory structure** - No dependencies
2. **Add state slice** - Depends on directory
3. **Create base components** - Depends on state
4. **Wire up routing** - Depends on components
5. **Connect to store** - Depends on all above

## Validation Checklist
- [ ] All file paths verified to exist
- [ ] All line numbers are current
- [ ] Code snippets compile without errors
- [ ] No circular dependencies introduced
- [ ] Pattern consistency maintained


**STATUS**: Research complete. Ready for planning phase.
```