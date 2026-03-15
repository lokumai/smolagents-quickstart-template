# Week 1: Prerequisites & Development Environment Setup

In this project, we will design an AI Agent chatbot that answers complex questions about a software repository's architecture and logic. We will utilize two different agent architectures: a ReAct Agent and a Deep Agent. Ultimately, we will write and publish a research paper comparing the performance and efficiency of these two agents on the SWE-QA dataset.

Below are the prerequisites and the required tasks for the first week.

---

## Part 1: Theoretical Foundations (What to Learn)
You must understand the vocabulary and the basic mechanics of modern AI architecture. Please research and read up on the following concepts:

- [ ] **LLM Fundamentals:** What is a Large Language Model? Understand context windows, tokens, temperature, and API limits.
- [ ] **RAG (Retrieval-Augmented Generation):** How to give an LLM "memory" by using Vector Databases to retrieve relevant text chunks before answering.
- [ ] **Tool Calling:** How LLMs interact with the outside world by triggering functions (e.g., getting the weather, reading a file).
- [ ] **MCP (Model Context Protocol):** What is it? Why is it the new standard for connecting AI systems to external data?
- [ ] **MCP Servers:** Understand how MCP Servers work and how they expose specialized data or tools to an LLM.
- [ ] **LLM vs. Agent:** What is the difference between a simple text-generation model and an "Agent" that has autonomy and goals?
- [ ] **ReAct Agent (Multi-step Agent):** Learn the "Reason-then-Act" loop. How does an agent constantly observe its environment and loop until a goal is met?
- [ ] **Deep Agent:** Refer to the [LangChain Deep Agents Documentation](https://docs.langchain.com/oss/python/deepagents/overview). Understand how hierarchical architectures, task decomposition (planning), and sub-agents solve the context overflow issues found in standard ReAct agents.

*(Note: We will provide mini-courses outlining some of the topics above, but independent research is highly encouraged.)*

---

## Part 2: Environment Setup (What to Do)
As an AI researcher and software engineer, your tooling must be flawless. Follow these steps to set up your "Vibe-Coding" environment.

### 1. Version Control Setup
- [ ] **Learn Git & GitHub:** If you do not know Git, take a crash course. You must know how to commit, push, pull, and branch.
- [ ] **Repository Setup:** Ensure you have access to the main project repository and can clone it locally.

### 2. Set Up Antigravity (Gemini Pro)
- [ ] **Get your Subscription:** Sign up for the Gemini Pro Student subscription.
- [ ] **Install Antigravity:** Set up the Antigravity application/CLI on your machine.
- [ ] **Connect MCP Servers:** Hook up your Antigravity setup to the following MCP Servers so that your AI assistant becomes a domain expert:
    - **LangChain Docs MCP** (so it knows the latest library syntax)
    - **DeepWiki MCP** (so it knows the repository analysis patterns)

### 3. Set Up VS Code & Copilot Pro
- [ ] **Get GitHub Student Developer Pack:** Apply for the student pack using your university email.
- [ ] **Claim Copilot Pro:** Activate your free Copilot Pro subscription via the Student Dev Pack.
- [ ] **Install VS Code Extension:** Install the GitHub Copilot extension inside Visual Studio Code.
- [ ] **Connect MCP Servers to Copilot:** Configure VS Code/Copilot to also connect to the **LangChain Docs** and **DeepWiki** MCP servers, ensuring your in-editor completions are context-aware.

---
> [!TIP]
> **Why all this setup?** 
> By the time Week 2 starts, we want you to focus purely on the *ideas, the workflow, and the experiments*. If you encounter a bug, your IDE should be smart enough to read the LangChain docs and fix it for you. This is what we call **"Vibe-Coding."**
