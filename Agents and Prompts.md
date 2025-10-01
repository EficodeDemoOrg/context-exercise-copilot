# Multi-Agent Development Workflow

## System Status: Experimental 🧪

This is an experimental multi-agent system for orchestrating software development through VS Code Copilot. The prompts, chatmodes, and workflows are actively being refined. When you encounter issues or inefficiencies, use GitHub Copilot to help you improve the prompts and share your enhancements with the community.

---

## Overview

This system implements a structured, multi-layer development workflow using specialized AI agents. Each agent has a specific role, defined capabilities, and strict operational boundaries. The workflow moves from high-level project initialization through architecture, planning, and finally to implementation.

## The Agents & Their Roles

### 🎯 **Initializer**
The project constitution creator. Conducts a structured 12-question interview to establish the foundational technical decisions for a new project.

### 🏗️ **Architect** 
The strategic technical designer. Translates the constitution into architectural blueprints, creates development roadmaps, and assesses new features against existing architecture.

### 👨‍💼 **Lead Developer**
The technical manager. Bridges architectural vision and practical implementation by researching, planning, and decomposing epics into context-efficient tasks.

### ⚙️ **Implementer**
The execution specialist. Takes individual task specifications and transforms them into working code with surgical precision.

---

## Human Responsibilities ⚠️

**The success of this system depends on active human oversight:**

### **YOU MUST:**
- **✅ VALIDATE** all architectural decisions and plans before proceeding to implementation
- **📎 ATTACH** the correct context files when invoking any prompt (agents cannot find files themselves)
- **📖 READ** all generated documentation and reports thoroughly before moving to the next phase
- **🔍 REVIEW** code changes before committing (even after verification passes)
- **⬆️ ESCALATE** to higher abstraction levels when agents report blockers or conflicts
- **💾 COMMIT** code only after the Implementer's verification checklist passes

### **Context Attachment Rules:**
- Always provide files as markdown attachments in the chat
- Include ALL files listed as "REQUIRED CONTEXT" in prompts
- Use relative paths from project root (e.g., `docs/ADR/FEATURE_ADR.md`)

---

## Agent Capabilities Reference

| Agent | Command | Description | Required Input |
|-------|---------|-------------|----------------|
| **Initializer** | | | |
| | `/init_project` | Conduct 12-question interview to create CONSTITUTION.md | README.md |
| | `/enrich_constitution` | Enhance basic constitution with comprehensive best practices | Existing `CONSTITUTION.md` |
| **Architect** | | | |
| | `/create_blueprint` | Generate initial architecture from constitution | `CONSTITUTION.md` |
| | `/assess_feature` | Evaluate feature impact on architecture | Constitution + existing ADRs + feature description |
| **Lead Developer** | | | |
| | `/lead_research` | Research implementation approach for epic | `CONSTITUTION.md` + ADR file + relevant code |
| | `/lead_plan` | Create implementation plan and tasks | Epic ADR + `RESEARCH.md` |
| | `/report_to_architect` | Generate completion report | Epic ADR + plan + manifest |
| **Implementer** | | | |
| | `/implement` | Execute a single task file | Task file from `docs/epic_*/tasks/` |
| | `/ask_advice` | Escalate blockers or ambiguities | Current task file + problem context |
| | `/report_to_lead` | Report task completion status | Completed task file |
| | `/split_to_helper` | Delegate sub-task to helper agent | Current task + sub-task definition |
| **All Agents** | | | |
| | `/thread_dump` | Generate context handoff for new agent instance | Current session state |

---

## Workflow Protocol

### Phase 1: Project Initialization (One-time)
```
User → Initializer (/init_project) → CONSTITUTION.md 
                 ↓
         Optional: /enrich_constitution → Enhanced CONSTITUTION.md
                 ↓
         Architect (/create_blueprint) → Initial Architecture + Roadmap
```

### Phase 2: Feature Development (Repeatable)
```
User requests feature → Architect assesses → Creates ADR
                                ↓
                        Lead Developer researches → Creates tasks
                                ↓
                        Implementer executes → Reports completion
```

### Phase 3: Iteration & Refinement
```
Implementer blocked → Ask advice → User guidance
Task failed → Report to Lead → Lead revises → New task
Feature complete → Report to Architect → Roadmap updated
```

---

## File Output Structure

The system generates a structured documentation hierarchy:

```
project-root/
├── CONSTITUTION.md                    [Initializer output]
├── docs/
│   ├── ROADMAP.md                    [Architect output]
│   ├── ADR/
│   │   ├── INITIAL_ARCHITECTURE_ADR.md   [Architect output]
│   │   ├── FEATURE_X_ADR.md             [Architect output]
│   │   └── ...
│   └── epic_<name>/                  [Lead Developer workspace]
│       ├── research/
│       │   └── RESEARCH.md           [Lead research output]
│       ├── plans/
│       │   ├── IMPLEMENTATION_PLAN.md    [Lead planning output]
│       │   └── DECISION_LOG.md           [Lead decisions]
│       ├── tasks/
│       │   ├── 01_task_name.md          [Lead task definition]
│       │   ├── 02_task_name.md          [Lead task definition]
│       │   └── ...
│       ├── MANIFEST.md                   [Lead task manifest]
│       └── COMPLETION_REPORT.md          [Lead final report]
└── src/                              [Implementer modifications]
    └── ...
```

---

## Information Flow Protocol

### Document Handoffs

1. **Initializer → Architect**
   - Output: `CONSTITUTION.md`
   - Contains: Technical stack, practices, principles

2. **Architect → Lead Developer**
   - Output: Epic-specific ADR (e.g., `docs/ADR/AUTH_ADR.md`)
   - Contains: Requirements, architectural decisions, constraints

3. **Lead Developer → Implementer**
   - Output: Individual task files (e.g., `docs/epic_auth/tasks/01_create_slice.md`)
   - Contains: Step-by-step instructions, file paths, code snippets

4. **Implementer → Lead Developer**
   - Output: Completion reports (in chat or as markdown)
   - Contains: Status, deviations, incomplete items

### Context Requirements by Agent

- **Initializer**: Needs only README.md
- **Architect**: Needs `CONSTITUTION.md` + any existing ADRs
- **Lead Developer**: Needs ADR + existing codebase files
- **Implementer**: Needs single task file + referenced context files

---

## Quality Gates

Each phase has mandatory verification before proceeding:

### After Initialization
- [ ] CONSTITUTION.md exists and contains all 12 answered questions
- [ ] Technical decisions are clear and non-conflicting
- [ ] (Optional) Constitution enriched with coding standards and best practices

### After Architecture
- [ ] ADR contains context, decision, and consequences
- [ ] ROADMAP.md has 5 clearly defined epics
- [ ] Architecture aligns with CONSTITUTION.md

### After Planning
- [ ] Each task is under 25k token context limit
- [ ] Tasks can be executed sequentially without blocking
- [ ] All file paths are explicit (no placeholders)

### After Implementation
- [ ] All Definition of Done items checked or explained
- [ ] Linter passes on modified files
- [ ] Tests pass (where applicable)
- [ ] No TypeScript/compilation errors

---

## Escalation Patterns

### When to Escalate

| Situation | Current Agent | Escalate To | Action |
|-----------|--------------|-------------|---------|
| Task contradicts specifications | Implementer | Lead Developer | Use `/ask_advice` |
| Epic scope needs change | Lead Developer | Architect | Request ADR revision |
| Architecture conflicts with constitution | Architect | Initializer/Human | Revise constitution |
| Security vulnerability detected | Any | Human | Immediate stop and review |
| Context window exceeded | Implementer | Lead Developer | Split task further |

---

## Context Management

### Thread Dump Protocol

When a chat session's context window approaches capacity or becomes degraded, use `/thread_dump` to create a comprehensive handoff briefing. This protocol:

- **Captures complete session state**: Agent role, current command, workflow phase, and exact interruption point
- **Documents all work completed**: Files created/modified, decisions made, accomplishments
- **Preserves critical context**: Task status, dependencies, constraints, and immediate next steps
- **Provides continuation instructions**: Exact files to attach and steps to resume work

**When to use:**
- Chat becomes slow or repetitive
- Agent loses track of previous decisions
- You need to switch models/agents mid-task
- Session exceeds ~50k tokens (if you can estimate)

**How it works:**
1. Run `/thread_dump` in current session
2. Agent outputs a structured briefing directly in chat
3. Copy the entire briefing
4. Start fresh session with specified agent/model
5. Paste briefing as first message
6. New agent acknowledges and continues from exact interruption point

The receiving agent will have complete context to continue seamlessly as if no handoff occurred.

### Constitution Enrichment
The `/enrich_constitution` prompt transforms the minimal CONSTITUTION.md into a comprehensive project charter including:
- **Coding Standards**: Naming conventions, file organization, import ordering
- **Error Handling**: Standardized patterns, logging strategies
- **Security Practices**: Authentication, authorization, input validation
- **Data Management**: Database patterns, state management rules
- **Testing Standards**: Coverage requirements, test structure, mocking strategies
- **Performance Guidelines**: Metrics, caching, optimization rules
- **Development Workflow**: Branch naming, commit format, PR requirements
- **Documentation Requirements**: ADRs, API docs, inline comments
- **Operational Standards**: Monitoring, deployment, rollback procedures
- **Dependency Management**: Addition criteria, update schedules

This enriched constitution serves as a comprehensive onboarding document and guides all downstream agents.

---

## Contributing

This system is experimental and actively evolving. To contribute:

1. **Test the workflows** with real projects
2. **Document issues** with specific agent behaviors
3. **Use Copilot** to refine prompts that don't work well
4. **Share improvements** via pull requests
5. **Suggest enhancements** based on your use cases

Remember: The prompts and chatmodes are meant to be tweaked. When something doesn't work as expected, treat it as an opportunity to improve the system.

---

## Resources

- [Creating Chat Modes](https://code.visualstudio.com/docs/copilot/customization/custom-chat-modes)
- [Creating Prompt Files](https://code.visualstudio.com/docs/copilot/customization/prompt-files)
- [Prompt File Variables](https://code.visualstudio.com/docs/copilot/customization/prompt-files#_prompt-file-format)