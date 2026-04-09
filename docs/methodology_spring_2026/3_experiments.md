# Week 4: Experimental Setup and Execution

## Overview

Now that both the baseline (ReAct-style) agent and the Deep Agent are functional and integrated into the UI, it is time to move on to the core of the research project: the empirical experiments. 

This week, you will run both agents against the **SWE-QA benchmark** to compare their performance, reasoning workflows, and efficiency. 

As always, remember to use your "Vibe-Coding" tools connected to the LangChain Docs MCP and DeepWiki MCP to write the automation scripts quickly and correctly.

## Experimental Configurations

You will compare the two distinct architectures on the SWE-QA questions:

### 1. The Baseline Agent (ReAct-style)
- **Tools:** Must remain strictly limited to the three tools from the original SWE-QA paper: `read_file`, `get_repo_structure`, and `search_rag`.
- **Architecture:** Standard multi-step reasoning using standard LangChain `create_agent()`. It solves tasks purely through its RAG and file-reading tools.

### 2. The Deep Agent
- **Tools:** Uses its original, default action space (including the virtual filesystem, etc.).
- **CRITICAL System Prompt Update:** You must modify the fixed **System Prompt** of the Deep Agent. You must explicitly instruct the agent that for *any* given task or question, it **MUST ALWAYS** use a **TODO list** for planning, and it **MUST ALWAYS** use the **generic sub-agent** (which is provided by default in the LangChain Deep Agents library) to investigate and answer the question.
- **Architecture:** Hierarchical task decomposition. We are testing whether delegating code-understanding tasks to a sub-agent outperforms a flat ReAct structure.

## Execution Rules

To ensure scientific validity and avoid data contamination, you must strictly follow these execution rules:

### 1. Strict Context Isolation (One by One)
The agents must answer the SWE-QA questions **one by one**. 
- The system prompt remains fixed for the agent across all questions.
- However, **each question MUST be asked in a completely new, clean context (a new thread).** 
- Do *not* ask multiple questions sequentially within the same conversation thread. Starting a fresh thread for every question ensures previous codebase context does not poison or help the current question.

### 2. Comprehensive Log Storage (Critical Requirement)
The analysis phase of this research relies entirely on the execution traces, not just the final output. You are required to **keep and store ALL agent logs** emitted by the LangGraph framework when answering the questions.
- For each question answered in the SWE-QA dataset, save the complete execution logs (all tool calls, planner actions, sub-agent spawns, and internal reasoning steps).
- You must structure these logs cleanly on disk (e.g., in JSON files grouped by `question_id` and `agent_type`).
- In the coming weeks, we will use these exact logs to perform qualitative analysis (Error Taxonomy) to understand the pros and cons of the ReAct vs. Deep Agent workflows. If you do not save the raw logs now, your experiments will have to be rerun.

### 3. Strict Virtual Filesystem Isolation
When setting up the environment for an agent to answer a question, its virtual filesystem **MUST ONLY** contain the specific code repository relevant to that question.
- **IT IS NOT ACCEPTABLE AND YOUR RESEARCH METHODOLOGY WILL BECOME INVALID IF** the agent has access to multiple repositories simultaneously. For example, if a question is about Repository A, then Repositories B and C must **not** be mounted or accessible in the agent's virtual filesystem. 
- Each question that the LLM is prompted about should have the environment required to answer that specific question ONLY. Nothing more, nothing less.

## 💰 Cost Management & LLM Selection

Running the entire SWE-QA dataset involves thousands of questions and will consume a substantial amount of LLM credits. To avoid running out of funding halfway through your experiments:
- **Funding Sources:** You must utilize the free credits provided by **Google Cloud Vertex AI** and **Azure Foundry** that you acquired via your student packs.
- **Model Selection:** These credits are **not enough** if you recklessly use top-tier, expensive models. You must select and run the experiments using **mid-priced or cheap models** (such as `GPT-OSS-120B`, `Gemini 3 Flash`, etc.).
- **Execution Strategy:** Start by running the *entirety* of SWE-QA using a **single LLM** across both agent types. This guarantees you will have at least one complete baseline comparison for the final paper. If you have credits remaining at the end of the project, you may then test other LLMs to strengthen your findings.

## Tasks for this Week

1. **Update Deep Agent Prompt:** Modify the Deep Agent's system prompt to enforce the strict use of TODO lists and the generic sub-agent as directed above.
2. **Write an Automation Script:** Use your AI tools to write a script that iterates through the SWE-QA dataset.
3. **Execute and Log:** Have the script send questions to both the Baseline Agent and the Deep Agent (in isolated threads). Ensure the script saves both the final response and the complete framework logs to disk for every single question.

## Success Criteria

By our next meeting, you must have:
1. An automated script capable of running the SWE-QA dataset through both agents.
2. A pilot run of the dataset completed.
3. A clearly organized directory containing the full execution logs and final answers for each question, separated by agent architecture.

## What's Next? (Next Week)

Next week, you will receive a new methodology document detailing the **Evaluation and Analysis** protocol. However, we cannot proceed to that stage unless you have your data. Until our next meeting, your sole priority is completing all the experiments outlined above and ensuring every single log is maintained in a clean, perfectly formatted directory structure.

---

## ⚠️ Critical Warnings and Penalties

To ensure the scientific integrity of this empirical study, strict adherence to the methodology is absolutely required. **You will face grading penalties if any of the following occur:**

1. **Missing Logs:** If you forget to keep and store all of the execution logs emitted by the framework.
2. **Poor Log Organization:** If the logs are not stored in a clear, proper way (for example, if it is not known which specific agent trajectories and tool calls belong to which specific SWE-QA question).
3. **Deep Agent Protocol Violation:** If the Deep Agent possesses any extra tools other than its default tools, or if it fails to use both the sub-agents and the TODO list for planning/answering questions in *all* scenarios.
4. **Baseline Agent Protocol Violation:** If the ReAct (baseline) agent includes any extra tools other than the minimal set strictly mentioned in the SWE-QA paper.
5. **Context/Thread Leakage:** If during benchmarking, a completely new and clean thread is not created for every single prompt.
