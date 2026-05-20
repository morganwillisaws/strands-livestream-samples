# Strands Agents Livestream Samples

Sample code from the Strands Agents livestream series. Each episode builds on the previous one, progressing from a simple "hello world" agent to a fully deployed agent on Amazon Bedrock AgentCore with memory, guardrails, and knowledge base integration.

## Episodes

### [Episode 1: Getting Started with Strands Agents](./episode-1/)

Introduction to the Strands Agents SDK — building your first agent, adding tools, using different model providers, and connecting to MCP servers.

**Topics covered:**
- Creating a simple agent
- Adding custom tools
- Using community tools (strands-agents-tools)
- Switching model providers (Bedrock, Anthropic, OpenAI, Ollama)
- Connecting to MCP servers over HTTP

### [Episode 2: Conversation Management & Skills](./episode-2/)

Building a production-style customer service agent with conversation memory, system prompts, steering, and skills.

**Topics covered:**
- System prompts and steering/guardrails
- Agent Skills for guided workflows
- Conversation memory strategies (sliding window, summarization)
- Session persistence (file-based and S3)
- Custom event handlers

### [Episode 3: Deploying to Amazon Bedrock AgentCore](./episode-3/)

Taking a Strands agent from local development to cloud deployment with Amazon Bedrock AgentCore, adding knowledge base retrieval, guardrails, and persistent memory.

**Topics covered:**
- AgentCore CLI workflow (create, dev, deploy, invoke)
- Knowledge Base integration for RAG
- Bedrock Guardrails for content safety
- Semantic and summarization memory strategies
- IAM permissions and production configuration

## Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/getting-started/installation/) package manager
- AWS account with Bedrock model access enabled
- AWS CLI configured

## Quick Start

```bash
# Clone the repo
git clone https://github.com/aws-samples/strands-livestream-samples.git
cd strands-livestream-samples

# Create a virtual environment
uv venv
source .venv/bin/activate

# Install base dependencies
uv pip install strands-agents strands-agents-tools

# Run the simplest example
python episode-1/simple_agent.py
```

## Resources

- [Strands Agents SDK](https://github.com/strands-agents/sdk-python)
- [Strands Agents Tools](https://github.com/strands-agents/tools-python)
- [Amazon Bedrock AgentCore Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/agentcore.html)
- [Amazon Bedrock for Beginners](https://github.com/aws-samples/sample-amazon-bedrock-for-beginners) — Knowledge Base setup guide

## License

This project is licensed under the MIT License.
