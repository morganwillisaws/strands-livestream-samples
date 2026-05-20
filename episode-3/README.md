# Episode 3: Deploying Strands Agents with Amazon Bedrock AgentCore

This episode covers deploying a Strands agent to Amazon Bedrock AgentCore — from local development to cloud deployment with memory, guardrails, and knowledge base integration.

## Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/getting-started/installation/) package manager
- AWS CLI configured with appropriate credentials

## Setup

```bash
# Create and activate a virtual environment
uv venv
source .venv/bin/activate

# Install Strands Agents SDK and tools
uv pip install strands-agents strands-agents-tools

# Install the AgentCore CLI (requires Node.js 20+)
npm install -g @aws/agentcore

# Verify the CLI is available
agentcore --help
```

## Setting Up the Knowledge Base

This agent uses an Amazon Bedrock Knowledge Base to answer university FAQ questions. To create one:

1. Follow the instructions in the [Amazon Bedrock for Beginners](https://github.com/aws-samples/sample-amazon-bedrock-for-beginners) repository to set up a Knowledge Base with your own documents and a Guardail. Choose the 
2. Once created, note the **Knowledge Base ID** and **Guardrail ID** from the AWS console.
3. Update the `KNOWLEDGE_BASE_ID` variable in your agent's `main.py`.

## AgentCore CLI Workflow

### 1. Create a new AgentCore project

```bash
agentcore create --project-name UniversityBot --defaults
```

This scaffolds a new project with the standard directory structure:

```
universitybot/
├── agentcore/
│   ├── agentcore.json      # Agent configuration (runtimes, memories, etc.)
│   └── .cli/               # CLI state and logs
├── app/
│   └── MyAgent/
│       ├── main.py         # Your agent code
│       └── pyproject.toml  # Python dependencies
└── README.md
```

### 2. Run locally in development mode

```bash
agentcore dev
```

This starts your agent locally with hot-reload. You can interact with it directly in the terminal to test before deploying.

### 3. Add memory to your agent

```bash
agentcore add memory --name UniversityBotMemory --strategies SEMANTIC,SUMMARIZATION
```

This configures memory in your `agentcore.json` so the agent can remember context across sessions using semantic search and conversation summarization.

### 4. Deploy to AWS

```bash
agentcore deploy
```

This packages your agent, builds a container, and deploys it to Amazon Bedrock AgentCore. The CLI handles CDK synthesis, ECR image push, and runtime provisioning.

### 5. Invoke the deployed agent

```bash
agentcore invoke '{"prompt": "When does CS 201 meet?"}'
```

To test memory across turns, use a consistent `session_id` and `actor_id`:

```bash
agentcore invoke '{"prompt": "My name is Morgan", "actor_id": "demo_user"}' --session-id my-session-123

agentcore invoke '{"prompt": "What is my name?", "actor_id": "demo_user"}' --session-id my-session-123
```

## Agent Features

- **Knowledge Base retrieval** — Uses the Strands `retrieve` tool to search university policies and FAQs
- **Guardrails** — Bedrock Guardrails applied to model invocations for content safety
- **Memory** — Semantic and summarization strategies for cross-session context
- **Custom tools** — `lookup_course` tool for course schedule queries

## Files

| File | Description |
|------|-------------|
| `strands_agent_local.py` | Run the agent locally without AgentCore |
| `strands_agent_memory.py` | Local agent with memory integration |
| `demo-commands.txt` | Quick reference commands used in the livestream |

## IAM Permissions

Your AgentCore execution role needs permissions for:

- `bedrock:InvokeModel` / `bedrock:InvokeModelWithResponseStream` — Model access
- `bedrock:ApplyGuardrail` — Guardrail evaluation
- `bedrock:Retrieve` — Knowledge Base queries
- `bedrock-agentcore:*` memory actions — Memory read/write
- CloudWatch Logs and X-Ray — Observability

The `agentcore deploy` command creates a role with base permissions automatically. If you add a knowledge base or guardrail, you may need to attach additional permissions to the role (see the [demo-commands.txt](./demo-commands.txt) for the role ARN).
