# Week 3: Agent Implementation and UI Integration

## Overview

This week, building upon the Deep Agent setup you started previously, your objective is to implement the baseline agent architecture and integrate both agents into a unified, functional user interface.

As always, remember to rely on your "Vibe-Coding" tools. Ensure your AI assistants are connected to the LangChain Docs and DeepWiki MCP servers to generate accurate and up-to-date code.

## Tasks

### 1. Implement the Baseline Agent

Your first major task is to implement a standard agent architecture using the latest version of the LangChain library. This will serve as our fundamental baseline for comparison against the Deep Agent.

**Important LangChain Update:** Please note that in the latest versions of LangChain, the term "ReAct Agent" has been deprecated. Instead, it is simply referred to as an "Agent" and can be instantiated using the `create_agent()` method. We will still conceptually refer to it as our baseline or "ReAct-style" agent.

- **Action Space (Tools):** This agent must be strictly constrained to match the experimental setup outlined in the SWE-QA paper. You must provide it with **only** the following minimal tools:
  1. `read_file`
  2. `get_repo_structure`
  3. `search_rag`
- **Constraint:** Do not provide this agent with any extra tools (e.g., shell access, advanced planning, filesystem writing). It should only navigate and read the codebase to find its answers using these three specific tools.

### 2. Update and Customize the UI

With both the Deep Agent (from last week) and the standard baseline Agent (from this week) implemented on your backend, you must now bring them together in the frontend.

- **Customizing the GUI:** Modify your forked version of the Deep-Agents UI.
- **Setup Selector:** Implement a user-facing toggle or dropdown menu. At the beginning of a conversation, before asking a question about a codebase, the user must be able to select which architecture they want to use:
  - Agent (Standard/ReAct)
  - Deep Agent

### 3. Testing and Deployment

Once integrated, perform end-to-end testing:

- Provide a sample repository to your backend.
- Select the Standard Agent in the UI, ask a complex architectural question, and monitor how it loops through its specific tools to find the answer.
- Switch to the Deep Agent, ask the exact same question, and compare how it plans and assigns sub-agents to achieve the same goal.

## Success Criteria

For our meeting next week, you must successfully demonstrate:

1. A working chatbot UI where users can explicitly select either the standard Agent or the Deep Agent.
2. The ability to ask questions about a given codebase and receive answers from the selected underlying agent architecture.
3. Both the frontend and backend implementations pushed to your respective GitHub repositories. Keep committing your changes frequently!

---

## Technical Guidance: How to integrate both agents to the same UI

To make both the Standard Agent and the Deep Agent work within the same UI, we will use **LangGraph Graph IDs**.

Since both architectures utilize the same underlying LangChain-native communication, the Deep Agent UI can handle both easily. You do not need to create two separate backends. Instead, you should:

### 1. Unified Backend Architecture

Keep both agent implementations in the same repository. When you run `langgraph dev`, it will automatically expose both agents as valid endpoints on the same port (e.g., `127.0.0.1:2024`).

In your `langgraph.json`, define both:

```json
{
  "graphs": {
    "standard_agent": "./baseline_agent.py:graph",
    "deep_agent": "./deep_agent.py:graph"
  },
  "env": ".env"
}
```

### 2. State Schema Consistency (Critical for UI)

Both agents **must** store their conversation history in a key named `messages`. This is what the `ChatInterface` component in the UI listens to.

### 3. Frontend Integration (Deep-Agents UI)

The frontend uses the `@langchain/langgraph-sdk` to talk to your backend. To implement the selector:

- **Hook to use**: The UI uses the `useChat` hook. It accepts an `assistantId` parameter.
- **The Selector**: Create a simple React component (dropdown or toggle) that updates a state variable (e.g., `activeAgentId`).
- **Dynamic Connection**: Pass this `activeAgentId` into your LangGraph client configuration. When the user flips the toggle, the UI will reconnect to the corresponding graph ID (`standard_agent` or `deep_agent`).

> [!TIP]
> **Prompting your Vibe-Coding tool:**
> If you're stuck, use a prompt like this:
> *"I have two LangGraph graphs defined in my backend: 'standard_agent' and 'deep_agent'. Update the Deep-Agents UI (Next.js) to include a dropdown selector that allows the user to switch the `assistantId` used by the `useChat` hook so they can toggle between these two agents at the start of a thread."*
