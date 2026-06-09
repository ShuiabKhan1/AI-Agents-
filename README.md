Core Concepts


Agents¶
Autonomous systems that execute tasks by selecting and running actions. Each agent has:

agent_card - Metadata (name, description, version, URL)
execute() - Main entry point for processing requests


Actions¶
Building blocks that agents use to accomplish tasks. Built-in types:

Tools - Perform operations and return results
Outputs - Send messages to users
MCP - Integrate tools from MCP servers
RemoteAgent - Call other agents via A2A
If you'd like you can also implement additional action classes yourself. All actions are Pydantic models with auto-generated JSON schemas and access to shared memory.


Orchestrators¶
Define how agents execute tasks. Available strategies:

ReAct (default) - Simple reasoning + Acting loop
PlanAct - Strict planning, then acting
CodeAct - Python code generation with dynamic tool discovery for safe action execution
Orchestrators manage action selection, state (records, memory), and termination.


Events¶
Communication mechanism during execution. Types: START, STATUS, CHUNK, OUTPUT, CONTENT, ERROR, END.

Each event has routing properties:

output - Stream to user via A2A artifact
record - Add to LLM context
append - Append to previous artifact (streaming)
last_chunk - Mark as final chunk in stream
stop - Signal execution end
propagate - Bubble event through remote agents to the original caller's SSE stream
pacer - Publish event to PACER when yielded (requires pacer_config)



An Agent SDK (Software Development Kit) is a programming framework that helps developers build AI agents. Instead of building the "thinking" and "doing" loop from scratch, developers use an SDK to quickly provide Large Language Models (LLMs) with tools, memory, and environments to autonomously execute multi-step tasks. 

Download Claude Code
 +3
What Do They Actually Do?
Building an effective AI agent requires heavy "plumbing" to keep it running properly. An Agent SDK handles the following core mechanics: 

Microsoft Learn
 +1
Autonomous Tool Loops: Instead of you manually writing code to execute a function and feeding the result back into the model, the SDK's built-in loop handles the Model decides → Tool runs → Result returns cycle automatically. 

Download Claude Code
 +1
Built-in Tools: SDKs provide ready-to-use capabilities like file reading/writing, web searching, running terminal commands, and interacting with codebases. 

Download Claude Code
 +1
Sandboxing: Many SDKs (like OpenAI's) integrate with isolated computer environments (sandboxes) where the model can safely read files, install dependencies, and run code without compromising your system. 

OpenAI
 +1
State & Memory Management: SDKs track conversation histories, prevent the model's context window from overflowing, and allow agents to resume tasks across multiple sessions. 

Microsoft Learn
 +1
Multi-Agent Orchestration: Many modern SDKs allow developers to build multi-agent networks where specialized agents collaborate or delegate tasks to one another. 

OpenAI Developers
 +1
Why Not Just Use Standard API Calls?
With a standard API client, you have to write the code that stops the LLM when it wants to use a tool, executes that tool on your server, and formats the response back to the LLM. An Agent SDK abstracts that entire process away so you can just declare the agent's goal and let it work. 

Download Claude Code
 +3
Examples of Popular Agent SDKs
Major technology and AI companies provide SDKs tailored to specific ecosystems: 
OpenAI Agents SDK: A framework that provides a model-native harness and native sandbox support for building file-editing and code-writing agents. 

OpenAI
Claude Agent SDK: Anthropic's library that gives developers the same built-in agent loop and context management that powers Claude Code. 

Download Claude Code
Microsoft 365 Agents SDK: A framework specifically designed to help developers connect agents to enterprise systems, Microsoft Teams, and business apps. 

Microsoft Learn
Agent SDKs are fundamentally transforming how AI is used, shifting it from simple text-chat interfaces into autonomous systems capable of executing complex work like auditing code, researching, and operating software
