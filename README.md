Core Concepts¶
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
