# Context Window Visualizer – MVP Project Brief

## 1. The Client & The Challenge

**Scenario:**
Our internal Developer Experience team is building a tool to help engineers understand and debug AI agent behavior. A common point of failure is "context mismanagement," where the AI's limited context window becomes filled with irrelevant information, leading to degraded performance and incorrect outputs.

**Goal:**
Build an integrated tool that makes the invisible state of an AI's context window visible. You will develop a single, interactive web application that handles both the context management logic and its visualization.

**Purpose of MVP:**
To create a functional web application that provides a real-time, interactive simulation of a context window, helping developers build an intuition for context management.

## 2. The Development Path: An Integrated Web Application

You will build a **ChatGPT-style interface** with an integrated context window monitor that makes context management visible and interactive.

### Core Interface Components:

#### Chat Interface
A familiar conversation interface featuring:
- **Message Display Area**: Shows conversation history with clear visual distinction between user and assistant messages
- **Input Field**: Text area for typing messages at the bottom of the interface
- **Send Button**: Triggers message submission
- **Attachment Controls**: Buttons or drag-and-drop area for adding files, images, or pasting text blocks

#### Context Monitor Panel
A dedicated visualization area (sidebar or top panel) displaying:
- **Visual Progress Bar**: Horizontal segmented bar showing context window usage
  - Different colors represent different content types (system prompts, files, conversation, images)
  - Bar fills proportionally as content is added
  - Segments are sized according to their token usage
- **Token Counter**: Real-time display (e.g., "45,231 / 128,000 tokens")
- **Context Items List**: Expandable list showing all items currently in context with their individual token costs
- **Performance Status Indicator**: Visual indicator showing current state (Optimal/Degraded/Critical)

### User Interaction Flow:

**Adding Content:**
1. User types messages in chat → adds to "conversation" context type
2. User attaches files via button or drag-and-drop → adds to "file" context type  
3. User pastes images → adds to "image" context type
4. User configures system prompts via settings → adds to "system" context type

**Visual Feedback:**
- Context bar fills in real-time as content is added
- Each addition shows its token cost
- Hover over bar segments to see item details (type, source, token count)
- Smooth animations when items are added or removed

**Example User Journey:**
1. Start with empty chat and context window at 0 tokens
2. Add system prompt: "You are a helpful assistant" → 500 tokens (Blue segment appears)
3. Attach a markdown file → 2,000 tokens (Green segment grows)
4. Type several messages back and forth → conversation history grows (Gray segments expand)
5. Context reaches 60% → Status changes to "Degraded" with yellow indicator
6. Continue adding content
7. Context reaches 80% → Status becomes "Critical" with red alert
8. Add more content → Automatic compaction triggers, oldest messages removed
9. Notification appears: "Context compacted - removed 3 oldest messages (1,200 tokens)"

### State Management Logic:

The application must maintain a clear internal state model:

**Performance States:**
- **Optimal** (< 60% full): Green indicator, normal operation
- **Degraded** (60%-80% full): Yellow indicator with warning message
- **Critical** (> 80% full): Red indicator, compaction triggers automatically when new content would exceed limit

**Compaction Algorithm:**
When context limit is reached, the system must:
1. Identify oldest compressible items (conversation history)
2. Remove them in chronological order (oldest first)
3. Never remove system prompts or attached files
4. Display notification with details of what was compacted
5. Update context bar visualization immediately

## 3. Application State Model

The application should be built around a clear internal state model representing the context window.

### Context Item Structure:
Each item in the context must track:
```
ContextItem:
  - id: unique identifier
  - type: one of [system, file, message, image]
  - content: the actual text or data
  - tokenCount: calculated token usage
  - timestamp: when it was added
  - source: optional (e.g., filename, "user", "assistant")
  - compressible: boolean (can it be removed during compaction?)
```

### Application State:
The application state must include:
```
ApplicationState:
  - maxTokens: 128000
  - currentTokens: sum of all item token counts
  - status: one of [optimal, degraded, critical]
  - contextItems: array of ContextItem
  - chatMessages: array of chat history (user/assistant exchanges)
  - compactionEvents: count of how many times compaction occurred
```

### Token Calculation:
For MVP purposes, use simple approximation:
- 1 token ≈ 4 characters
- Display both character count and estimated tokens
- More sophisticated tokenization is a stretch goal

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