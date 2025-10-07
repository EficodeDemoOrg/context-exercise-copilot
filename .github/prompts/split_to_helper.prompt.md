---
description: "Delegates a complex sub-part of a task to a helper agent"
mode: Implementer
tools: ['edit', 'runNotebooks', 'search', 'new', 'runCommands', 'runTasks', 'usages', 'vscodeAPI', 'problems', 'changes', 'testFailure', 'openSimpleBrowser', 'fetch', 'githubRepo', 'extensions', 'todos']
---
Create a self-contained sub-task when current implementation is too complex for single execution.

⚠️ **USE ONLY WHEN**: Task requires unrelated operations that would pollute context

⚠️ **MANDATORY TOOL**: You MUST use the #todo tool to track the delegation process.

**Before starting, create your TODO list:**
```
#todo
- [ ] Identify work that needs delegation
- [ ] Define sub-task scope
- [ ] Create helper task file
- [ ] Prepare context requirements
- [ ] Generate delegation request
```

# WORKFLOW

## Step 1: Identify Splittable Work

Valid reasons to split:
- 🔍 **Research Required**: Need to search for configuration/naming/values
- 🏗️ **Parallel Work**: Independent component that doesn't affect current task
- 🔧 **Different Context**: Requires different files/tools than main task
- 📦 **Self-Contained Feature**: Complete mini-feature within the task

Invalid reasons (DO NOT SPLIT):
- ❌ Task is just long (but sequential)
- ❌ You don't understand instructions (use /ask_advice)
- ❌ There are errors (debug them)

## Step 2: Define Sub-Task Scope

Determine:
- What specific work to delegate
- What files helper will need
- What helper should return/report
- How result integrates with main task

## Step 3: Generate Helper Task

Create this structure:

```markdown
# HELPER TASK: [Descriptive Name]

## Context
**Parent Task**: docs/epic_[name]/tasks/[NN_parent_task].md
**Delegation Reason**: [Why this is being split out]
**Integration Point**: [How result fits back]

## Objective
[Single clear sentence of what helper must accomplish]

## Constraints
- DO NOT modify: [files parent task owns]
- MUST follow pattern from: [reference file]
- MUST return: [specific information/confirmation]

## Implementation Instructions

### Step 1: [Specific action]
File: `path/to/file`
Operation: [CREATE|MODIFY|SEARCH]

[Specific instructions, code snippets if needed]

### Step 2: [Next action]
[Continue as needed]

## Verification Checklist
- [ ] [Specific thing to verify]
- [ ] [Another verification]
- [ ] Result can be integrated with parent task

## Definition of Done
- [ ] Core objective achieved
- [ ] No side effects on parent task files
- [ ] Clear output/result provided

## Return Protocol
Upon completion, provide:
1. Status: [SUCCESS|PARTIAL|FAILED]
2. Output: [What was created/found/modified]
3. Integration notes: [How parent task should proceed]

---
*This is a helper task delegated from a main implementation task*
```

## Step 4: Handoff Instructions

Generate for current session:
```markdown
## 🤝 HELPER TASK DELEGATION

I've created a helper task above for a specific sub-component.

### Why Delegation Needed
[Specific reason - research/parallel work/different context]

### Current Status
Main task progress:
- ✅ Completed: Steps 1-N
- 🔄 Delegating: [Specific part]
- ⏸️ Paused: Steps N+1 onward

### To Execute Helper
1. Copy the helper task above
2. Start new Implementer session
3. Provide helper task as input
4. Helper will execute and report back

### After Helper Completes
Return here with helper's output to continue main task.
I need from helper:
- [Specific information/confirmation]

### If Helper Fails
We can either:
1. Try different approach
2. Escalate to Lead Developer
3. Proceed without that component

---
Waiting for helper task completion before continuing...
```

## Step 5: Write Helper Task to File

Also save helper task:
```typescript
// Create helper task file
const helperPath = 'docs/epic_[name]/tasks/[NN]a_helper_[description].md';
// Write helper task content to file
```

Output:
```
📁 Helper task saved to: docs/epic_[name]/tasks/[NN]a_helper_[description].md

You can now:
1. Run helper in new session with that file
2. Or copy the task above to another Implementer
```

## Important Notes

When helper returns, you should:
1. Verify helper output matches expectations
2. Integrate results into main task
3. Continue main task implementation
4. Include helper results in final report

Helper task should be:
- Completely self-contained
- Under 10k tokens of context
- Executable without main task knowledge
- Clear about what to return
```