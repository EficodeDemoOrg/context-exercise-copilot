# Context Window Visualizer – MVP Project Brief

## 1. The Client & The Challenge

**Scenario:**
Our internal Developer Experience team is building a tool to help engineers understand and debug AI agent behavior. A common point of failure is "context mismanagement," where the AI's limited context window becomes filled with irrelevant information, leading to degraded performance and incorrect outputs.

**Goal:**
Build an integrated tool that makes the invisible state of an AI's context window visible. You will develop a single, interactive web application that handles both the context management logic and its visualization.

**Purpose of MVP:**
To create a functional web application that provides a real-time, interactive simulation of a context window, helping developers build an intuition for context management.

## 2. The Development Path: An Integrated Web Application

You will build a single-page web application that combines the context management engine with a real-time visualization.

**Features:**

### Interactive UI:
- Display the context window as a dynamic bar that fills up as content is added.
- Use different colors within the bar to represent different types of context (e.g., system_prompt, file, history).
- Show the current token count and the maximum limit in a text display (e.g., 45,000 / 128,000 tokens).
- Provide UI controls (e.g., input fields for type and token count, and an "Add Context" button) to allow a user to add items to the context.

### State Management Logic:
- The application must maintain the state of all items in the context window internally.
- Implement the performance degradation logic, which is reflected visually:
  - **optimal** (< 60% full): The bar should be green.
  - **degraded** (60%-80% full): The bar turns yellow, and a warning indicator appears.
  - **critical** (> 80% full): The bar turns red, and a compaction event is automatically triggered.
- The compaction logic should remove the oldest history item from the application's state and log a message to the UI (e.g., "Context limit reached. Compacting history.").

## 3. Application State Model

The application should be built around a clear internal state model representing the context window.

This model should track the total tokens, max tokens, current status (optimal, degraded, critical), and a list of all context items. Each item in the list should have properties like type, token_count, and an optional source.

## 4. Expected Outcome & Deliverables

- A functional single-page web application that meets all the specified requirements.
- A `docs/STATE_MODEL.md` file briefly describing the structure of the application's core state object.

**Demo (5 min):**
- Show how the application visualizes the context window and handles adding items.
- Demonstrate the degraded and critical states, including an automatic compaction event.
- Explain how this tool helps developers debug AI context issues.
- Briefly describe your agentic workflow.

## 5. Stretch Goals (Optional)

- Animate the context bar filling up and items being removed during compaction.
- Allow users to click on segments in the bar to see more details about that context item.
- Implement a more sophisticated compaction algorithm (e.g., summarizing the two oldest history items into one).
- Allow users to configure the degradation thresholds via UI inputs.

## 6. Learning Goals

- **Adopt an Agentic Workflow:** The primary goal is to practice building a complete prototype using an AI agent as your primary development partner.
- **Practice Blueprint Creation:** Start new projects by collaborating with an AI Architect to establish foundational technical decisions before implementation.
- **Practice Thread Isolation:** Learn to manage complexity by assigning distinct, single-purpose tasks to separate, isolated agent threads.
- **Utilize AI for Planning:** Use the agent not just for coding, but as a strategic partner to create a project roadmap and a TODO.md to track progress.
- **Task Decomposition:** Break down the larger project goal into small, well-defined tasks that can be completed by a focused agent in a single thread.
- **Practice Memory Persistence Between Agent Threads:** Utilize markdown files (BLUEPRINT.md, research.md, developer_todo.md) in a systematic way to ground agents in a shared 'memory'.
- **Leverage Agent Roles:** Improve the quality of the AI's output by assigning it specific, expert roles for different phases of the project.

## 7. Getting Started

This exercise uses a multi-agent development workflow with specialized AI agents for different phases of development.

### Documentation

- **[Agents and Prompts](Agents%20and%20Prompts.md)** - Comprehensive system reference detailing the agent architecture, roles, capabilities, and protocols. Read this if you want to understand how the multi-agent system works.

- **[Exercise Guide](exercise-guide.md)** - Step-by-step walkthrough for building the Context Window Visualizer. Start here if you're ready to begin the exercise immediately.

### Quick Start

If you're impatient and want to dive in:
1. Read the **Exercise Guide** and follow the steps
2. Reference the **Agents and Prompts** documentation when you need clarification

If you prefer to understand the system first:
1. Read the **Agents and Prompts** documentation to learn about the workflow
2. Then follow the **Exercise Guide** to build the project