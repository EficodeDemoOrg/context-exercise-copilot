---
mode: agent
tools: ['edit', 'runNotebooks', 'search', 'new', 'runCommands', 'runTasks', 'usages', 'vscodeAPI', 'problems', 'changes', 'testFailure', 'openSimpleBrowser', 'fetch', 'githubRepo', 'extensions', 'todos']
description: "Critical context handoff protocol for seamless continuation in new agent instance"
---
Execute the **THREAD DUMP PROTOCOL** to preserve critical context for continuation.

⚠️ **CRITICAL**: You are about to generate a handoff briefing. Follow this template EXACTLY.

⚠️ **MANDATORY TOOL**: You MUST use the #todo tool to track the thread dump process.

**Before starting, create your TODO list:**
```
#todo
- [ ] Acknowledge thread dump initiation
- [ ] Generate context handoff briefing
- [ ] Document current task state
- [ ] List work completed
- [ ] Specify next steps
- [ ] Provide continuation instructions
```

# EXECUTION PROTOCOL

## Step 1: Acknowledge the Situation
Output EXACTLY this line first:
```
🚨 THREAD DUMP INITIATED - Preparing context handoff...
```

## Step 2: Generate the Handoff Briefing

Output the following template DIRECTLY in chat. DO NOT wrap in code fences. DO NOT create a file.
Fill in each section with relevant information from our current session:

---

# 🔄 CONTEXT HANDOFF BRIEFING

**Previous Agent**: [Initializer|Architect|Lead Developer|Implementer]
**Previous Command**: [e.g., /lead_research, /implement, etc.]
**Workflow Phase**: [e.g., Step 3 of 5 in research phase]
**Timestamp**: [Current date/time]

## 1. PRIMARY MISSION
[State the overarching goal in ONE sentence - what were we trying to accomplish?]

## 2. ACTIVE CONTEXT

### Current Epic/Task
- **Epic**: [Name if in Lead Developer/Implementer mode]
- **Task File**: [Exact path if Implementer, e.g., docs/epic_auth/tasks/01_create_slice.md]
- **Task Status**: [Not Started|In Progress|Verification Phase|Complete]

### Key Files Under Work
| File Path | Status | Purpose |
|-----------|--------|---------|
| [path/to/file] | [Created|Modified|Reading] | [Why this file matters] |

### Project State Files
**These MUST be attached to continue:**
- `CONSTITUTION.md` - Project technical foundation
- `docs/ROADMAP.md` - Current epic: [X of 5]
- [Other critical files specific to current work]

## 3. WORK COMPLETED

### Session Accomplishments
✅ [Major achievement 1]
✅ [Major achievement 2]
✅ [Decision made]

### Code Changes Made
- Created: [List new files]
- Modified: [List changed files with brief description]
- Uncommitted changes: [Yes/No - if Yes, list files]

## 4. IMMEDIATE CONTINUATION

### You Were About To:
[SPECIFIC action that was interrupted - be precise]

### Next Steps (in order):
1. [Most immediate action - usually continuing from interruption point]
2. [Following action]
3. [Subsequent action if applicable]

### Required Context for Next Steps:
- Attach: [specific file needed]
- Read: [specific section or line numbers]
- Consider: [any constraints or decisions already made]

## 5. CRITICAL CONSTRAINTS

### Do NOT:
❌ [Specific thing to avoid]
❌ [Rejected approach from earlier]
❌ [Technical limitation discovered]

### MUST Follow:
✅ [Specific pattern or convention]
✅ [Architectural decision already made]
✅ [User preference stated]

## 6. DEPENDENCIES & BLOCKERS

### Completed Dependencies:
- [Task/Epic that this work depends on]

### Pending Dependencies:
- [What still needs to be done by others]

### Known Issues:
- [Any blockers or problems discovered]

---

## 📋 CONTINUATION INSTRUCTIONS FOR USER

To continue this work:

1. **Copy this entire briefing** (everything above the line)
2. **Start a NEW chat session**
3. **Select chatmode**: [Exact mode to use]
4. **Attach these files**:
   - [List exact files needed for continuation]
5. **Paste the briefing** as your first message
6. **Add this instruction**: "Continue from this context handoff. Acknowledge you understand the context, then proceed with the immediate next step."

The new agent should acknowledge understanding and continue from the interruption point.

---

## Step 3: Confirm Handoff Complete

After outputting the briefing, add:

```
✅ Thread dump complete. Session ending.
Please follow the continuation instructions above to resume work.
```

# VALIDATION CHECKLIST

Before outputting, verify you have included:
- [ ] Current agent role and command
- [ ] Specific task/epic being worked on
- [ ] Files that were created/modified
- [ ] The EXACT next action to take
- [ ] Critical constraints discovered
- [ ] Clear continuation instructions

# EXAMPLE OUTPUT (DO NOT COPY - FOR REFERENCE ONLY)

```
🚨 THREAD DUMP INITIATED - Preparing context handoff...

# 🔄 CONTEXT HANDOFF BRIEFING

**Previous Agent**: Implementer
**Previous Command**: /implement
**Workflow Phase**: Step 2 of 4 in task implementation
**Timestamp**: 2024-01-15 14:35

## 1. PRIMARY MISSION
Implement the Context Window Visualizer's state management system as defined in Epic 1.

## 2. ACTIVE CONTEXT

### Current Epic/Task
- **Epic**: foundation_setup
- **Task File**: docs/epic_foundation/tasks/02_create_state_slice.md
- **Task Status**: In Progress

### Key Files Under Work
| File Path | Status | Purpose |
|-----------|--------|---------|
| src/store/contextSlice.ts | Created | Redux slice for context state |
| src/store/index.ts | Modified | Register new reducer |

[... rest of example ...]
```

# ERROR HANDLERS

If you cannot complete the dump:
```
⚠️ THREAD DUMP FAILED
Reason: [Specific reason]
Alternative: Start fresh with [suggested agent] and provide [key context manually]
```