# Introduction

This guide walks you through building the Context Window Visualizer project. It
offers two distinct paths for you to explore different AI-driven development
methodologies:

*   **Path A: The `spec-kit` Workflow** - A streamlined, tool-assisted workflow
    using the `spec-kit`. This path is ideal for learning a structured,
    specification-first approach to development where a tool orchestrates the
    process.
*   **Path B: The Manual Agent Workflow** - A hands-on, role-playing workflow
    where you direct a team of specialized AI agents (`Initializer`,
    `Architect`, `Implementer`). This path is excellent for understanding the
    distinct phases of software development and how different AI specializations
    can contribute.

**Note for Path B:** If you choose Path B, be aware that the "chatmodes"
feature used in this workflow is currently only available in the VS Code
environment. This path requires VS Code with GitHub Copilot installed to access
the specialized AI agent chatmodes.

Choose the path that interests you the most. Both will guide you through
building the same project but with different tools and processes.

## Table of Contents

*   [Path A: The `spec-kit` Workflow](#path-a-the-spec-kit-workflow)
    *   [Phase 1: Initialize the Project](#phase-1-initialize-the-project)
        *   [Step 1: Install the `specify` CLI](#step-1-install-the-specify-cli)
        *   [Step 2: Initialize the Project with `spec-kit`](#step-2-initialize-the-project-with-spec-kit)
    *   [Phase 2: Define Project Principles](#phase-2-define-project-principles)
        *   [Step 3: Create the Constitution](#step-3-create-the-constitution)
    *   [Phase 3: Specify the Application](#phase-3-specify-the-application)
        *   [Step 4: Define the "What"](#step-4-define-the-what)
    *   [Phase 4: Create the Technical Plan](#phase-4-create-the-technical-plan)
        *   [Step 5: Define the "How"](#step-5-define-the-how)
    *   [Phase 5: Generate and Execute Tasks](#phase-5-generate-and-execute-tasks)
        *   [Step 6: Create the Task List](#step-6-create-the-task-list)
        *   [Optional Step: Analyze and Refine](#optional-step-analyze-and-refine)
        *   [Step 7: Execute the Implementation](#step-7-execute-the-implementation)
    *   [Troubleshooting the `spec-kit` Workflow](#troubleshooting-the-spec-kit-workflow)
        *   [Issue: `specify init` fails or hangs](#issue-specify-init-fails-or-hangs)
        *   [Issue: A `/speckit.*` command produces poor or incomplete results](#issue-a-speckit-command-produces-poor-or-incomplete-results)
        *   [Issue: `/speckit.tasks` creates a strange or illogical plan](#issue-speckittasks-creates-a-strange-or-illogical-plan)
        *   [Issue: `/speckit.implement` fails or produces buggy code](#issue-speckitimplement-fails-or-produces-buggy-code)
*   [Path B: The Manual Agent Workflow](#path-b-the-manual-agent-workflow)
    *   [Phase 1: Initialize the Project](#phase-1-initialize-the-project-1)
        *   [Step 1: Create the Constitution](#step-1-create-the-constitution)
        *   [Step 2: Enrich the Constitution](#step-2-enrich-the-constitution)
    *   [Phase 2: Create the Architecture](#phase-2-create-the-architecture)
        *   [Step 3: Generate Blueprint and Roadmap](#step-3-generate-blueprint-and-roadmap)
    *   [Phase 3: Research and Plan Epic 1](#phase-3-research-and-plan-epic-1)
        *   [Step 4: Research the First Epic](#step-4-research-the-first-epic)
        *   [Step 5: Create Implementation Tasks](#step-5-create-implementation-tasks)
    *   [Phase 4: Implement the Tasks](#phase-4-implement-the-tasks)
        *   [Step 6: Execute the First Task](#step-6-execute-the-first-task)
        *   [Step 7: Handle Implementation Issues](#step-7-handle-implementation-issues)
        *   [Step 8: Complete Remaining Tasks](#step-8-complete-remaining-tasks)
    *   [Phase 5: Complete the Epic](#phase-5-complete-the-epic)
        *   [Step 9: Report Epic Completion](#step-9-report-epic-completion)
        *   [Step 10: Update the Roadmap](#step-10-update-the-roadmap)
    *   [Troubleshooting: When a Prompt Fails to Perform](#troubleshooting-when-a-prompt-fails-to-perform)
        *   [The Prompt Debugging Workflow](#the-prompt-debugging-workflow)
        *   [Example: Fixing the Initializer](#example-fixing-the-initializer)
        *   [Model Recommendations for Troubleshooting](#model-recommendations-for-troubleshooting)
    *   [What To Do If...](#what-to-do-if)
        *   [The agent skips steps or questions](#the-agent-skips-steps-or-questions)
        *   [An epic seems too large](#an-epic-seems-too-large)
        *   [A task is too complex for Implementer](#a-task-is-too-complex-for-implementer)
        *   [Context window issues arise](#context-window-issues-arise)
        *   [The agent hallucinates or makes things up](#the-agent-hallucinates-or-makes-things-up)

## Path A: The `spec-kit` Workflow

This path uses the `spec-kit` to drive the development process. It's a more automated and opinionated approach.

This guide walks you through building the Context Window Visualizer project
using the `spec-kit` development workflow. You'll use the `specify` CLI and a
series of structured commands to direct a single AI agent from project
initialization to a complete implementation.

**Key Principle:** This workflow is tool-driven. The `specify` CLI and its
associated `/speckit.*` commands provide the structure, and your AI assistant
executes the well-defined steps.

### Prerequisites

*   IDE with GitHub Copilot (or another supported AI agent) installed.
*   [Python 3.11+](https://www.python.org/downloads/) installed.
*   `uv` installed for Python package management. You can install it with:

    ```bash
    pip install uv
    ```

### A Note on Agent and Model Management

Unlike the manual multi-agent workflow, the `spec-kit` approach is designed for
a single, continuous interaction with your AI assistant. You do not need to
switch between different "chatmodes" or AI models. Simply ensure your preferred
assistant, such as GitHub Copilot, is active. The `spec-kit` commands will
provide the necessary structure for the agent to follow.

---

### Phase 1: Initialize the Project

#### Step 1: Install the `specify` CLI

First, you need to install the `spec-kit` command-line tool.

1.  Open a terminal in VS Code.
1.  Run the following command to install the `specify-cli` using `uv`:

    ```bash
    uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
    ```

    This makes the `specify` command available globally in your terminal.

#### Step 2: Initialize the Project with `spec-kit`

Next, you'll use the CLI to scaffold a new project. This will set up the
necessary directory structure and enable the `/speckit.*` commands in your AI
assistant.

1.  In your terminal, navigate to where you want to create your project.
1.  Run the `init` command:

    ```bash
    specify init context-window-visualizer --ai copilot
    ```

1.  Navigate into the newly created directory:

    ```bash
    cd context-window-visualizer
    ```

**Your responsibility:** Ensure the command completes successfully. You should
see a new `context-window-visualizer` folder.

### Phase 2: Define Project Principles

#### Step 3: Create the Constitution

The Constitution is a document that contains the governing principles, coding
standards, and technical guidelines for your project.

1.  Start a **new chat session** with copilot.
1.  Here you have few options:
    1.  Run the `/speckit.constitution` and add the repos ready made README.md
        as context.
    1.  Alternatively, run the `/speckit.constitution` command with a prompt
        describing your desired standards.

    **Example Prompt:**

    ```
    /speckit.constitution Create a constitution for a web application built with React and TypeScript. The standards should emphasize functional components with hooks, styling with Tailwind CSS, and unit testing with Vitest. All code must be formatted with Prettier.
    ```

The agent will generate a `CONSTITUTION.md` file in your project.

**Your responsibility:** Read the generated `CONSTITUTION.md` file. Does it
accurately reflect the standards you want? If not, you can either edit the file
directly or re-run the command with a more specific prompt.

### Phase 3: Specify the Application

#### Step 4: Define the "What"

Now, describe the application you want to build from a user-centric perspective.
Focus on features and behavior, not technical implementation.

1.  In the same chat session, run the `/speckit.specify` command.

    **Example Prompt:**

    ```
    /speckit.specify Build a web application that helps developers visualize the context window of a large language model. The user should be able to add different types of content (like code blocks, plain text, and image placeholders) and see a visual representation of how much space each item consumes in the context window. The total context size should be configurable.
    ```

This will generate a `spec.md` file, capturing the core requirements of your
project.

**Your responsibility:** Review the `spec.md`. Does it clearly define the
application's features? Is anything missing?

### Phase 4: Create the Technical Plan

#### Step 5: Define the "How"

With the "what" defined, it's time to specify the "how." Provide the agent with
your technology stack and architectural choices.

1.  In the same chat session, run the `/speckit.plan` command.

    **Example Prompt:**

    ```
    /speckit.plan The application will be a single-page application built using Vite, React, and TypeScript. State management will be handled globally with Zustand. Styling will be implemented using Tailwind CSS. No backend is required; all state is managed on the client side.
    ```

The agent will create an `plan.md` and other architectural documents.

**Your responsibility:** Check that the plan aligns with your technical goals
and the project's constitution.

### Phase 5: Generate and Execute Tasks

#### Step 6: Create the Task List

The `spec-kit` can automatically break down the implementation plan into a
series of small, actionable tasks.

1.  In the same chat session, simply run:

    ```
    /speckit.tasks
    ```

The agent will analyze the plan and generate `tasks.md`.

**Your responsibility:** Briefly review the generated task file. It should
represent a logical sequence of steps to build the application, such as setting
up the project structure, creating components, and styling them.

#### Optional Step: Analyze and Refine

Before executing the implementation, you can use optional `spec-kit` commands to
enhance quality and validation. These commands help ensure consistency and
completeness.

1.  In the same chat session, run `/speckit.analyze` to perform a cross-artifact
    consistency and coverage analysis. This is highly recommended after
    generating tasks and before implementation.

    ```
    /speckit.analyze
    ```

1.  You can also generate a quality checklist to validate requirements using
    `/speckit.checklist`.

    ```
    /speckit.checklist
    ```

    This is like running "unit tests for your English" to ensure clarity and
    consistency.

1.  If you find your specification is underspecified, you can use
    `/speckit.clarify` to ask clarifying questions. This is best used before
    creating the technical plan (after Step 4).

**Your responsibility:** Review the output of these commands. They may highlight
inconsistencies or areas that need more detail before you proceed with
implementation.

#### Step 7: Execute the Implementation

This is where the magic happens. The `/speckit.implement` command instructs the
agent to execute all the generated tasks in sequence to build the application.

1.  In the same chat session, run:

    ```
    /speckit.implement
    ```

The agent will now work through each task, creating and modifying files
according to the plan. It will report its progress and let you know when it's
finished.

**Your responsibility:** Monitor the agent's progress. Once it reports
completion, explore the generated codebase. Run the application to see the
result.

---

### Troubleshooting the `spec-kit` Workflow

Even with a structured tool, things can sometimes go awry. Here's what to do
when a `spec-kit` command doesn't behave as expected.

#### Issue: `specify init` fails or hangs

*   **Check Prerequisites:** Ensure `git`, `python`, and `uv` are correctly
    installed and available in your system's PATH.
*   **Network Issues:** The command clones a template from GitHub. Check your
    internet connection and any firewall or proxy settings that might be
    blocking `git`.
*   **Run with Debug:** Try running the command with the `--debug` flag for more
    detailed output: `specify init my-project --ai copilot --debug`.

#### Issue: A `/speckit.*` command produces poor or incomplete results

If `/speckit.constitution`, `/speckit.specify`, or `/speckit.plan` generates a
document that is vague or incorrect, the issue is likely with the prompt you
provided.

*   **Be More Specific:** Re-run the command with a more detailed prompt. Add
    constraints, mention specific libraries, or clarify requirements.
    *   **Bad:** `/speckit.plan Use React.`
    *   **Good:** `/speckit.plan Use Vite, React, and TypeScript. Use functional
        components and hooks. Avoid class-based components.`
*   **Edit Manually:** For minor issues, it's often faster to manually edit the
    generated markdown file before proceeding to the next step.

#### Issue: `/speckit.tasks` creates a strange or illogical plan

If the task breakdown seems wrong, it's a sign that the `plan.md` was not clear
enough.

1.  **Go Back:** Return to Step 5 and re-run `/speckit.plan` with a clearer
    architectural description.
1.  **Manually Adjust:** You can also manually edit the task files in
    `docs/tasks` to correct the logic before running the implementation.

#### Issue: `/speckit.implement` fails or produces buggy code

This is the most complex failure mode. The agent might get stuck, write
non-working code, or fail to complete all tasks.

*   **Review the Logs:** Carefully read the agent's output to identify which
    task failed and why.
*   **Isolate the Problem:** Look at the specific task file that caused the
    issue. Is the instruction unclear?
*   **Try thread_dump:** If the agent seems confused or repetitive, use the
    `/thread_dump` command to generate a handoff briefing. Start a fresh chat
    session with this briefing to reset context.


## Path B: The Manual Agent Workflow

This path simulates a team of specialized AI agents that you manage. It's a more
manual process that gives you a deeper look into the mechanics of multi-agent
collaboration.

### Introduction

This guide walks you through building the Context Window Visualizer project
using the multi-agent development workflow. You'll direct specialized AI agents
through different phases, from project initialization to implementing your first
epic.

### Key Principle

Use a fresh chat session for each agent interaction. The agents don't share
memory—all project state lives in markdown files that you pass between them.

### Prerequisites

*   VS Code with GitHub Copilot installed
*   `.github/chatmodes` and `.github/prompts` directories set up with agent
    definitions
*   Basic understanding of attaching files in Copilot chat (use `#` to reference
    files)

### Model Recommendations

Different agents work best with different AI models:

*   **Initializer & Architect**: Gemini 2.5 Pro, Claude Sonnet 3.5/4, or GPT-5
    (your preference)
*   **Lead Developer**: Claude Sonnet 4/4.5 (better at detailed planning and
    research)
*   **Implementer**: Claude Sonnet 4/4.5 (superior code generation and
    precision)

### ⚠️ Critical: Chat Thread Behavior

**VS Code Copilot has a gotcha:** When you switch between chat threads, the
chatmode and model selection do NOT carry over. If you start a thread with
"Architect" mode, switch to work on "Implementer", then return to the Architect
thread—it will still have **Implementer** mode and model selected.

**Always verify before running a prompt:**

1.  Check the chatmode selector shows the correct agent
1.  Check the model selector shows your preferred model for that agent
1.  Manually switch back if needed

This is current VS Code behavior and easy to miss!

### Phase 1: Initialize the Project

### Step 1: Create the Constitution

1.  Start a **new chat session**
1.  Select the **Initializer** chatmode
1.  Attach the README.md: `@README.md`
1.  Run: `/init_project`

The Initializer will conduct a 12-question interview about your technical
choices. For this project, JavaScript/TypeScript with React is recommended, but
you can choose your preferred stack.

**Your responsibility:** Answer all 12 questions thoughtfully. These decisions
will guide every subsequent agent.

Once complete, you'll have `CONSTITUTION.md` with your technical decisions.

**If it fails:** The agent might skip questions (blame the prompt author). Tell
it explicitly: "You missed questions X, Y, Z. Please ask them now."

### Step 2: Enrich the Constitution

1.  Keep the same chat or start fresh with **Initializer** mode
1.  Attach the `CONSTITUTION.md` you just created
1.  Run: `/enrich_constitution`

The agent will propose comprehensive coding standards, error handling patterns,
security practices, and more based on your tech stack.

**Your responsibility:** Review the proposed enhancements. You can:

*   Accept all proposals
*   Request modifications to specific sections
*   Remove sections you don't want

The enriched `CONSTITUTION.md` becomes the project's definitive guide.

## Phase 2: Create the Architecture

### Step 3: Generate Blueprint and Roadmap

1.  Start a **new chat session**
1.  Select the **Architect** chatmode
1.  Attach your `CONSTITUTION.md`
1.  Run: `/create_blueprint`

The Architect will:

*   Design the component architecture
*   Define the state management approach
*   Create a 5-epic ROADMAP.md
*   Generate an Initial Architecture ADR

**Your responsibility:**

*   **READ** the proposed architecture carefully
*   Verify the epics make sense for the Context Visualizer project
*   Check that the architecture aligns with your Constitution
*   Ensure Epic 1 is a reasonable starting point (usually "Foundation" or
    "Setup")

Output files:

*   `docs/ROADMAP.md` - Your development plan
*   `docs/ADR/INITIAL_ARCHITECTURE_ADR.md` - Architectural decisions

## Phase 3: Research and Plan Epic 1

### Step 4: Research the First Epic

1.  Start a **new chat session**
1.  Select the **Lead Developer** chatmode
1.  **Set model to Claude Sonnet 4 or 4.5** (recommended for planning tasks)
1.  Attach:
    *   `CONSTITUTION.md`
    *   `docs/ADR/INITIAL_ARCHITECTURE_ADR.md`
    *   The first epic's ADR (if Architect created one)
    *   Any existing code files relevant to the epic
1.  Run: `/lead_research`

The Lead Developer will investigate:

*   What files need to be created/modified
*   What patterns to follow
*   Technical specifications needed
*   Integration points

**Your responsibility:**

*   **READ** the research output thoroughly
*   Check if the research makes sense
*   Verify file paths are correct
*   If something seems wrong, tell the agent or tweak the prompt

Output: `docs/epic_[name]/research/RESEARCH.md`

### Step 5: Create Implementation Tasks

1.  Continue with the same **Lead Developer** session (or start new)
1.  Attach:
    *   The epic's ADR
    *   `docs/epic_[name]/research/RESEARCH.md`
1.  Run: `/lead_plan`

The Lead Developer will:

*   Create an implementation plan
*   Generate numbered task files (01_task_name.md, 02_task_name.md, etc.)
*   Document decisions in a decision log
*   Create a task manifest

**Task numbering:** Tasks are numbered sequentially (01, 02, 03...) to enforce
execution order. Each task is designed to be completed without blocking on
others.

**Your responsibility:**

*   Read each task file to ensure it makes sense
*   Verify tasks are small enough (each should be completable in one session)
*   Check that file paths use project root (`/`) not placeholders

Output files in `docs/epic_[name]/`:

*   `plans/IMPLEMENTATION_PLAN.md`
*   `plans/DECISION_LOG.md`
*   `tasks/01_[name].md`, `tasks/02_[name].md`, etc.
*   `MANIFEST.md`

## Phase 4: Implement the Tasks

### Step 6: Execute the First Task

1.  Start a **new chat session**
1.  Select the **Implementer** chatmode
1.  **Set model to Claude Sonnet 4 or 4.5** (best for precise code generation)
1.  Attach the first task file: `docs/epic_[name]/tasks/01_[task_name].md`
1.  Run: `/implement`

The Implementer will:

*   Read and summarize what it plans to do
*   List all files it will create/modify
*   Ask for your approval to proceed

**Your responsibility:**

*   Review the implementation plan
*   Confirm it matches the task specification
*   Approve with "yes" or request clarification

Once approved, the Implementer will:

*   Execute the task step by step
*   Run linter on modified files
*   Execute tests if applicable
*   Report completion status

### Step 7: Handle Implementation Issues

**If the task succeeds:**

*   Review the code changes
*   Commit when the Implementer confirms all checks pass
*   Move to the next task (repeat Step 6 with `02_[task_name].md`)

**If verification fails:**

*   Read the Implementer's explanation
*   Minor issues: Let it proceed if non-critical items failed
*   Major issues: The Implementer will use `/ask_advice`

**If the Implementer gets blocked:**
The agent will present an escalation request with:

*   What went wrong
*   What was attempted
*   Proposed solutions

You can:

*   Approve a proposed solution
*   Provide alternative approach
*   Modify the task specification
*   Abort and go back to Lead Developer for task revision

### Step 8: Complete Remaining Tasks

Repeat Step 6 for each task file in sequence (02, 03, etc.) until all tasks in
the epic are complete.

**Important:** Each task should be run in a fresh Implementer session with just
that task file as context.

## Phase 5: Complete the Epic

### Step 9: Report Epic Completion

After the last task succeeds:

1.  Stay in **Implementer** mode or start new session
1.  Attach:
    *   The epic's ADR
    *   `docs/epic_[name]/plans/IMPLEMENTATION_PLAN.md`
    *   `docs/epic_[name]/MANIFEST.md`
1.  Run: `/report_to_lead`

The Implementer generates a completion report with:

*   Summary of work completed
*   Any deviations from plan
*   Recommendations for future epics

### Step 10: Update the Roadmap

1.  Start a **new chat session**
1.  Select the **Architect** chatmode
1.  Attach:
    *   `docs/ROADMAP.md`
    *   The completion report from Step 9
1.  Ask the Architect to update the ROADMAP marking Epic 1 as complete

## Troubleshooting: When a Prompt Fails to Perform

Sometimes an agent won't follow its prompt correctly—it skips questions, ignores
instructions, or produces incomplete output. When this happens, don't just
retry. Instead, use this systematic approach to fix the prompt itself:

### The Prompt Debugging Workflow

**Step 1: Stop and Document**

*   Don't continue with the broken session
*   Note exactly what went wrong:
    *   What the prompt should have done
    *   What the agent actually did
    *   Which steps were skipped or incorrect

**Step 2: Start a Fresh Debugging Session**

1.  Open a **new chat session**
1.  Select **Ask** mode (not the agent that failed)
1.  **Choose a high-powered model:**
    *   **Recommended:** Claude Sonnet 4 or 4.5 (excellent at analysis)
    *   **Alternative:** GPT-4o, Gemini 2.0 Flash, or best available
1.  Attach the problematic prompt file (e.g.,
    `.github/prompts/Init Project.prompt.md`)

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

*   Answer the model's clarifying questions
*   Discuss what instructions are unclear or missing
*   Review the model's proposed improvements
*   Iterate until you have a clear fix

**Step 5: Generate the Updated Prompt**
Once you've agreed on the changes:

1.  **Switch to Opus 4.1** if available (superior for precise generation)
1.  Or stay with Claude Sonnet 4/4.5 if Opus isn't available
1.  Ask it to generate the complete updated prompt
1.  Review carefully—ensure all changes are incorporated
1.  Update the prompt file

**Step 6: Test the Fixed Prompt**

1.  Start a **new session** with the appropriate agent mode
1.  Run the updated prompt
1.  Verify it now behaves correctly
1.  If issues remain, repeat from Step 2

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

*   "Are the questions in distinct sections that might confuse it?"
*   "Does the prompt have explicit counters and checkpoints?"
*   "Is there ambiguity in the progression logic?"

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

*   **Best:** Claude Sonnet 4 or 4.5 (excellent reasoning and clarifying
    questions)
*   **Alternative:** GPT-4o, Gemini 2.0 Flash (if Claude unavailable)

**Generation Phase (Step 5):**

*   **Best:** Claude Opus 4.1 (superior precision and completeness)
*   **Fallback:** Claude Sonnet 4/4.5 (still very good)
*   **Note:** Use what's available to you—Sonnet 4/4.5 can handle both phases

## What To Do If...

### The agent skips steps or questions

*   Use the **Prompt Debugging Workflow** above to fix the prompt
*   Explicitly tell it what it missed as a temporary workaround
*   Reference the specific requirement from the prompt
*   Don't rely on verbal corrections—fix the prompt file itself

### An epic seems too large

*   Go back to Architect mode
*   Ask it to split the epic into smaller ones
*   Or proceed to Lead Developer and let it create more granular tasks

### A task is too complex for Implementer

*   Use `/split_to_helper` to delegate part of it
*   Or abort and go back to Lead Developer for better task decomposition

### Context window issues arise

*   Agent becomes repetitive or confused
*   Performance degrades
*   **Use `/thread_dump`** to generate a handoff briefing
*   Copy the briefing and start a fresh session with it
*   Or use smaller task files and start fresh sessions more frequently

### The agent hallucinates or makes things up

*   Stop immediately
*   Verify against the Constitution and ADRs
*   Provide explicit correction
*   Start a new session with correct context

## Moving Forward

After Epic 1 completes successfully:

1.  Return to **Architect** mode for the next epic
1.  The workflow repeats: Research → Plan → Implement → Report
1.  Each epic builds on the previous work
1.  Always reference the Constitution and Architecture ADRs

Remember: The agents are probabilistic and will sometimes need correction. Your
job is to guide them, validate their output, and maintain project coherence
through careful review of all generated documentation.

## Tips for Success

*   **One agent, one task, one chat session** - Don't mix contexts
*   **Double-check chatmode and model** - Every time you switch threads, verify
    they're correct
*   **Use Claude Sonnet 4/4.5 for implementation** - It's superior for code
    generation and detailed planning
*   **Use `/thread_dump` when stuck** - If agent loses context or becomes
    confused, dump and restart fresh
*   **Read everything** - The agents generate detailed documentation for a
    reason
*   **Commit frequently** - After each successful task or epic
*   **Trust but verify** - Agents follow patterns but can make mistakes
*   **When in doubt, escalate** - Go back to higher abstraction levels

This experimental system will evolve. When you find issues, use Copilot to
improve the prompts and share your enhancements with the community.