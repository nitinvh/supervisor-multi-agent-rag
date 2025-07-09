# Supervisor Multi-Agent System
This project implements a sophisticated multi-agent system orchestrated using LangGraph, featuring a central Supervisor agent that intelligently delegates tasks to specialized Researcher and Coder agents. This architecture allows for dynamic task routing, iterative refinement of solutions, and robust problem-solving based on user queries.

## Project Description
Traditional single-agent systems can struggle with complex, multi-faceted tasks. This project addresses that by creating a collaborative environment where different AI agents specialize in distinct functions:

Supervisor Agent: Acts as the central orchestrator, receiving user queries, deciding which specialized agent (Researcher or Coder) is best suited for the current task, evaluating their outputs, and determining if further iterations or a final answer are needed.

Researcher Agent: Specializes in information retrieval and synthesis. When a query requires external knowledge, the Supervisor delegates to the Researcher.

Coder Agent: Specializes in generating and executing code. When a query requires code generation, logical problem-solving through code, or script creation, the Supervisor delegates to the Coder.

The system's strength lies in its ability to adaptively route tasks, allowing for efficient resource utilization and a more comprehensive approach to problem-solving. The iterative feedback loop, where the Supervisor evaluates and potentially re-delegates, ensures a high-quality final output.

## Technologies Used
Python: The core programming language for the entire system.

LangChain: A framework for developing applications powered by large language models, used here for building the individual agents and their capabilities.

LangGraph: An extension of LangChain specifically designed for building stateful, multi-actor applications with LLMs, enabling the complex workflow and conditional routing between agents.

OpenAI GPT-4: The powerful Large Language Model (LLM) used across all agents for understanding queries, generating responses, making decisions, and producing code.

Tavily Search API: Integrated within the Researcher agent to provide real-time, relevant information retrieval from the web.

PythonREPL: Used by the Coder agent to execute generated Python code and return results.

## Architecture and Workflow
The system's workflow is defined as a graph where the Supervisor agent directs the flow based on the nature of the task and the intermediate results.

![image](https://github.com/user-attachments/assets/3a7feeea-6a60-4b48-b6ec-27e2228d56a3)


START Node: The initial entry point where the user's query is received.

SUPERVISOR Node:

This is the central decision-making unit. It receives the initial user query (or the output from a previous agent).

Decision Logic: Based on the query's content and the current state, the Supervisor decides:

If the query requires information gathering, it routes the task to the RESEARCHER.

If the query requires code generation or logical problem-solving, it routes the task to the CODER.

If the Supervisor determines that a satisfactory answer has been achieved or no further steps are needed, it routes to END.

Evaluation & Iteration: After an agent (Researcher or Coder) completes its task, its output is returned to the Supervisor. The Supervisor then evaluates this output. If the output is not sufficient or requires further refinement/different approach, the Supervisor can re-route the task back to the same agent, or to the other agent, effectively creating a feedback loop until the task is complete.

RESEARCHER Node:

Activated by the SUPERVISOR when information retrieval is needed.

Utilizes Tavily Search API to search the web for relevant data, articles, or facts.

Synthesizes the gathered information and returns it to the SUPERVISOR.

CODER Node:

Activated by the SUPERVISOR when code generation or logical scripting is required.

Generates Python code (or other specified languages) to address the query.

Executes the generated code using PythonREPL and returns the execution results (along with the code itself) to the SUPERVISOR.

Returns the generated code and results to the SUPERVISOR.

END Node:

The termination point of the graph. The system stops when the SUPERVISOR determines the task is complete and the final answer is ready.
