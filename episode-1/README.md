# Episode 1: Getting Started with Strands Agents

📺 [Watch on YouTube](https://www.youtube.com/watch?v=HFLZT01UVqc)

Introduction to the Strands Agents SDK — building your first agent, adding tools, using different model providers, and connecting to MCP servers.

## Setup

```bash
# From the repo root
source .venv/bin/activate

# Install dependencies
pip install strands-agents strands-agents-tools "mcp[cli]"

# Optional: for local models with Ollama
brew install ollama
ollama serve
ollama pull gemma4:latest
```

## Files

| File | Description |
|------|-------------|
| `simple_agent.py` | Minimal "hello world" agent — just 3 lines of code |
| `agent_with_tools.py` | Agent with custom tools and community tools (calculator, current_time) |
| `community_tools.py` | Using pre-built tools from strands-agents-tools |
| `model_providers.py` | Switching between Bedrock, Anthropic, OpenAI, and Ollama |
| `mcp_http.py` | Connecting to MCP servers (remote Streamable HTTP + local stdio) |

## Running the Examples

```bash
# Simplest possible agent
python episode-1/simple_agent.py

# Agent with custom + community tools
python episode-1/agent_with_tools.py

# MCP server integration (AWS knowledge + pricing)
python episode-1/mcp_http.py
```

## Topics Covered

- **Simple agent** — Create an agent with `Agent()` and call it with a prompt
- **Custom tools** — Use the `@tool` decorator to give agents new capabilities
- **Community tools** — Pre-built tools like `calculator`, `current_time`, `shell`, `http_request`
- **Model providers** — Swap between Bedrock, Anthropic, OpenAI, and Ollama with one line
- **MCP integration** — Connect to remote (Streamable HTTP) and local (stdio) MCP servers
- **Agent metrics** — Access cycle counts, token usage, and duration from results
