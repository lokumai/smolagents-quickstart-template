# Week 2: Scaffoling

## Overview

This week you should start coding. In this project you must only do vibe-coding, meaning that you should not write any code by yourself. You should use AI tools to generate code for you by prompt engineering. 2 tools you can use for free with your student email are Google Antigravity and Github Copilot (its VSCode extension). 

to briefly summarize, in this project you will implement two different code agents with different  architectures, ReAct and Deep Agents, and compare their performance on the SWE-QA dataset, and the results will be written in a research paper. Also you will create a chatbot UI so users can ask questions to agents regarding any codebase.

## Prerequisites

#### Vibe-Coding Tools with MCP
Have your vibe-coding tools ready. Any tool you choose, MUST be connected to DeepWiki MCP and LangChain MCP servers. Both of these tools allow your AI agents to query the latest LangChain/Deep-Agents documentation in real-time and write proper code for you. NEVER forget to ask the tool to use DeepWiki MCP and LangChain MCP servers in your prompts. 
As for the LLM in your vibe-coding tool, you can use any model you want, but it is recommended to use "Gemini Flash 3.0" and "GPT 5.4 mini" which are both capabale and cost-effective. Otherwise your monthly credit will run out soon.

#### API Key
As you know, these AI Agents that you gonna implement use LLMs as their brain. Running LLMs required for this project requires huge GPUs which we do not have. So you should connect your agent to cloud LLMs. 
There are a few options for you to get LLM Inference for free:

- [Google AI Studio](https://aistudio.google.com/) : This is a platform for using Google's LLMs. Here you can get an API Key which has daily limits. I suggest using the cheapest models which have higher limits such as "Gemini Lite" series. You can create account with multiple emails to get multiple keys.

- [OpenRouter](https://openrouter.ai/) : This is a platform that provides access to almost all cloud LLMs in the world. Some of its models are free with a limited daily qouta. You can create account with multiple emails to get multiple keys.

- [Google Cloud](https://cloud.google.com/pricing?hl=en) : Google Cloud provides about 300$ of free credits in which you can use for running their LLMs. I suggest not using this now and keep this credit for experiments of your research paper on SWE-QA dataset. For this you should use googles [Vertex AI](https://cloud.google.com/vertex-ai?hl=en) Service.

- [Azure](https://azure.microsoft.com/en-us/products/ai-services/openai-service) : Azure provides about 100$ of free credits with your github student pack (that you can get with your university email) in which you can use for running their LLMs. I suggest not using this now and keep this credit for experiments of your research paper on SWE-QA dataset. For this you should use [Azure Foundry](https://azure.microsoft.com/en-us/products/ai-foundry/models) Service.

## Tasks

This week you will only implement a Deep Agent and its UI.

#### 1. UI Setup
For this project you will later write a UI. But for now in order to progress and prototype faster, you can use the UI provided by LangChain:
- For Deep Agent: [Deep Agents UI](https://github.com/langchain-ai/deep-agents-ui)


#### 2. Deep Agent Implementation
Use the Langchain Deep Agents library (Python version) to implement a Deep Agent that can answer questions about a software repository. 
- [Langchain Deep Agents](https://github.com/langchain-ai/deepagents)

This Deep Agent must have all the default tools of Deep Agent library including:
- Planning Tool
- Virtual Filesystem
- Shell 
- Sub-agents
- Context Summarization

IMPORTANT NOTE: When implementing the Deep Agent, ask your vibe-coding tool to use the "uv" package manager instead of "pip". This is because "uv" is much faster and more efficient than "pip".

#### 3. Connect Agent and UI
Deploy the agent using `langgraph dev` as shown in the UI's documentation and README. 

#### 4. Ask Questions to the Agent
Give agent access to any code repository you want and ask it to answer questions about it. For example, you can ask it to "Explain the architecture of this repository" or "Find the function that handles user authentication". 

#### 5. Share your Codes
For this project, we will have one frontend and one backend repositories. For the frontend for now use the UI provided by LangChain and create a github repository for it in your github account. Also create another repository for the backend in your github account. 

All your codes should be always in your github account and you should commit and push the latest version of your code regularly. You should use git effectively, and frequenelty even for small changes, commit and push your code.

If you add Github MCP server to your vibe-coding tools, your vibe-coding tool can manage git operations for you. 

Share the links of these repositories with me and add me as collaborator.
My github: https://github.com/amirkiarafiei
My email: amirkia.rafiei@gmail.com

