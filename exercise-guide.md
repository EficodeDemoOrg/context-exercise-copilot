# Introduction

This guide walks you through building the Context Window Visualizer project using the multi-agent development workflow. You'll direct specialized AI agents through different phases, from project initialization to implementing your first epic.

**Key Principle:** Use a fresh chat session for each agent interaction. The agents don't share memory—all project state lives in markdown files that you pass between them.

## Prerequisites

- VS Code with GitHub Copilot installed
- `.github/chatmodes` and `.github/prompts` directories set up with agent definitions
- Basic understanding of attaching files in Copilot chat (use `@` to reference files)

## Model Recommendations

Different agents work best with different AI modelsß

- **Initializer & Architect**: Gemini 2.5 Pro, Claude Sonnet 3.5/4, or GPT-5 (your preference)
- **Lead Developer**: Claude Sonnet 4/4.5 (better at detailed planning and research)
- **Implementer**: Claude Sonnet 4/4.5 (superior code generation and precision)

## ⚠️ Critical: Chat Thread Behavior

**VS Code Copilot has a gotcha:** When you switch between chat threads, the chatmode and model selection do NOT carry over. If you start a thread with "Architect" mode, switch to work on "Implementer", then return to the Architect thread—it will still have **Implementer** mode and model selected.

**Always verify before running a prompt:**
1. Check the chatmode selector shows the correct agent
2. Check the model selector shows your preferred model for that agent
3. Manually switch back if needed
ß
This is current VS Code behavior and easy to miss!ide: Building the Context Window Visualizer

## Introduction

This guide walks you through building the Context Window Visualizer project using the multi-agent development workflow. You'll direct specialized AI agents through different phases, from project initialization to implementing your first epic.

**Key Principle:** Use a fresh chat session for each agent interaction. The agents don't share memory—all project state lives in markdown files that you pass between them.

## Prerequisites

- VS Code with GitHub Copilot installed
- chatmodes and prompts directories set up with agent definitions
- Basic understanding of attaching files in Copilot chat (use `@` to reference files)

## Phase 1: Initialize the Project

### Step 1: Create the Constitution

1. Start a **new chat session**
2. Select the **Initializer** chatmode
3. Attach the README.md: `@README.md`
4. Run: `/init_project`

The Initializer will conduct a 12-question interview about your technical choices. For this project, JavaScript/TypeScript with React is recommended, but you can choose your preferred stack.

**Your responsibility:** Answer all 12 questions thoughtfully. These decisions will guide every subsequent agent.

Once complete, you'll have `CONSTITUTION.md` with your technical decisions.

**If it fails:** The agent might skip questions (blame the prompt author). Tell it explicitly: "You missed questions X, Y, Z. Please ask them now."

### Step 2: Enrich the Constitution

1. Keep the same chat or start fresh with **Initializer** mode
2. Attach the `CONSTITUTION.md` you just created
3. Run: `/enrich_constitution`

The agent will propose comprehensive coding standards, error handling patterns, security practices, and more based on your tech stack.

**Your responsibility:** Review the proposed enhancements. You can:
- Accept all proposals
- Request modifications to specific sections
- Remove sections you don't want

The enriched `CONSTITUTION.md` becomes the project's definitive guide.

## Phase 2: Create the Architecture

### Step 3: Generate Blueprint and Roadmap

1. Start a **new chat session**
2. Select the **Architect** chatmode
3. Attach your `CONSTITUTION.md`
4. Run: `/create_blueprint`

The Architect will:
- Design the component architecture
- Define the state management approach
- Create a 5-epic ROADMAP.md
- Generate an Initial Architecture ADR

**Your responsibility:** 
- **READ** the proposed architecture carefully
- Verify the epics make sense for the Context Visualizer project
- Check that the architecture aligns with your Constitution
- Ensure Epic 1 is a reasonable starting point (usually "Foundation" or "Setup")

Output files:
- `docs/ROADMAP.md` - Your development plan
- `docs/ADR/INITIAL_ARCHITECTURE_ADR.md` - Architectural decisions

## Phase 3: Research and Plan Epic 1

### Step 4: Research the First Epic

1. Start a **new chat session**
2. Select the **Lead Developer** chatmode
3. **Set model to Claude Sonnet 4 or 4.5** (recommended for planning tasks)
4. Attach:
   - `CONSTITUTION.md`
   - `docs/ADR/INITIAL_ARCHITECTURE_ADR.md`
   - The first epic's ADR (if Architect created one)
   - Any existing code files relevant to the epic
4. Run: `/lead_research`

The Lead Developer will investigate:
- What files need to be created/modified
- What patterns to follow
- Technical specifications needed
- Integration points

**Your responsibility:**
- **READ** the research output thoroughly
- Check if the research makes sense
- Verify file paths are correct
- If something seems wrong, tell the agent or tweak the prompt

Output: `docs/epic_[name]/research/RESEARCH.md`

### Step 5: Create Implementation Tasks

1. Continue with the same **Lead Developer** session (or start new)
2. Attach:
   - The epic's ADR
   - `docs/epic_[name]/research/RESEARCH.md`
3. Run: `/lead_plan`

The Lead Developer will:
- Create an implementation plan
- Generate numbered task files (01_task_name.md, 02_task_name.md, etc.)
- Document decisions in a decision log
- Create a task manifest

**Task numbering:** Tasks are numbered sequentially (01, 02, 03...) to enforce execution order. Each task is designed to be completed without blocking on others.

**Your responsibility:**
- Read each task file to ensure it makes sense
- Verify tasks are small enough (each should be completable in one session)
- Check that file paths use project root (`/`) not placeholders

Output files in `docs/epic_[name]/`:
- `plans/IMPLEMENTATION_PLAN.md`
- `plans/DECISION_LOG.md`
- `tasks/01_[name].md`, `tasks/02_[name].md`, etc.
- `MANIFEST.md`

## Phase 4: Implement the Tasks

### Step 6: Execute the First Task

1. Start a **new chat session**
2. Select the **Implementer** chatmode
3. **Set model to Claude Sonnet 4 or 4.5** (best for precise code generation)
4. Attach the first task file: `docs/epic_[name]/tasks/01_[task_name].md`
5. Run: `/implement`

The Implementer will:
- Read and summarize what it plans to do
- List all files it will create/modify
- Ask for your approval to proceed

**Your responsibility:**
- Review the implementation plan
- Confirm it matches the task specification
- Approve with "yes" or request clarification

Once approved, the Implementer will:
- Execute the task step by step
- Run linter on modified files
- Execute tests if applicable
- Report completion status

### Step 7: Handle Implementation Issues

**If the task succeeds:**
- Review the code changes
- Commit when the Implementer confirms all checks pass
- Move to the next task (repeat Step 6 with `02_[task_name].md`)

**If verification fails:**
- Read the Implementer's explanation
- Minor issues: Let it proceed if non-critical items failed
- Major issues: The Implementer will use `/ask_advice`

**If the Implementer gets blocked:**
The agent will present an escalation request with:
- What went wrong
- What was attempted
- Proposed solutions

You can:
- Approve a proposed solution
- Provide alternative approach
- Modify the task specification
- Abort and go back to Lead Developer for task revision

### Step 8: Complete Remaining Tasks

Repeat Step 6 for each task file in sequence (02, 03, etc.) until all tasks in the epic are complete.

**Important:** Each task should be run in a fresh Implementer session with just that task file as context.

## Phase 5: Complete the Epic

### Step 9: Report Epic Completion

After the last task succeeds:

1. Stay in **Implementer** mode or start new session
2. Attach:
   - The epic's ADR
   - `docs/epic_[name]/plans/IMPLEMENTATION_PLAN.md`
   - `docs/epic_[name]/MANIFEST.md`
3. Run: `/report_to_lead`

The Implementer generates a completion report with:
- Summary of work completed
- Any deviations from plan
- Recommendations for future epics

### Step 10: Update the Roadmap

1. Start a **new chat session**
2. Select the **Architect** chatmode
3. Attach:
   - `docs/ROADMAP.md`
   - The completion report from Step 9
4. Ask the Architect to update the ROADMAP marking Epic 1 as complete

## Troubleshooting: When a Prompt Fails to Perform

Sometimes an agent won't follow its prompt correctly—it skips questions, ignores instructions, or produces incomplete output. When this happens, don't just retry. Instead, use this systematic approach to fix the prompt itself:

### The Prompt Debugging Workflow

**Step 1: Stop and Document**
- Don't continue with the broken session
- Note exactly what went wrong:
  - What the prompt should have done
  - What the agent actually did
  - Which steps were skipped or incorrect

**Step 2: Start a Fresh Debugging Session**
1. Open a **new chat session**
2. Select **Ask** mode (not the agent that failed)
3. **Choose a high-powered model:**
   - **Recommended:** Claude Sonnet 4 or 4.5 (excellent at analysis)
   - **Alternative:** GPT-4o, Gemini 2.0 Flash, or best available
4. Attach the problematic prompt file (e.g., `.github/prompts/Init Project.prompt.md`)

**Step 3: Explain the Problem**
Tell the model:
```
This prompt isn't working as expected.

What I expected: [describe the correct behavior]

What actually happened: [describe what went wrong]

The prompt file is attached. Please analyze it and ask me clarifying 
questions about what needs to be fixed.
```

**Step 4: Collaborate on the Fix**
- Answer the model's clarifying questions
- Discuss what instructions are unclear or missing
- Review the model's proposed improvements
- Iterate until you have a clear fix

**Step 5: Generate the Updated Prompt**
Once you've agreed on the changes:
1. **Switch to Opus 4.1** if available (superior for precise generation)
2. Or stay with Claude Sonnet 4/4.5 if Opus isn't available
3. Ask it to generate the complete updated prompt
4. Review carefully—ensure all changes are incorporated
5. Update the prompt file

**Step 6: Test the Fixed Prompt**
1. Start a **new session** with the appropriate agent mode
2. Run the updated prompt
3. Verify it now behaves correctly
4. If issues remain, repeat from Step 2

### Example: Fixing the Initializer

**Problem:** The Initializer skipped questions 7-9 in the interview.

**Debug Session (Claude Sonnet 4):**
```
This /init_project prompt isn't working. It should ask all 12 questions
sequentially, but it jumped from question 6 to question 10, skipping 
questions 7, 8, and 9 entirely.

The prompt is attached. What might be causing this and how can we fix it?
```

The model analyzes and asks:
- "Are the questions in distinct sections that might confuse it?"
- "Does the prompt have explicit counters and checkpoints?"
- "Is there ambiguity in the progression logic?"

After discussion, you identify the issue and agree on improvements.

**Generation Phase (Switch to Opus 4.1 if available):**
```
Based on our analysis, please generate the updated prompt with:
1. Explicit progress counters after each question
2. Mandatory checkpoint validations between sections
3. Clearer instructions about sequential execution
```

Review the output, update the file, and test again.

### Model Recommendations for Troubleshooting

**Analysis Phase (Step 2-4):**
- **Best:** Claude Sonnet 4 or 4.5 (excellent reasoning and clarifying questions)
- **Alternative:** GPT-4o, Gemini 2.0 Flash (if Claude unavailable)

**Generation Phase (Step 5):**
- **Best:** Claude Opus 4.1 (superior precision and completeness)
- **Fallback:** Claude Sonnet 4/4.5 (still very good)
- **Note:** Use what's available to you—Sonnet 4/4.5 can handle both phases

## What To Do If...

### The agent skips steps or questions
- Use the **Prompt Debugging Workflow** above to fix the prompt
- Explicitly tell it what it missed as a temporary workaround
- Reference the specific requirement from the prompt
- Don't rely on verbal corrections—fix the prompt file itself

### An epic seems too large
- Go back to Architect mode
- Ask it to split the epic into smaller ones
- Or proceed to Lead Developer and let it create more granular tasks

### A task is too complex for Implementer
- Use `/split_to_helper` to delegate part of it
- Or abort and go back to Lead Developer for better task decomposition

### Context window issues arise
- Agent becomes repetitive or confused
- Performance degrades
- **Use `/thread_dump`** to generate a handoff briefing
- Copy the briefing and start a fresh session with it
- Or use smaller task files and start fresh sessions more frequently

### The agent hallucinates or makes things up
- Stop immediately
- Verify against the Constitution and ADRs
- Provide explicit correction
- Start a new session with correct context

## Moving Forward

After Epic 1 completes successfully:

1. Return to **Architect** mode for the next epic
2. The workflow repeats: Research → Plan → Implement → Report
3. Each epic builds on the previous work
4. Always reference the Constitution and Architecture ADRs

Remember: The agents are probabilistic and will sometimes need correction. Your job is to guide them, validate their output, and maintain project coherence through careful review of all generated documentation.

## Tips for Success

- **One agent, one task, one chat session** - Don't mix contexts
- **Double-check chatmode and model** - Every time you switch threads, verify they're correct
- **Use Claude Sonnet 4/4.5 for implementation** - It's superior for code generation and detailed planning
- **Use `/thread_dump` when stuck** - If agent loses context or becomes confused, dump and restart fresh
- **Read everything** - The agents generate detailed documentation for a reason
- **Commit frequently** - After each successful task or epic
- **Trust but verify** - Agents follow patterns but can make mistakes
- **When in doubt, escalate** - Go back to higher abstraction levels

This experimental system will evolve. When you find issues, use Copilot to improve the prompts and share your enhancements with the community.